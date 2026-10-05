# Plan

## Diagnosis

The PostgreSQL health check in `api/routes/health.py` executes the raw SQL string `"SELECT 1"` through SQLAlchemy's `AsyncSession`.

Issue #61 reports that this raw SQL execution causes the PostgreSQL health probe to be marked unhealthy. The issue evidence refers to an `ArgumentError`.

My local reproduction independently confirmed that the raw SQL string is not accepted by the SQLAlchemy execution path. The direct SQLAlchemy reproduction raised:

> `sqlalchemy.exc.ObjectNotExecutableError: Not an executable object: 'SELECT 1'`

The health-check reproduction also showed the PostgreSQL dependency as `unhealthy`.

The common defect is that the health check passes a plain Python string to `db.execute()` instead of SQLAlchemy's executable `text()` construct.

The intended fix is:

```python
from sqlalchemy import text
```

and:

```python
db.execute(text("SELECT 1"))
```

instead of:

```python
db.execute("SELECT 1")
```

The Redis health-check failure observed during the local reproduction is a separate problem and is outside the scope of issue #61.

## Scope

### In scope

* Update the PostgreSQL health-check query in `api/routes/health.py`.
* Import SQLAlchemy's `text` construct.
* Replace `db.execute("SELECT 1")` with `db.execute(text("SELECT 1"))`.
* Add or update the focused health-check regression test under the repository's existing test structure.
* Remove the seeded `xfail` marker associated with the issue if the regression test is currently marked as expected to fail.
* Verify the PostgreSQL health dependency reports `healthy` when the database probe succeeds.
* Re-run the reproduction for issue #61 after the implementation.
* Run the repository's unit-test command, including `make test-unit` if that is the repository's documented command.
* Review the related `api.routes.health` mypy configuration in `pyproject.toml`.

### Out of scope

* Redis health-check behavior and issue #62.
* Dependency upgrades or downgrades.
* Database infrastructure or application configuration changes.
* Unrelated health-check refactoring.
* Unrelated raw-string `execute()` call sites.
* Changing exception handling unless testing demonstrates that it is required for issue #61.
* Treating the overall HTTP 503 response as evidence that the PostgreSQL fix failed, because Redis can independently cause the overall endpoint to return 503.

## Files to Change

1. `api/routes/health.py`

   * Import `text` from SQLAlchemy.
   * Replace the raw `"SELECT 1"` query with `text("SELECT 1")`.
   * Leave the remaining PostgreSQL health-check logic unchanged.

2. The existing focused health-check test file under `tests/`

   * Follow the repository's existing test naming and organization.
   * Exercise the actual SQLAlchemy execution path rather than a mock that would accept an invalid raw SQL string.
   * Remove the seeded `pytest.mark.xfail` marker associated with issue #61 if it is present.
   * Verify that the PostgreSQL health dependency reports `healthy` after the fix.

3. `pyproject.toml`

   * Review the existing `api.routes.health` type-checking configuration related to issue #61.
   * Remove or update the issue-specific suppression if it is no longer necessary after the implementation.
   * Do not change unrelated type-checking configuration.

## Approach

1. Inspect `api/routes/health.py` and confirm the current PostgreSQL health check uses `db.execute("SELECT 1")`.

2. Review the existing health-check tests, `tests/conftest.py`, `pyproject.toml`, and `docs/CONTRIBUTING.md` before changing the test structure.

3. Identify the existing regression test associated with issue #61 and determine whether it is marked with `pytest.mark.xfail` because the seeded bug is expected to fail.

4. Import SQLAlchemy's `text` construct in `api/routes/health.py`.

5. Replace:

   ```python
   db.execute("SELECT 1")
   ```

   with:

   ```python
   db.execute(text("SELECT 1"))
   ```

6. Leave the existing PostgreSQL health-check exception handling and unrelated Redis logic unchanged.

7. Update the focused regression test so it exercises the corrected SQLAlchemy execution path and verifies that the PostgreSQL health dependency reports `healthy`.

8. Remove the seeded `xfail` marker from the regression test because the issue should no longer be expected to fail after the fix.

9. Review the `api.routes.health` mypy suppression in `pyproject.toml` and remove or update it if the fixed code no longer requires it.

10. Create the implementation branch using the repository convention:

```text
fix/61-<short-description>
```

11. Run the focused regression test.

12. Run the repository's relevant unit checks, including `make test-unit` if required by the repository documentation.

13. Re-run the original issue #61 reproduction after the implementation.

14. Confirm that the PostgreSQL health probe no longer becomes unhealthy because of the raw `"SELECT 1"` execution.

15. Keep Redis issue #62 separate from the verification because it may continue to make the overall health endpoint return HTTP 503.

## Test Plan

### Baseline

The local reproduction before the fix showed:

```text
sqlalchemy.exc.ObjectNotExecutableError:
Not an executable object: 'SELECT 1'
```

The health-check reproduction also reported:

```text
postgres: unhealthy
redis: unhealthy
vector_db: healthy
```

The Redis result is treated separately because it corresponds to the unrelated Redis health-check problem.

### Regression test

Run the focused health-check regression test after changing the query.

The test should use the repository's existing test conventions and exercise an actual SQLAlchemy execution path rather than a mock that accepts arbitrary SQL strings.

Verify that:

```python
db.execute(text("SELECT 1"))
```

executes successfully and that the PostgreSQL health dependency reports:

```text
healthy
```

### Repository checks

Run:

```text
make test-unit
```

if this is the repository's documented unit-test command, along with any focused test command required by the existing test setup.

Review the resulting test output for failures related to the change.

### Endpoint verification

Run the health-check reproduction again after the implementation.

The PostgreSQL dependency should no longer be reported as unhealthy because of the `"SELECT 1"` execution.

Do not use an overall HTTP 503 response alone as the success criterion because Redis issue #62 can independently cause the endpoint to return HTTP 503.

### Final verification

Compare the post-fix reproduction with the baseline and confirm that the PostgreSQL SQL-execution failure is resolved.

## Risks and Unknowns

* The local reproduction uses SQLite to expose the SQLAlchemy execution problem, so it may not reproduce every PostgreSQL-specific behavior. The repository's existing health-check test and the original reproduction should both be used for verification.

* A mocked database session could hide the defect because a mock may accept a raw SQL string. The regression test should exercise the actual SQLAlchemy execution path.

* Redis issue #62 can continue to make the overall health endpoint unhealthy even after the PostgreSQL problem is fixed.

* The existing `pytest.mark.xfail` marker may be part of the seeded issue setup and should be removed only for the regression test associated with issue #61.

* The `api.routes.health` mypy suppression may be tied to the seeded defect. It should be reviewed and removed or updated only if the fixed code no longer requires it.

* Other raw SQL string executions may exist elsewhere in the repository. They remain outside the scope of issue #61 unless the implementation evidence shows they are directly related.

## Deviations


The implementation stayed within the planned scope, but several test and verification details differed from the original plan:

* No existing focused health-check regression test or seeded `xfail` marker was present, so I created a new `tests/unit/test_health.py` instead of modifying an existing test or removing an `xfail` marker.
* The regression test uses a real SQLAlchemy `AsyncSession` object, but its `execute()` method is controlled by the test so the submitted statement can be inspected as a SQLAlchemy `TextClause`. It does not connect to a live PostgreSQL database. This isolates the SQLAlchemy execution defect from external database availability.
* The focused regression test was run before the production fix and failed because the captured statement was the raw string `"SELECT 1"`. After changing the health check to `text("SELECT 1")`, the test passed.
* Instead of `make test-unit`, the repository unit tests were run with `python -m pytest tests -m unit -v`. The resulting suite completed with 376 passed and 53 expected failures (`xfailed`).
* `pyproject.toml` was reviewed, but no type-checking configuration was changed because the existing configuration was not required to be modified for this fix.
* The Redis health-check issue remained unchanged and was treated as out of scope for Issue #61.


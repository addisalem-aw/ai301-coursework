# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

Where it lives

In an eval bundle, read the plan-context block's scope pair, intended behavior, and deviation notes. Compare them with the candidate PR's diff, changed-file list, commits, and description.

In live mode, read plan.md and its deviation notes, inspect the branch's diff against the target branch, and compare the draft PR title and description with the actual changes.

Check both the implementation and any claims that the PR follows the plan or completes the intended fix.

What good looks like

Every changed file and material behavior change falls within the plan's stated boundary or is explained by a documented, justified deviation. The description accurately represents what the diff implements, including incomplete work and limitations. Unexplained omissions, extra changes, or claims contradicted by the diff indicate silent drift.

## Test evidence (harness category: not-tested)

Where it lives

In an eval bundle, read the candidate PR's test-evidence section, including before-and-after behavior, the plan-context block's test plan, and the original reproduction steps and expected behavior.

Inspect the reported results of the repository's required tests and checks in the package's test-evidence section or captured execution output.

In live mode, compare the plan's test plan with the added or modified tests, captured test output, and results of the relevant repository test suite and required checks.

Verify the reported result against the actual test output when available; do not rely only on the PR description's statement that tests pass.

What good looks like

The evidence identifies an observable behavior, states the expected result after the fix, and demonstrates whether the relevant test or reproduction achieved that result. Required repository checks have visible outcomes. A statement such as "tests pass" without supporting results, tests that do not exercise the reported failure, or missing required execution evidence indicates a testing gap.

## Diff quality (harness category: unreviewable)

Where it lives

In an eval bundle, inspect the candidate PR's unified diff, changed-file list, and commit list.

In live mode, inspect the branch diff against the intended base branch and review each changed file and relevant diff hunk.

Look for debug statements, dead code, commented-out blocks, unnecessary generated files, unrelated edits, and formatting changes that obscure the functional fix.

What good looks like

The relevant fix is visible in the diff, and the changed files and hunks can be reviewed without unrelated modifications obscuring the intended behavior. Debug leftovers, unnecessary generated artifacts, dead code, or unrelated changes that materially complicate review indicate an unreviewable diff. A large diff is not automatically a failure if its changes are relevant and reviewable.

## Standards and comms (harness category: standards-wall)

Where it lives

In an eval bundle, inspect the repo-facts block's PR template requests, contributing instructions, stated repository policies, AI-use disclosure requirements, and any explicit maintainer direction in the issue thread. Compare these requirements with the candidate PR's description and disclosures.

In live mode, inspect the repository's PR template, CONTRIBUTING.md, applicable policy documents, and relevant maintainer comments. Compare them with the draft PR title, description, completed template sections, and required AI-use disclosure.

Evaluate whether required information is present and meaningful rather than merely checking whether a heading or placeholder exists.

What good looks like

The PR satisfies applicable mandatory template requests, repository policies, disclosure requirements, and explicit maintainer directions. Required sections contain accurate, relevant information rather than boilerplate, and required AI-use disclosure is present. Missing mandatory disclosures, ignored maintainer instructions, or unfilled required template requests indicate a standards failure. Optional stylistic preferences alone do not constitute a failure.

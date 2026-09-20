# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61

**Verdict output**

```
Same issue as I just graded in this session. Re-checking the one signal that could have moved — whether anyone has claimed it — then re-emitting the result.

  Ran 1 shell command

Nothing has changed: still open, no assignee, 0 comments, 0 PRs in the repo, not archived, last push 2026-09-16. The grading stands unchanged.

┌──────────────────┬───────┬────────────────────────────────────────────────────────────────────────────────────────┐
│      Check       │ Grade │                                        Evidence                                        │
├──────────────────┼───────┼────────────────────────────────────────────────────────────────────────────────────────┤
│ maintainer_alive │ pass  │ All 5 latest main commits authored by a human, Aburke225, newest 2026-09-16; issue     │
│                  │       │ opener's author_association is COLLABORATOR.                                           │
├──────────────────┼───────┼────────────────────────────────────────────────────────────────────────────────────────┤
│ repo_active      │ pass  │ archived: false, pushed_at: 2026-09-16T21:50:20Z — 4 days ago, inside the 180-day      │
│                  │       │ threshold.                                                                             │
├──────────────────┼───────┼────────────────────────────────────────────────────────────────────────────────────────┤
│ newcomer_scope   │ pass  │ One bounded defect, confirmed live at api/routes/health.py:32 (await                   │
│                  │       │ db.execute("SELECT 1")); labeled bug, good first issue, tier-1.                        │
├──────────────────┼───────┼────────────────────────────────────────────────────────────────────────────────────────┤
│ unclaimed        │ pass  │ No assignees, 0 comments, no linked PRs — the repo has zero PRs of any state.          │
├──────────────────┼───────┼────────────────────────────────────────────────────────────────────────────────────────┤
│ ai_policy        │ pass  │ docs/CONTRIBUTING.md is the only contribution policy and never mentions AI-assisted    │
│                  │       │ work. Silence passes.                                                                  │
└──────────────────┴───────┴────────────────────────────────────────────────────────────────────────────────────────┘

Verdict: accept — every required check passes. Fix is from sqlalchemy import text plus await db.execute(text("SELECT 1")); remember to delete the @pytest.mark.xfail marker naming issue #61, and leave the settings.redis_host bug in the same file alone (that's issue #62).

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
  "checks": [
    {"name": "maintainer_alive", "grade": "pass",
     "evidence": "All 5 latest main commits authored by human Aburke225, newest 2026-09-16; issue opener author_association is COLLABORATOR."},
    {"name": "repo_active", "grade": "pass",
     "evidence": "archived: false and pushed_at 2026-09-16T21:50:20Z, 4 days before today 2026-09-20."},
    {"name": "newcomer_scope", "grade": "pass",
     "evidence": "Single bounded defect at api/routes/health.py:32 with repro steps, labeled bug / good first issue / tier-1."},
    {"name": "unclaimed", "grade": "pass",
     "evidence": "No assignees, 0 comments, no linked PRs; the repo contains zero PRs in any state."},
    {"name": "ai_policy", "grade": "pass",
     "evidence": "docs/CONTRIBUTING.md is the only contribution policy and never mentions AI-assisted contributions; no AI_POLICY.md exists."}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

3/3, 17/20, 16/20, 18/20

**Issue analysis**

issue-19  accept  reject   NO     failed: newcomer_scope

My rubric rejected issue-19 because the newcomer_scope check failed, but the gold label accepted it. 
This means my scope check was stricter than the expected result.

**Check rationale**

`| repo_active | Repo facts: archived status, last push to any branch, and latest release. | Pass if the repository is not archived and the last push to any branch is within 180 days of the repo-facts capture date. | required |`

I used this check because repository activity is important when deciding whether an issue is suitable as a first contribution. The 180-day threshold gives the check a specific and repeatable condition instead of relying on a subjective description such as "active."

**Trade-offs**

This check can miss a healthy repository that has intentionally had no push within 180 days.
 I accepted that trade-off because a first contribution should generally be made to a repository with recent activity, and the separate `maintainer_alive` check provides another signal of ongoing human maintenance.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**


1. The issue's fit to my interests and to the time available.

I selected issue #61 because it is a focused backend issue involving an API health check and database access. 
My background is in backend development, Java, Spring Boot, REST APIs, and SQL, so the general type of problem is familiar to me even though this project uses Python and SQLAlchemy. 
The issue appears small and well-bounded enough to work on within the time available.

2. What the verdict identified correctly, and what you weighed that the rubric could
   not.

The verdict correctly identified that the repository is active, the issue has a bounded scope, the issue is unclaimed, and there is no explicit AI contribution prohibition. 
I also considered my own backend experience, familiarity with database-related problems, the specific reproduction steps, and the time I would need to learn the project's Python and SQLAlchemy setup. 
Those personal-fit considerations were not part of the rubric.

3. The anticipated difficulty in claiming it.

The main difficulty I expect is becoming familiar with the project's Python and SQLAlchemy environment and understanding the existing health-check test setup. 
The issue provides a specific reproduction and location and appears unclaimed, so I expect the main work to be understanding the project and reproducing the problem before making the fix.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

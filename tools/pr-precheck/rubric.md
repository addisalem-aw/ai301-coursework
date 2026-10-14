# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| silent_drift | Compare the actual diff and changed files against the original plan's stated scope, intended behavior, and documented deviation notes. Compare the PR description's claims about implementation and plan fidelity against the actual diff. | Pass if the diff stays within the planned scope or its documented, justified deviations, and the description does not misrepresent what was implemented. A material unexplained omission, scope expansion, or contradiction between the description and diff fails. An honestly disclosed shortfall passes when the description accurately reports it and the remaining change is consistent with the documented scope and limitations. |required  |
| not_tested | Compare the candidate PR's test-evidence section and captured check results with the plan-context block's test plan, expected behavior, and repository checks identified by the evidence guide. | Pass if the evidence demonstrates an observable result relevant to the intended fix and required repository checks have visible outcomes. Fail if tests do not exercise the relevant behavior, required execution evidence is missing, or failures leave the fix unverified. An honestly disclosed limitation may pass only when the required verification standard is still satisfied. | required |
|unreviewable|Inspect the implementation diff, including changed files and individual hunks, using the diff-quality guidance in references/evidence-guide.md.|Pass if the relevant change can be reviewed without unrelated modifications or generated debris obscuring the fix. Unrelated changes, unnecessary generated artifacts, or irrelevant hunks that materially obscure or complicate review fail.|required|
|standards_wall|Inspect the repository facts and template requirements identified by references/evidence-guide.md, along with the PR description, required disclosure statements, and other applicable submission conventions.|Pass if the PR meets applicable repository template and disclosure requirements and communicates the change and its limitations accurately. Missing required disclosures, ignored mandatory template requests, or materially misleading communication fail. Optional stylistic preferences do not fail the check.|required|

## Verdict rule

Accept the PR package only when every required check passes. Reject if any required check fails or is unclear because the evidence cannot verify the required outcome. Preferred checks, if added, never change the verdict. An honestly disclosed shortfall does not automatically require rejection: accept when the remaining implementation, verification evidence, scope, and required disclosures satisfy all applicable pass conditions. Do not treat missing evidence as proof of success.

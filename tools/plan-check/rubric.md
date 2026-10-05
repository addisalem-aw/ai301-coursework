# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|diagnosis|The plan's stated diagnosis read against the reproduced issue evidence, including the quoted repro evidence and the relevant issue/thread evidence.|Pass if the diagnosis explains the observed failure and does not contradict the reproduced evidence; the stated cause should account for the behavior rather than merely restating the symptom.|required|
|scope|The plan's scope statement and list of files/areas to change, read against the issue's requested outcome and the repo-facts/conventions evidence.|Pass if the proposed change is bounded to the reproduced problem, identifies what will and will not change, and does not introduce unrelated work or scope creep.|required|
|approach|The plan's proposed implementation approach and files to touch, read against the diagnosis and repo-facts evidence.|Pass if a stranger could use the plan to begin the implementation without having to guess the intended change, and the approach addresses the diagnosed cause rather than only masking the symptom.|required|
|test-plan|The plan's test plan read against the repro evidence's steps, expected behavior, and any relevant repo testing conventions.|Pass if the planned checks exercise the reproduced failure through the real code and specify an observable result that would demonstrate the fix works without breaking the relevant behavior.|required|
| files |The plan's list of files to touch and files explicitly excluded, read against the diagnosis, scope, and repo-facts evidence.| Pass if the files identified are appropriate for the proposed fix and are sufficient to implement and verify it, while unrelated files are kept out of scope. |required|
|risks | The plan's risks and unknowns read against the available repro evidence and repo-facts evidence.|Pass if material uncertainties and possible side effects are identified as risks or unknowns rather than presented as established facts, and the plan explains what should be checked if they matter to implementation or testing.|required| 
| comment | The draft comment compared with the plan, issue thread, posted reproduction evidence, and repository communication conventions. | Pass if the comment accurately represents the plan and available evidence, uses the same confirmed diagnosis and exception name, does not make unsupported promises, and follows repository communication requirements. | required |

## Verdict rule

Accept if every required check passes. If any required check fails or is unclear, reject. Unclear is treated as a fail because the evidence is insufficient to establish that the plan is ready to post and build from.

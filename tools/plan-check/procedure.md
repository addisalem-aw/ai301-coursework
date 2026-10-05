# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue first. Record the reported problem, requested outcome, relevant constraints, and important comments from the issue thread.
2. Read the reproduced issue evidence next. Record the observed behavior, reproduction steps, expected behavior, and any evidence showing the likely cause.
3. Read the repository facts and conventions identified by the evidence guide. Record relevant files, testing conventions, and repository rules that affect the proposed change.
4. Read the plan's diagnosis and compare it with the reproduced evidence before reading the proposed solution. Record whether the diagnosis explains the observed failure.
5. Read the plan's scope and files-to-touch information. Record what will change, what will not change, and which files are proposed for modification.
6. Read the plan's approach and compare it with the diagnosis, scope, files, and repository facts.
7. Read the plan's test plan and compare it with the original reproduction steps and expected behavior.
8. Read the plan's risks and unknowns and record claims that are uncertain or could affect implementation or testing.
9. Read the draft comment last and compare it with the issue thread and the actual plan so the comment is not treated as independent evidence.
10. Use the evidence guide to locate each required piece of evidence. Do not assume that a missing statement in the plan is supported by information elsewhere unless the rubric or evidence guide says to use that source.

## Evidence gathering

1. For diagnosis, collect the plan's stated cause and the reproduced issue evidence showing the observed behavior. Record whether the proposed cause is supported by, consistent with, or contradicted by the evidence.
2. For scope, collect the plan's explicit change boundary, including what will be changed and what will remain unchanged. Compare it with the issue's requested outcome and repository constraints.
3. For files, collect the plan's files-to-touch list and compare each proposed file with the diagnosis, scope, and repository facts. Record any required file that is missing and any unrelated file included.
4. For approach, collect the implementation steps or strategy from the plan. Compare them with the diagnosed cause and the files identified for the fix. Record whether another developer could begin the implementation without guessing.
5. For test-plan, collect the original reproduction steps and expected behavior, then collect the plan's proposed test steps and expected results. Record whether the proposed test exercises the real code and produces an observable result that can distinguish a fixed behavior from the original failure.
6. For risks, collect the plan's stated risks and unknowns. Compare them with the evidence and identify assumptions that are presented as facts or material uncertainties that were not acknowledged.
7. For comment, collect the draft comment and compare it with the issue thread, repository conventions, and the actual plan. Record any material mismatch, unsupported claim, or omitted thread requirement.
8. If evidence is genuinely absent, record the missing evidence rather than filling the gap with an assumption.

## Check execution

1. Grade the checks in this order: diagnosis, scope, files, approach, test-plan, risks, and comment.
2. For each check, use only the evidence gathered for that check and the evidence sources explicitly allowed by the rubric.
3. Assign pass when the evidence satisfies the check's pass condition.
4. Assign fail when the evidence contradicts the pass condition or shows that the plan does not meet it.
5. Assign unclear when the available evidence is insufficient to determine whether the pass condition is satisfied.
6. Do not treat the existence, length, formatting, or number of sections as evidence that a check passes. Grade the substance of the proposed plan.
7. Do not re-grade an earlier check unless later evidence directly changes the evidence relevant to that check.
8. For diagnosis, do not accept a symptom description as the cause unless the reproduced evidence supports that explanation.
9. For scope, reject proposed work that expands beyond the issue without evidence that the additional work is necessary.
10. For files, reject files that are unrelated to the planned fix or a necessary verification change.
11. For approach, reject an approach when a developer would have to guess what implementation change is intended.
12. For test-plan, reject tests that cannot demonstrate the reported failure is fixed or that do not exercise the relevant real behavior.
13. For risks, reject unsupported certainty when the evidence leaves an important question unresolved.
14. For comment, reject material differences between what the comment claims and what the plan or issue evidence supports.
15. When evidence is missing, use unclear rather than guessing.

## Verdict assembly
1. Collect the final grade for every required check.
2. Apply the rubric's verdict rule after all checks have been graded.
3. Return accept only when every required check is pass.
4. Return reject if any required check is fail.
5. Return reject if any required check is unclear.
6. Preferred checks, if present, must not change the verdict.
7. For each failed or unclear check, include the specific missing, contradictory, or insufficient evidence that caused the result.
8. For the deciding check or checks, quote or identify the relevant evidence location so another grader can verify the decision.
9. Do not change a check's grade merely to reach a target number of accepted packages.
10.Produce one binary final verdict: accept for ready to post and build from, or reject for hold and revise.


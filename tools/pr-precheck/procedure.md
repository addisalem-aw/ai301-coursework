# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the original issue and record the reported problem, requested outcome, relevant constraints, and important issue-thread comments.
2. Read the original plan before examining the implementation. Record the diagnosis, intended solution, files to change, scope boundaries, and test plan. Use the plan as the baseline for evaluating the PR.
3. Read the implementation diff file by file. Record the changed files, actual code changes, behavior affected, and any changes outside the planned scope.
4. Read the test changes and available test execution evidence. Record which tests were added or modified, which planned tests were executed, their results, and any missing or failing evidence.
5. Read the repository check results required by the rubric. Record the outcomes of relevant tests, builds, lint checks, or other required checks, distinguishing confirmed failures from checks that were not run.
6. Read the PR description last. Record its summary, claimed fixes, testing claims, and any explanation of deviations from the plan.
7. Compare the plan, diff, test evidence, repository checks, and PR description before grading. Do not treat a statement in the PR description as proof unless the corresponding implementation or test evidence supports it.
8. Use the evidence guide to locate every required source. If evidence is missing, record the gap rather than assuming the requirement was satisfied.

## Evidence gathering

1. For diagnosis and implementation, collect the plan's diagnosis and intended behavior, then compare them with the actual diff. Record whether the code addresses the diagnosed problem and implements the intended fix.
2. For scope, collect the plan's files-to-touch list, explicit exclusions, and intended behavior. Compare them with every changed file and material change in the diff. Record missing planned changes, unrelated modifications, and unexplained scope expansion.
3. For implementation approach, collect the plan's proposed steps and compare them with the actual code. Record whether the implementation follows the intended approach and whether any deviations are explained and justified by the available evidence.
4. For test coverage, collect the plan's test plan and expected results. Compare each planned test with the tests actually added or modified. Record whether the tests exercise the relevant behavior and can distinguish the original failure from the fixed behavior.
5. For test results, collect the available execution output for the relevant tests. Record which tests passed, failed, or were not run. Do not treat the presence of a test file as proof of a passing test.
6. For repository checks, collect the execution evidence for each check required by the rubric. Record the exact outcome and relevant errors. Distinguish a confirmed failure from unavailable execution evidence.
7. For the PR description, compare each material claim about the fix, changed files, behavior, and testing with the diff and execution evidence. Record inaccurate claims, unsupported testing statements, and important omissions.
8. For deviations, compare the final implementation with the original plan. Record each material difference, its explanation, and whether the evidence supports the decision to deviate.
9. For every rubric check, retain a concise evidence note identifying the relevant plan requirement, changed file, test result, or PR description statement.
10. If evidence is genuinely absent or contradictory, record precisely what is missing or conflicting. Do not resolve the gap through assumptions.

## Check execution
1. Grade the checks in the order specified by `rubric.md`: `silent_drift`, `not_tested`, `unreviewable`, and `standards_wall`.
2. For `silent_drift`, compare the plan's stated scope, intended behavior, and deviation notes with the actual diff. Compare the PR description's claims with the implementation. Fail if material changes or omissions are unexplained, or if the description contradicts the diff. Allow an honestly disclosed shortfall when the remaining change satisfies the rubric's pass condition.
3. For `not_tested`, compare the plan's test plan and expected behavior with the available test evidence and required repository check results. Fail if the relevant behavior is not meaningfully tested, required execution evidence is missing, or the intended fix remains unverified. Do not infer a pass from a test file's existence or a claim that tests passed.
4. For `unreviewable`, inspect the diff and commit list for unrelated modifications, debug leftovers, dead code, commented-out blocks, unnecessary generated artifacts, and formatting churn. Fail when these materially obscure or complicate review of the intended fix.
5. For `standards_wall`, compare the repository's PR template, contributing instructions, applicable policies, required disclosures, and explicit maintainer directions with the PR's actual content. Fail when a mandatory requirement is missing or ignored.
6. Apply each rubric pass condition exactly as written. Assign `pass` when the condition is satisfied, `fail` when the evidence contradicts it, and `unclear` when the permitted evidence cannot establish the outcome and the rubric allows that grade.
7. Record each check's grade and one concise evidence line identifying the fact, quote, or artifact location that determined the grade. Do not invent evidence or add checks that are not in `rubric.md`.

## Verdict assembly

1. Collect the final grade for every required check.
2. Apply the verdict rule specified in the Unit 4 rubric. Do not invent a threshold or substitute an informal overall judgment.
3. Apply the rubric's explicit rules for failed, unclear, and missing-evidence grades. Do not silently treat unclear evidence as a pass.
4. Return accept only when the package satisfies the rubric's acceptance conditions. Otherwise, return reject.
5. If multiple required checks fail, select the first failing required check in rubric order as the deciding check, unless the rubric specifies another selection rule.
6. For the deciding check, quote the smallest relevant piece of evidence or identify its precise source location. Explain briefly how it violates the check's pass condition.
7. If the verdict depends on missing or contradictory evidence, identify the specific gap or conflict rather than presenting an unsupported claim as fact.
8. Include the per-check grades, evidence, final verdict, and deciding-check explanation in the exact structure and field names required by SKILL.md.
9. Before returning the result, verify that the verdict follows from the recorded grades, the deciding check follows the selection rule, and all quoted evidence is supported by the PR package.

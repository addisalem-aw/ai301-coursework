---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Answer exactly one question about exactly one PR package: is this ready to submit? Treat a PR package as a candidate pull request containing its title, description, commits, diff, and test evidence. Evaluate those artifacts against the plan.md it claims to implement, including its ## Deviations notes, and the issue the plan belongs to. Do not grade unrelated work, multiple packages, general code quality outside the PR's scope, or the student's overall performance.

## Inputs and modes

Determine the mode from the invocation and the available inputs. In live mode, grade the student's own draft PR. In eval mode, grade exactly one practice package bundle. Do not combine the two modes or mix their sources.
Live mode: Read these inputs

plan.md, including ## Deviations, from the working copy or the house-chain plan supplied for the assignment.
The complete committed branch diff relative to main, obtained from the working copy by running git diff main...HEAD.
The draft PR title and description from pr_draft.md in the working copy or the equivalent house-chain submission artifact.
test_evidence.md from the working copy or the equivalent house-chain evidence artifact.
The issue URL supplied in the invocation. Read its issue description and discussion thread from the scoped Path Review repository.
The repository's .github/PULL_REQUEST_TEMPLATE.md and docs/CONTRIBUTING.md.
For a house-chain assignment, use the provided house issue, repro pack, plan, working branch, and corresponding submission artifacts instead of assuming the student has their own issue and working change. Apply the same rubric checks to the available house-chain artifacts.
Use the actual committed diff, not an assumed summary of the changes. Compare the plan and its deviations with the diff, the planned tests with the test evidence, and the PR description with both the diff and the repository's stated requirements. Do not treat a claim in the description as proof that the underlying action occurred.

Eval mode: Read the selected package from the evaluation harness's package bundle. Treat that bundle as the entire available world. Derive every fact from the bundle text only. Do not fetch the issue, browse the repository, read the working copy, or use any outside files or information. Run every rubric check and apply the complete verdict rule to each package. Do not skip checks merely because evidence is missing; grade missing or unverifiable evidence according to the rubric.

## The scope seam (live mode only)

In live mode, read scope.md before reading or evaluating any other PR artifacts. Identify the permitted repository from its Repo: line and follow the scope rules it defines. If the repository line contains an unfilled placeholder, refuse to grade, explain that the student must replace it with codepath/pathreview-ai301-fa26-s3 or the correct Path Review repository for their section, and stop without producing a graded verdict. If the supplied PR or issue is outside the scoped repository, refuse to grade it and explain the scope mismatch. Never guess the repository or silently switch scopes.
After confirming the scope, gather the live-mode inputs specified above. In eval mode, ignore scope.md entirely and do not use it to accept, reject, or refuse a package.

## The voice seam (live mode only)

In live mode, read voice-guide.md and apply its writing rules to the draft PR title and description. Report any broken voice-guide rule in the readable per-check summary, with the specific rule and the affected text. Treat the voice guide as a communication aid, not an independent acceptance criterion: a voice violation changes the verdict only if a rubric check explicitly makes that violation relevant. Do not add voice checks to the JSON output unless they are defined in rubric.md. In eval mode, ignore voice-guide.md entirely.

## Component reads

Read rubric.md to obtain the complete list of checks, their evidence requirements, pass conditions, weights, and verdict rule. Read references/evidence-guide.md to identify where each evidence family is located in a package and what sufficient evidence looks like. Execute procedure.md in its written order, including its Read order, Evidence gathering, Check execution, and Verdict assembly sections.
Use the rubric as the sole authority for which checks exist and what constitutes a pass or fail. Use the procedure as the authority for how evidence is gathered and checks are executed. Use the evidence guide to locate and interpret evidence; it does not override the rubric or procedure.
If rubric.md contains no actual rubric content, refuse to grade and explain that the rubric must be completed. If procedure.md contains no actual procedure content, refuse to grade and explain that the procedure must be completed. Do not invent checks or a verdict rule to compensate for either missing component.
If the procedure is silent about a step needed to complete an evaluation, report the procedural gap in the readable summary. Do not silently invent an alternative procedure or claim that an unspecified step was completed. Continue only with the steps that the written procedure supports and the evidence that is available; apply the rubric's treatment of missing or unverifiable evidence when assembling the verdict.

## Verdict and output

Return exactly one binary verdict for the package: accept means the PR is ready to submit; reject means hold it for correction or for evidence that resolves a failing check. Grade every check defined by the rubric and assemble the verdict using its written rule. Do not invent a score, a third verdict, or an informal exception to the rule.
End the response with the fenced JSON block below, using the exact schema and key order shown. Populate item with the PR URL or package bundle ID. Include every rubric check in checks, preserving its name and reporting its pass, fail, or unclear grade. Give each check one concise evidence line stating the fact or quote that decided its grade. Set verdict to accept or reject according to the rubric. The JSON must be valid, the fenced block must be the final content in the response, and nothing may follow it.

{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}

## Grading discipline

Evidence first. Do not grade a check without identifying the specific fact, artifact, or quote that supports the decision. Never use statements such as "looks fine" as evidence. When evidence is missing or cannot be verified, say so explicitly and grade it according to the rubric.
Grade the artifact, not the polish. Evaluate the PR's actual title, description, diff, plan, deviations, and test evidence against the issue and repository standards. Do not reward confident wording or attractive formatting when the underlying artifacts contradict the claims.
The rubric decides. Apply each pass condition exactly as written. If a check satisfies its pass condition, pass it even if another concern feels important. If a requirement should affect the verdict but the rubric does not cover it, report the gap rather than inventing a new check.
The procedure decides how. Follow the documented evidence-gathering and check-execution steps. If a step is missing, report the gap rather than silently improvising or claiming unsupported verification.
Unclear defaults to fail. Follow the rubric's explicit verdict rule for unclear grades. If that rule does not specify how to handle unclear, treat it as a failing result for verdict assembly. Do not accept a PR based on claims that cannot be verified from the permitted evidence.

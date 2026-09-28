# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Where it lives: In the eval bundle, check the repro report's environment record and compare it with the issue context for the versions, operating system, runtime, dependencies, repository/commit, and any issue-specific setup that matters. In live mode, check the student's repro report and the repository's relevant setup/documentation.
What good looks like: The recorded environment identifies the conditions needed to understand or repeat the attempt. Versions or configuration that the issue specifically targets are named and match the target, or any difference is explicitly called out.
Steps
Where it lives: In the eval bundle, check the repro report's reproduction steps, including commands, inputs, configuration, setup actions, and any required starting state. In live mode, check the student's repro report for the same information.
What good looks like: A competent reader can start from the stated starting state and follow the listed actions and commands to reach the reported result without inventing a missing action, input, or configuration that could change the outcome.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Where it lives: In the eval bundle, check the artifacts read against the issue description, such as command output, error messages, logs, test results, screenshots, traces, or other captured observations. Also check the repo-facts block when repository state or behavior is relevant. In live mode, check the artifacts attached or linked from the repro report.
What good looks like: The artifact demonstrates the behavior described by the issue, including the relevant error, output, or observable result. A similar error or unrelated failure does not count unless the evidence connects it to the issue's reported behavior.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Where it lives: Check the claim comment against the issue thread and the repository's contribution conventions. Check the repro report and final repro comment against the repository's stated templates, contribution policy, attribution requirements, and applicable AI-use disclosure requirements. In live mode, also check the student's draft claim comment before reproduction.
What good looks like: The claim describes the intended reproduction work without presenting an after-the-fact result, and the final communication accurately reports what was actually observed. The wording follows applicable repository conventions and disclosures, while giving specific evidence instead of relying on boilerplate or unsupported assertions.
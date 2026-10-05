# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
Where it lives:

In an eval package, read the issue context and the repro-evidence block for the reported problem, reproduction steps, observed behavior, and expected behavior.
Read the candidate plan's diagnosis or stated cause and any quoted reproduction evidence.
In live mode, read the GitHub issue thread, the student's posted reproduction/repro comment, and the draft plan.
Use the repo-facts block or repository documentation when the diagnosis depends on repository behavior or conventions.

What good looks like:

The stated cause explains the behavior demonstrated by the reproduction evidence and does not contradict it.
The plan distinguishes the underlying cause from the visible symptom and does not claim certainty that the available evidence does not establish.



## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives:

Read the candidate plan's scope statement, including what is in scope and explicitly out of scope.
Read the plan's files-to-touch list and proposed areas of change.
Compare those statements with the issue context and the repo-facts block.
In live mode, also compare the scope with the issue thread and repository contribution expectations.

What good looks like:

The proposed work is limited to the issue being addressed and identifies a clear boundary around the change.
Files and areas included in the plan are necessary for the fix or its verification, while unrelated cleanup or feature work remains out of scope.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives:

Read the candidate plan's files-to-touch list, implementation approach, and ordered work steps.
Use the diagnosis and repo-facts block to determine whether the proposed files and approach match the repository's actual structure and conventions.
In live mode, inspect the repository files or documentation referenced by the plan when needed to verify that the proposed implementation can be carried out.

What good looks like:

A developer who did not write the plan can identify what files or areas to change, what behavior to modify, and the intended implementation approach without needing to ask the author to fill in a missing decision.
The proposed approach addresses the diagnosed cause and gives enough concrete direction to begin implementation.


## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives:

Read the repro-evidence block for the original reproduction steps, inputs, observed failure, and expected behavior.
Read the candidate plan's test plan for the planned commands, inputs, checks, and expected results.
Use the repo-facts block for repository-specific testing commands or conventions.
In live mode, compare the plan with the student's original reproduction and the repository's available test mechanisms.

What good looks like:

The test plan reruns or faithfully converts the original reproduction into a check against the real code.
It identifies an observable result that distinguishes the fixed behavior from the original failure and includes enough information to determine whether the fix succeeded.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->
Where it lives:

Read the candidate plan's risks and unknowns.
Read the plan's ## Deviations section when present.
Compare uncertain claims with the issue context, repro evidence, and repo-facts block.
In live mode, inspect any posted updates or issue comments that describe changes from the original plan.

What good looks like:

Material uncertainties are explicitly identified instead of being presented as established facts.
If implementation differs from the plan, the deviation is recorded with the reason for the change rather than silently rewriting the history of the plan.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives:

Read the candidate plan's draft comment.
Compare it with the issue context and thread highlights, including maintainer requests or constraints.
Read the repo-facts block for contribution guidance, comment templates, repository conventions, and AI-use disclosure requirements.
In live mode, compare the draft or posted comment with the actual GitHub issue thread and repository contribution policy.

What good looks like:

The comment accurately describes the proposed diagnosis, scope, and approach without making claims unsupported by the plan or evidence.
It responds to relevant thread guidance and follows repository communication and AI-use disclosure requirements rather than using unrelated boilerplate.

# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|Environment recorded|The repro report's environment record, including repository/version or commit, runtime and tool versions, operating system, and any issue-specific setup. Compare these details with the issue context.|The environment contains enough information to understand the conditions under which the reproduction was attempted. Versions or setup specifically targeted by the issue match, or any differences are explicitly identified.|required|
|Steps followable |The reproduction steps in the repro report, including commands, inputs, configuration, setup actions, and starting state.  | A competent reader can follow the steps from the stated starting state to the reported result without inventing a missing action, input, or configuration that could change the outcome.  | required |
|Target behavior matches |Output excerpts, logs, screenshots, test results, traces, or other artifacts read against the issue description and expected behavior. Use the repo-facts block when repository state is relevant.  | The evidence shows the same behavior described by the issue, rather than an adjacent, similar, or unrelated failure. | required |
| Outcome is evidenced |The outcome statement in the repro report together with the artifacts and observations supporting it.  | The stated outcome is consistent with the evidence. A successful reproduction shows the issue's reported behavior. An evidenced cannot-reproduce result passes when the documented attempt and evidence support that conclusion. An unsupported or contradicted outcome fails. | required |
|Evidence is sufficient|The artifacts read against the issue description, including command output, logs, test results, screenshots, traces, and relevant repo facts.|The evidence is sufficient to distinguish the claimed outcome from a guess, unrelated failure, or environment/setup problem.| required|
| Repository conventions respected | The claim comment and repro report, together with the repository conventions identified in `references/evidence-guide.md`. Check specifically for required attribution, reporting requirements, and AI-use disclosure requirements when the repository requires disclosure. | All applicable repository requirements are satisfied. If the repository requires AI-use disclosure, the package includes the required disclosure; if it requires attribution or a specific reporting practice, that requirement is also satisfied. Missing a required disclosure, attribution, or reporting requirement fails this check. | required |
| AI-use disclosure | The claim comment and repro report, compared with the repository's contribution policy and the disclosure requirements located through `references/evidence-guide.md`. | When the repository requires AI-use disclosure, the package contains the required disclosure. A missing required AI-use disclosure fails this check. If the repository does not require disclosure, this check passes. | required |
## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every required check passes.
Preferred checks never change the verdict.
If a required check is unclear, treat it as a failure and reject the package.
Reject if any required check fails or is unclear.

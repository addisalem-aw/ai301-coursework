# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer_alive | Repo facts: last 5 default-branch commits and maintainer first-response sample; issue Comments for `author_association`. | Pass if there is evidence of recent human maintainer activity: at least one human-authored commit in the last 5 default-branch commits, or at least one maintainer response in the first-response sample, or a maintainer comment in the issue thread. Bot-only activity does not count. | required |
| repo_active | Repo facts: archived status, last push to any branch, and latest release. | Pass if the repository is not archived and the last push to any branch is within 180 days of the repo-facts capture date. | required |
| newcomer_scope | Issue body and Comments; scope guidance in `references/evidence-guide.md`. | Pass if the issue describes a clearly bounded contribution with a defined outcome or documentation home. Multiple related file/page updates may still pass when they support the same defined contribution. Fail if the issue is an umbrella/tracking issue, an unresolved design debate, a pure usage/support question, or explicitly requires changes to core internals. Short or imperfect issue descriptions do not fail by themselves. | required |
| unclaimed | Repo facts: this issue's assignees and linked PRs; issue Comments for active claim statements such as "I'll take this", "can I work on this", or "working on this". | Pass if there is no assignee, no open linked PR, and no active claim in the comments. | required |
| ai_policy | Repo facts: contribution policy, dedicated AI policy files, and templates. | Pass unless the repository explicitly prohibits AI-assisted or AI-generated contributions. Disclosure, testing, personal-understanding, or human-review requirements are allowed. Silence about AI passes. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required check passes. Preferred checks never change the verdict; they only rank accepted issues. Treat `unclear` as a fail.

# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

I am an experienced software developer contributing a specific reproduction of an issue. I am here to document what I tested and what I observed, not to speak for the maintainers or claim more than my evidence shows. Readers should be able to distinguish my planned reproduction from my completed findings.


## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->
Rule: State the work, not the conclusion

I describe what I am going to test in a claim and reserve the result for the reproduction report.

Wrong: "I reproduced this issue and will share the details soon."
Right: "I will reproduce the reported behavior in the stated environment and post the observed result."
Rule: Tie claims to evidence

I connect important conclusions to something I actually observed rather than making a broad assertion.

Wrong: "This definitely confirms the issue."
Right: "The command produced the same error described in the issue, which is the behavior I was testing."
Rule: Be specific about the result

I name the actual outcome, including when the issue could not be reproduced, instead of using vague success language.

Wrong: "Everything worked as expected."
Right: "I could not reproduce the reported error with the documented environment and steps."
Rule: Separate my test from someone else's

I describe my own reproduction work and evidence instead of relying on another contributor's reproduction.

Wrong: "Same reproduction as the previous comment."
Right: "I ran the reproduction independently using the following environment and steps, and observed the result below."
Rule: Keep the wording proportional to the evidence

I do not claim more than my artifacts establish. When evidence is incomplete or shows a different behavior, I describe that limitation instead of forcing a reproduction claim.

Wrong: "The issue is fixed because I did not see the error."
Right: "I did not observe the reported error during this attempt; the available evidence does not establish whether the underlying issue is fixed."


## Things I never post

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->

I never claim I reproduced an issue before I actually tested it.
I never say "same as above" instead of documenting my own reproduction.
I never describe an unrelated or adjacent error as the reported issue.
I never call something confirmed when the evidence does not support that conclusion.
I never hide a cannot-reproduce result just because a reproduction would be preferable.
I never invent commands, test results, environment details, or observations.
I never omit required attribution or AI-use disclosure when the repository requires it.

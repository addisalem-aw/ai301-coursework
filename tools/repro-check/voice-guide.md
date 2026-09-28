# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am an experienced software developer contributing a specific reproduction of an issue. I am here to document what I tested and what I observed, not to speak for the maintainers or claim more than my evidence shows. Readers should be able to distinguish my planned reproduction from my completed findings.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

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

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

I never claim I reproduced an issue before I actually tested it.
I never say "same as above" instead of documenting my own reproduction.
I never describe an unrelated or adjacent error as the reported issue.
I never call something confirmed when the evidence does not support that conclusion.
I never hide a cannot-reproduce result just because a reproduction would be preferable.
I never invent commands, test results, environment details, or observations.
I never omit required attribution or AI-use disclosure when the repository requires it.
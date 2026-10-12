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

Josh Borthick
Experience:
8 years - coding
4 years - data structures
3 years - AI engineering
3 years - kernel engineering
3 years - algorithms
3 years - prompt engineering
1 year - data science and engineering

I seek to take issues and provide reproducibility statements and logs,
including line(s) that break, local and tool environment statements, 
and fixes.

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

### Rule: Environment
Logs must specify exact environments.
- Wrong: "Yeah, I've reproduced it and it's definitely broke."
- Right: "I've reproduced the bug on version x.xx.xxxxx on Ubuntu 26.04.1 (Linux 7.0.1-1-generic)."

### Rule: Reports
Full explanations of what line the bug appears at.
- Wrong: "It's line 434."
- Right: "Line 434 appears to be the start of the bug.  It seems to go through line 441."

### Rule: Tone
No fanboy tone and no begging.
- Wrong: "Oh, this looks great!  I'll definitely take this! Please assign, I'll fix right away!"
- Right: "I've reproduced the bug on version x.xx.xxxx on Ubuntu xx.xx.x (Linux x.x.x-x)."

### Rule: AI-Comments
No AI-written comments.
- Wrong: "The Problem: * Line 434 --- the bug begins here..."
- Right: "The bug seems to begin on line 434."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Completion date promises.
- AI-worded comments.
- Asking to be assigned the issue.
- Sarcasm or exasperation.
- Claims I cannot back up with logs.

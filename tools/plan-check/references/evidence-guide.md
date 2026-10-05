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
Eval Bundle: The plan's diagnosis section and repro-evidence block.
Live Mode: The posted repro comment and if the issue a bug to fix, 
then the diagnosis section.

What good looks like:
The cause is due to a null pointer exception found when calling the
after.next pointer when after is null.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives:
Eval Bundle: The issue text describes the issue scope and the plan
section matches this.
Live Mode: The issue text describes the issue scope and the plan
section matches this.

What good looks like:
(For a feature) The issue text mentions wanting a small LLM to re-
rank retrieved documents before sending them to the text generator.
The claim plan deals with this new feature and does not suggest
introducing anything else.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives:
Eval Bundle: The files and approach sections.
Live Mode: The files and approach sections.

What good looks like:
Files: main.py
Approach: Run `main.py` with the `-f` flag and give it the CSV file to
open and work with.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives:
Eval Bundle: The test section of the plan.
Live Mode: The test section of the plan.

What good looks like:
1. Open a terminal.
2. Change to the directory with the repo.
3. Run `main.py` with `-f <filename>.csv`.
4. Observe the output.  It should correctly compute the cosine 
similarities between the term names.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

Where it lives:
Eval Bundle: Any plan section describing dangers or deviations from
the issue.
Live Mode: Any plan section describing dangers or deviations from
the issue.

What good looks like:
The fix is in place and tests as working on my machine, but I will 
admit not knowing why it outputs in reverse on my hardware.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives:
Eval Bundle: Any plan section involving AI use disclosure, risks or
unknowns involved in execution or adoption of this fix or feature,
and any deviations taken from the issue scope and why.
Live Mode: Any plan section involving AI use disclosure, risks or
unknowns involved in execution or adoption of this fix or feature,
and any deviations taken from the issue scope and why.

What good looks like:
AI Use Statement
I used Claude Code to navigate the file structure and figure out how
everything is connected, as well as to evaluate a manually-written
rubric and skill package on the issue and my contribution.


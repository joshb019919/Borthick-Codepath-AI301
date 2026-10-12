# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

**Where it lives:**
**Eval Bundle:** The plan's prodecure section.
**Live Mode:** The plan's scope is in the `rag/retriever` section of
the pathreview repo.  Deviation from scope is in the `Deviations` 
section of `plan.md` in the `pathreview` repo.  The diff matches the 
plan if it changes only what the plan says it will change.  The plan
must also match the diff.  All diff notes are in the `plan` file.

**What good looks like (live mode):**
**Repo Issue:** Create an LLM reranker for RAG chunks given to a
text generator.
**Student PR:** The issue text in `README.md:Features` section tells
of the need and the PR in `plan.md` answers it exactly.  No more, no
less, except for anything in the `Deviations` section of the plan.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

**Where it lives:**
**Eval Bundle:** Test evidence lives in the `procedure.md` file and
the `rubric.md` file describes the rules.
**Live Mode:** In the pathreview repo, `plan.md` describes the 
observations the student made about the repo and the scope of what
is to change, what files will be touched.  The interface section 
shows the class and method contracts for the changes and how they
interact with the repo that's already there.  Prompt and parsing 
explains the way it should work.  For all of this, the tests section
should test that these work the way they should, as well as any 
other parts of `README.md`'s specifications for the feature.

**What good looks like (for a feature):**
The tests are in `tests/unit/test*.py`.  New tests are created to
test the functionality.  Nothing is wired up in the live repo, so
nothing is wired up in the `rag/` directory, either.  The tests do
this, explicitly, in a way that does not affect `rag/`.

**Before:** The keyword and vector searches rank the chunks and send 
the list of chunk scores and metadata to the text generating LLM.
**After:** The keyword and vector searches rank the chunks and send 
them to the LLM re-ranker, which changes the score value only for 
each chunk in the list of and sends the sorted list to the LLM text 
generator.  The generator and ogirinal rankers need no changes and
the generator takes in the same data in the same signature.  
**Tests**: Demonstrates that the feature works as expected when 
active but lets score lists pass through without change if not.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

**Where it lives:**
**Eval Mode:** The diff section of a package in `eval/packages/`
shows the changes in diff layout. 
**Live Mode:** The only new logic is in the script `rag/retriever/`
`reranker.py`.  New test file is `tests/unit/test_reranker.py`.  
The plan within `plan.md` in the pathreview repo contains the test 
structure and the scope, interface, and actions to take place.

**What good looks like (for a feature):**
The plan matches the changes and describes the test.  There are no
code sections commented out and no other files changed.  Any debug
code has been removed, like print calls.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

**Where it lives:**
**Eval Mode:** In `eval/packages/`, the repo issue section is the 
source of what it asks of the PR and the PR answers this by matching 
the issue.
**Live Mode:** The PR text is in the root directory of `pathreview-`
`ai301-fa26-s3`.  The README is also there, and contains the 
instructions for the development.

**What good looks like:**
The PR text contains the appropriate headers of the issue to solve
(the feature produced), how it is solved, and how it is tested.  It
also contains the AI-use disclosure and steps for the solution.
All sections are filled and match the desired solution in the README.

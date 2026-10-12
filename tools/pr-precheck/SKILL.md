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

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

This tool grades if the student's pull request (PR) is ready for being
committed to a live GitHub repo to satisfy the requests and needs of
an issue.  Grade nothing else.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

One of:

- **Live mode**: the student's own `plan.md` and draft plan comment,
  plus their issue's URL. Gather the issue-side evidence live (via
  `gh`, the GitHub API, or the web; `references/evidence-guide.md`
  says where each signal lives), and take the reproduction evidence
  from the student's posted repro comment on that issue (their week-2
  proof; the plan must follow from it). A student on the house issue
  has no posted repro comment of their own: there, the reproduction
  evidence is the house repro pack as quoted in the drafts, and if the
  drafts quote no repro evidence at all, that absence is what the
  relevant checks grade. Read the drafts the way a
  maintainer on the thread will read the posted comment: the package
  is what the drafts contain and quote, not other files in the
  student's working directory.  The diff is `git diff main...HEAD` 
  from the working copy of `codepath/pathreview-ai301-fa26-s3`.
- **Eval mode**: a package bundle (a markdown file containing the
  issue context, a repo-facts block, a repro-evidence block, the
  candidate plan, and the candidate plan comment). Use ONLY the bundle
  text as evidence. Do not fetch anything; the bundle is the whole
  world. Eval mode always grades a complete package: every check,
  full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read `scope.md` in this skill directory before anything
else. It names where the student's issue must live and the house rules
that apply there; a house rule changes how evidence is read in that
environment. Refuse to grade a package for an issue outside the scoped
source. If the scope's repo line still carries an unfilled placeholder,
stop without grading and tell the student to get their cohort's scope
file from the instructor; never guess a scope. In eval mode, ignore
`scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

Read `voice-guide.md` in this skill folder only in live mode and
ignore it completely in eval mode.  It gates the PR title and
description.  Report broken rules in the JSON block reporting the 
verdict.  The voice guide never changes the verdict, it is a guide to
help the student stick to the way they said they'd deal with others.
Ensure that the plan/PR and all comments and documentation satisfy
this guide by saying so when it doesn't.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

The rubric (`rubric.md`) contains the rules to follow and the 
`procedure.md` file explains how and where to link things.  The file,
`references/evidence-guide.md` maps the rubric to the locations of the
project.  Stop and let the student know if any of these are not filled
in.

## Verdict and output

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

- Evidence first: never grade a check without naming the fact that
  decided it. "Looks fine" is not evidence.
- Grade the plan, not the polish: a terse complete plan can be ready
  and a long confident one can be unbuildable or wrong. Every check
  reads the thing itself against the issue and its repro evidence,
  never the formatting.
- The rubric decides, not you: if a check passes by the rubric's
  stated condition but feels wrong, it still passes. Note the tension
  in the summary if you want; the fix belongs in the rubric, not in
  the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule
  does not say, treat `unclear` as `fail`: a plan you cannot verify
  from the package is a plan that is not ready to build from.

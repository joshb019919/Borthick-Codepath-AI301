# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Josh Borthick

## Featured Tools

I chose these tools because they were required *and* because they were 
useful.  

- `Skills`.
- `Bash`, `Read`, `Write`, `Edit`.
- `AskUserQuestions`.
- `pr-monitor` and `voice-guard`.

`AskUserQuestion` is necessary since there are quite a few 
things I need to handle myself, like overwriting something that's 
already present in a file. Last but not least are the `pr-monitor` and
`voice-guard` tools, which force Claude to use the required skills to 
ensure that my wording is complete and correct enough for maintainers.

**`Skills`**

**What it is, and the judgment hole I wrote:**

The `Skills` tool was indispensable at finding valid repos to
work on (`issue-scout`), and checking the wording of my pull requests
and claim and commit messages (`repro-check`, `plan-check`, and 
`pr-precheck`).  The rubrics and strategies kept me in line with how
I would prefer to interact with people and how I'd prefer they 
interact with me.

**How it evolved, dated:** 

9/22/2026

I created the rubric in `issue-select` with what seemed like good 
ideas such as nothing that doesn't have a versioned release in more
than one year or strict no AI-sounding-or-looking text, but they were
too strict and made it impossible to properly select those toy issues.
I had to relax those rules to get it to work.  Once I realized what 
was more able to work with the curated situations CodePath gave me, 
the following weekly problems were simple enough to copy rules over 
or write in my own words without having trouble being functional.

**Evidence:** 

The following is the rubric I created for `issue-scout/rubric.md` and
the difficulty note that let me know how hard a given repo would be to
work on.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Recent default-branch commits | "last 5 default-branch commits" under Repo facts or the repo's front page: the line above the file list shows the newest commit and its date; click the commit count next to it to see the recent history | last commit within 6 months | preferred |
| Release recency | "latest release" under Repo facts or the Releases box in the right sidebar of the repo front page: the latest release and its date | last release within 1 year | preferred |
| Archived flag | "archived:" on the repo line or an archived repo shows a "This repository has been archived" banner across the top and is read-only: hard dead | no | required |
| Assignee | "this issue: assignees:" under Repo facts or the Assignees box in the issue's right sidebar | 0 people | required |
| Linked PRs | "linked PRs:" with state per PR, plus any PRs mentioned in the Comments section or the Development box in the issue's right sidebar lists formally linked PRs: an open one is an active claim | 0 linked, open PRs | required |
| Claim comments | the Comments section or read the thread for "I'll take this", "can I work on this", "working on this"; note the date and whether a maintainer answered | 0 claims within 6 months | required |
| Contribution policy | the "contribution policy" line under Repo facts or `CONTRIBUTING.md` in the repo root or `.github/`, and any contributor docs it links out to | does not say anything related to "no AI allowed" or "no AI code contributions" | required |
| Dedicated AI policy files |  files like `AI_POLICY.md` or `AI_USAGE_POLICY.md`; an `AGENTS.md` file is the opposite signal, instructions written for AI coding agents or quoted or summarized on the same line | does not say anything related to "no AI allowed" | required |
| Scope Feasible | Issue body: the work it asks for | The issue describes one identifiable piece of work someone could start: a behavior, a gap, or a task you can point at. It fails only when there is no single piece of work in it: a codebase-wide checklist, an "improve X everywhere", or a container issue tracking many sub-tasks. An open design edge, an "etc.", or several files involved never fails this check; that raises the difficulty note instead. | required |
| Locally Runnable | issue text or repo documentation | this tool must be able to be ran locally without extensive effort so bugs can be reproduced and tests can be ran locally; if there is nothing explicitly mentioning a difficulty or impossibility in running the repo's contents locally, this passes | required |

With each accepted candidate, report a one-line difficulty note in
the read-out summary:

- **straightforward**: the issue names where the change lives and the
  change is bounded.
- **moderate**: the location is yours to find, or several files are
  involved.
- **ambitious**: an open design edge, or an unfamiliar subsystem;
  name the edge, because claiming this issue means raising it with
  the maintainer early.

The note is information for the chooser, never a verdict input: it
does not appear in the fenced JSON block, it never changes accept or
reject, and in eval mode it is skipped entirely.

I wrote the rubric by hand and CodePath fellows wrote the difficulty
note.

**`Bash`, `Read`, `Write`, `Edit`**

**What it is, and the judgment hole I wrote:**

The file and shell tools, `Bash`, `Read`, `Write`, and `Edit` made the 
automation possible.  `Bash`, in particular, allows Claude to access 
the `git` and `gh` commands to work with GitHub and verify the wording 
of messages or status of automated, server-side continuous integration 
tests.  `gh` was necessary for sifting through all the less or 
inappropriate repos to find one that is valid for me to work on.

**How it evolved, dated:** 

From 9/22/2026 onward:

While I did not have to create these tools, they were indispensable, 
as mentioned above, and I just had to mention them.

**Evidence:**

I didn't save any such reference calls during working with the CodePath
weekly project, but the following is an excerpt from a class project
in college.  The results are unimportant, so they're represented by the 
ellipsis "...".  It still is important for me to recognize the value of 
this tool.

```Text
Write(logs/changes.md)
Added 28 lines, removed 2 lines
  ...
```

**`AskUserQuestions`**

**What it is, and the judgment hole I wrote:**

AI absolutely has to have a human in the loop to keep from making huge
mistakes, especially when the logs are quiet.  In conventional coding,
this is referred to as a silent bug.  It doesn't trigger alarms, won't
throw exceptions or show up in static checks in the IDE, but they do
keep programs from behaving properly.  They can be sometimes very hard
to debug, too.  AI doing this is a hundred times worse, because it can
do so very much in such a short period of time.  Without this tool,
Claude can roll over an entire operating system, let alone a single 
repo, and cause havoc and emergency.

**How it evolved, dated:**

I did not write this, but felt it necessary to give it as one of the
tools I worked with because of how important it is.

**Evidence:**

I don't have evidence of this saved or in the history of Claude that
I've been working with, today.  However, I can explain the process.
I asked it to restore some things from `.git/lost-found/other` to bring
back something I'd accidentally done a `git restore .` command on when
thinking I was in another repo.  It found what it needed then prompted
me to make a decision about what to restore given that there was already
something present in one of the files I'd asked it to work on.

**`voice-guard`**

**What it is, and the judgment hole I wrote:**

I wrote these to ensure that the maintainers that I would be working
for by pushing to their repos had everything they needed to judge if my
plan and implementation were worthy in their spaces.  They had to be
able to understand what the change is and what issue I am targeting 
without guessing or having to look things up.  The `voice-guard` also 
needs to enforce having both a valid title and body before pushing, as
well as guide me in asking if issues are still open.

**How it evolved, dated:**

11/12/2026

As mentioned above, once I had figured out how this system worked, I
"had a good bead on things," as people say.  I copied various lines
from different skills into voice-guide/voice-guide.md and didn't
really have to change anything afterward.  I just worked within those
guidelines.

**Evidence:**

Here are some dated log entries in `voice-guard/guard-log.md`:

- 2026-11-10 12:07 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh issue comment --help
- 2026-11-10 12:09 [manual] stop: rule broken: "Demonstrate that I have read the issue thread fully." | target: claim-draft.md
- 2026-11-10 16:23 [manual] stop: rule broken: "A directly answerable question for the maintainer, with what I already checked and file, line, and version, so they don't have to ask me." | target: /home/user/Documents/github/codepath/ai301-unit6-starter/claim-draft.md
- 2026-11-10 16:25 [manual] stop: rule broken: "No AI-written comments." | target: /home/user/Documents/github/codepath/ai301-unit6-starter/claim-draft.md
- 2026-11-10 16:26 [manual] stop: rule broken: "A directly answerable question for the maintainer, with what I already checked and file, line, and version, so they don't have to ask me." | target: /home/user/Documents/github/codepath/ai301-unit6-starter/claim-draft.md
- 2026-11-10 16:26 [manual] pass | target: /home/user/Documents/github/codepath/ai301-unit6-starter/claim-draft.md
- 2026-11-12 10:01 [hook] stop: rule broken: "No AI-written comments." | target: gh pr create --repo InsightSoftwareConsortium/ITK
- 2026-11-12 10:19 [manual] pass | target: PR.md
- 2026-11-12 10:19 [hook] stop: could not read the body file: [Errno 2] No such file or directory: '/home/user/Documents/github/codepath/ai301-unit6-starter/$S/pr-body | target: gh pr create --repo InsightSoftwareConsortium/ITK
- 2026-11-12 10:20 [hook] pass | target: gh pr create --repo InsightSoftwareConsortium/ITK
- 2026-11-12 13:21 [manual] stop: rule broken: "Demonstrate that I have read the issue thread fully." | target: claim-draft.md
- 2026-11-12 13:22 [manual] stop: rule broken: "Demonstrate that I have read the issue thread fully." | target: claim-draft.md
- 2026-11-12 13:27 [manual] pass | target: claim-draft.md
- 2026-11-12 14:01 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh pr create --help

The first and last ones are the test with `--help` that are always
blocked.  You can see near the end several times it stopped because I
hadn't fully demonstrated that I'd read the issue fully before trying
to add a claim.  I'd pasted the claim manually in the browser, but 
used the `voice-guard` tool to ensure it was ready, first.

**`pr-monitor`**

**What it is, and the judgment hole I wrote:**

I wrote these to ensure that the maintainers that I would be working
for by pushing to their repos had everything they needed to judge if my
plan and implementation were worthy in their spaces.  They had to be
able to understand what the change is and what issue I am targeting 
without guessing or having to look things up.  The `pr-monitor` has to 
enforce guidelines regarding when to nudge maintainers if they haven't 
responded in long enough, when to walk away instead of trying to keep 
working at it, that I'm not arguing or trying to make excuses, and so 
forth.

**How it evolved, dated:**

11/12/2026

These were very straightforward and that week's activity of playing
around with a fake GitHub situation showed me all the things I needed
to keep an eye on, and therefore everything that went into the file,
`pr-monitor/playbook.md`.  I didn't have to alter it once setting it,
I just followed it as a guide.

**Evidence:**

Real PR (here: https://github.com/InsightSoftwareConsortium/ITK/pull/7159):

This pull request was created 11/10/2026 and altered on both 11/12/2026
and 11/14/2026.

Title

DOC: Cite perimeter paper in `ShapeLabelMapFilter` documentation - #7159

Body

Link the Insight Journal perimeter paper from the `ShapeLabelMapFilter` 
class documentation. Updated PR now also adds it to `ShapeLabelObject` 
class header docs. Closes #470.

<details>
<summary>AI assistance</summary>
  
    Tool: Claude Code (claude-sonnet-5-5)
    Role: located the doc comment, confirmed the link was absent from the tree, drafted the one-line comment
    Comment-only change; no local build or tests were run, relying on CI
    All changes were reviewed by the contributor before committing

</details>

<details>
<summary>Human Written</summary>

    The link to that paper was missing. It is now present. Insight Journal publication 852, "Efficient
    N-Dimensional surface estimation using Crofton formula and run-length encoding"

</details>

When tailored to my ITK repo commit, I had this one and only log in
`monitor-log.md`:

## 2026-11-12 16:02 [run] https://github.com/InsightSoftwareConsortium/ITK/pull/7159

- state: feedback-in: review feedback is in (latest from the thread: review (commented) under a day ago)
- move: No reply to post. This is a wait note, and nothing in the thread needs an answer. (via the review response form)
- state fingerprint: 292a2085a029
- mergeability: MERGEABLE/UNSTABLE

The rest are manual changes in browser after seeing requests for me
to change or add something.

## Inventory

- `ship-gate`: This tool helped me ensure that what I actually pushed was valid in the local scope before moving it to the repo; it made sure that the tests in the package manager, pixi, all passed; that the changes were planned and marked out and nothing else changed.  Basically, it made sure that I was able to actually run and test things so that my change didn't break anything.

## The Arc

The `Skills` built-in tool, with all the skills I wrote rules for, 
was fairly easy to complete.  Much of what I put in `issue-scout` in
week 1 was carried over, and so on with each new week's skill.  

Getting `voice-guard` finished was a bit more challenging, but not 
really that tough.  The same can be said of `pr-precheck` and
`ship-gate`.

**Beat 1**

Date: 9/22/2026--10/11/2026
Friction: Took some time to get used to this new way of doing things.  
Working with Claude instead of coding things myself or asking an AI 
tool to do the work without a skill present was completely new to me.

Change: Just kept at it till I understood.  I copied much of what I 
did from previous units into new ones.  It again took some time to 
make the rubrics judge how I wanted them to, but by the end of the 
assignments, I didn't need to alter anything any more.  I just copied 
everything I'd already done and added each new week's stuff.  I wrote 
`plan.md`, `comment.md`, and `procedure.md`.  `procedure.md` was 
already written from `issue-check` week, so I took a lot of notes 
from there when writing my version in the new unit.  `plan.md` and 
`comment.md` were simple enough: my and the repo's environment 
versions, changes proposed for the RAG retriever in the curated issue 
I'd selected to work on, tests to perform, things I didn't know for 
sure in unknowns, questions to the maintainer(s), and an AI Use 
statement.  They both followed my `voice-guide.md` and `rubric.md`.
I wrote `SKILL.md` while using previous weeks' `SKILL.md` files as
a starter.  `commend.md` and `plan.md` are present and the same as
from the previous week.  I also wrote `references/evidence-guide.md`,
where again I followed the format of previous weeks to produce my
copy.

Result: What happened was that it worked.  I got good scores for the
assignments and learned how to use Claude Code for semi-automatically
interacting with GitHub repositories.  The actual grades were each 
quite good, though not perfect.

**Beat 2**

Date: 11/3/2026--11/17-2026
Friction: The most challenging part up till writing `issue-scout` was 
getting used to this new way of doing things with AI.  By this 
point, however, time was an issue.  As a full time masters student,
course projects were the main goal and CodePath had to take a side
seat for several weeks.

Change: Once I had time again, I started working on CodePath beat 2.
It started with `issue-scout` but also included adding new tools, as
well.  I'm still waiting on a new score from a second submission to
try to increase my grade from initial, and there may be even more 
things to change in the `beat-2-contribution/contribution-story.md`
file before I'm done.  I have read the grading rubric and am having
trouble interpreting what it means for the given remarks per section.

Result: I got things how I wanted them to be and submitted in Unit 
5's submission link.  222/250.  This beat verified that what I'd 
learned in beat 1 was valid for real, live repos, not just fake ones.
The addition of extra tools helped me understand how to gate my 
throughput to ensure it's all top-notch and the best it can be for
maintainers to read.  The actual repo I worked on thanked me for my
commit and helped me be more confident in future real work.

**Beat 3**

Date: 11/17/2026
Friction: This is a writing assignment, so the main difficulty is
doing all this writing.  As a serious friction, I'm really not sure
if employers will appreciate these walls of text in considering me
for positions.  It makes it tough to keep going when I don't know
the purpose behind things.

Change: As always, there's really nothing to do other than keep
going.  All problems in life come down to determination.

Result: None.

## Limitations and What's Next

This toolkit doesn't really take that much time off my plate as a
software engineer or data scientist and has little, if any, bearing
on whether or not I'll get a job in my field.  It's just for 
helping gate commits into GitHub repositories, which will hopefully
help show future employers that I'm skilled, fast, and active.
However, it could probably have an automated pipeline tool that 
does all the skills, updates whatever it's to work on, and prepares
submissions for claim comment, commit comment, and PR.  It would
put all these into a file or files for me to review, and I could
say yay or nay to make it actually happen.  It would thoroughly
speed up my overall process, though it puts me more as an AI agent
manager than a software engineer or data scientist.

**Tool limits.** 

issue-scout: `none`

voice-guard: `none`

pr-monitor: `none`

ship-gate: `none`

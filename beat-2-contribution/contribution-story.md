# Contribution: Document LabelObject perimeter computations #470

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]

**Student:** Josh Borthick

**GitHub Username:** joshb019919

**Issue:** https://github.com/InsightSoftwareConsortium/ITK/issues/470

**Pull Request:** https://github.com/InsightSoftwareConsortium/ITK/pull/7159

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Wrote the `gh` query and ranking filters in search-strategy.md then selected an issue with issue-scout**

**11/12/2026**

For the activity, I chose the query `gh search issues --language python --state open --no-assignee --label "good first issue" --created ">2026-11-01" --json title,repository,labels,createdAt,updatedAt,commentsCount,url --limit 100` because it uses the language I want, is likely unpicked and good for beginners' first issue, isn't assigned, and recent enough to hopefully be actively maintained.  I wrote other queries for Java, Go, and C++ too, but they're commented out in case I wanted to try another language.  My filters preferred 0 comments, work involving AI models, and only issues in English.  Nothing broke really, all the issues the scout returned were interesting, passed the rubric and filters, and are issues I could work on with Claude.

**Unit 6: Drafted a claim comment and checked it with repro-check.**

**11/12/2026**

I added the required check to the voice-guard, did the symlinking.  I did the repo-memory file.  Otherwise, I copied everything that was already there into the new files.  The only things that broke anything were my claim comment formats, which I altered till it passed.

**Unit 7: Added ship-gate and ran pr-precheck**

**11/12/2026**

The ship gate kept failing thread-check test, so I had to give the Python file the ability to look at PR comments to find where a guy had asked me to make a small change after submitting the PR.  I ended up having to install Pixi package manager and explicitly give the full path to it because the pre-commit check couldn't find it.  I originally didn't have an "exclude" table in the gate, so I added some to keep it from running if functional code never changes (only docstring changes in this one).

**Unit 8: Ran the PR-monitor on PR #7159 with my playbook**

**11/12/2026**

My playbook enforces not "nudging" for at least 7 days of inactivity, responding courteously, and things like this.  PR-monitor found that the maintainers approved my PR with only a minor change requested.  It's only waiting on a couple last CI tests, and has already been marked as able to merge.

---

## Why I Chose This Issue

I first tried a wild repo that I'd found from a regular filtered search, but was told it wasn't a big enough project and didn't have enough hands in it to count.  I then went through about 50 curated issues with filters "python" and "good first issue" to find one that passed my issue-scout (most were already claimed, had PRs or assignees, or weren't maintained).  I settled on one that seemed easy enough (classification of **straightforward**) and didn't have any claims.  

I was going to find a complex one to do, but realized that I was running out of time in this course.  This does fit my profile so well because it isn't challenging or involving Python, Rust, or the other things I wanted to work on.  This is a selection of convenience because I'm running out of time.  Actually though, I hope to learn how to run this ITK tool and some of the inner workings of its codebase, perhaps even ingratiate myself to the maintainers and owners and be allowed to work with them in earnest.

The verdict was "accept".  The fix itself is a rather simple documentation addition.

**Claim Link**
`https://github.com/InsightSoftwareConsortium/ITK/issues/470#issuecomment-6828340620`

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: 

```JSON
  {
  "item": "https://github.com/InsightSoftwareConsortium/ITK/issues/470",
  "checks": [
    {"name": "Recent default-branch commits", "grade": "pass", "evidence": "newest default-branch commit 2026-11-12 (hjmjohnson)"},
    {"name": "Release recency", "grade": "pass", "evidence": "v5.4.7 published 2026-08-10"},
    {"name": "Archived flag", "grade": "pass", "evidence": "archived:false"},
    {"name": "Assignee", "grade": "pass", "evidence": "assignees: []; sjh26 unassigned 2021-08-18"},
    {"name": "Linked PRs", "grade": "pass", "evidence": "no PRs reference the issue; PR search for ShapeLabelMapFilter perimeter returned only unrelated #6521"},
    {"name": "Claim comments", "grade": "pass", "evidence": "3 comments, all Feb 2019; none are claims within 6 months"},
    {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction; Documentation/AI/ rules set disclosure conditions only"},
    {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md and Documentation/AI/*.md are conditions (disclose in PR, no AI Co-Authored-By), not a ban"},
    {"name": "Scope Feasible", "grade": "pass", "evidence": "one task: add link http://hdl.handle.net/10380/3342 to LabelObject perimeter docs; link absent from tree (code search: 0 results)"},
    {"name": "Locally Runnable", "grade": "pass", "evidence": "comment-only change; no stated difficulty"}
  ],
  "verdict": "accept"
  }
```

- Difficulties:  Difficulty was in finding an unclaimed issue on a repo that was actively maintained and wasn't someone's side project.
- What changed: I just keep trying repos from the curated issues selected by CodePath after adding the "Locally Runnable" check to the rubric to avoid an issue with another repo being something that required a supercomputer.

---

## Understanding the Issue

**Problem Description**

The class `ShapeLabelMapFilter` needed to also cite _Insight Journal publication 852, "Efficient 
N-Dimensional surface estimation using Crofton formula and run-length encoding"_ alongside it's citation already present.

**Expected Behavior**

It needs updated to cite that paper.

**Current Behavior**

It doesn't cite that paper.

**Affected Components**

The `ShapeLabelMapFilter` class in `ITK/Modules/Filtering/LabelMap/include/itkShapeLabelMapFilter.h`.

**Toolkit**

- Tool: issue-scout and voice-guard
- What it produced: Failure at first, then I found an issue that passed and altered the claim, commit, and PR messages till they passed the guard
- Difficulties: Finding an acceptable issue
- What changed: The `ShapeLabelMapFilter` docstring.

---

## Reproduction Process

**Environment Setup**

- **OS:** Ubuntu 26.04.1 LTS.
- **Kernel:** Linux 7.0.0-43-generic.
- **Architecture:** x86_64.
- **ITK:** `v6.0b02-6872-g2e3a1eb760` (development).
- **Toolchain:**
  - **Package Manager:** Pixi (conda-forge).
  - **Langauges:**
    - Python `>=3.13.5,<3.14`.
    - C++ `>17`.
  - **Dependencies:**
    - CMake `>=4.0.3,<5`.
    - Ninja `>=1.13.0,<2`.
    - ccache `>=4.13.6,<5`.
    - pre-commit `>=4.1.0,<5`.
    - C++ compiler `cxx-compiler >=1.10.0,<2`
- **Setup:**
  - `pixi install`.
  - `pixi run --as-is build`.
- **Challenges:** I have not built or run ITK's tests because this is a comment-only change.  Nothing in this change needs a build.

**Steps to Reproduce**

1. Fork InsightSoftwareConsortium/ITK.
2. Clone to local machine.
3. Observe that `ITK/Modules/Filtering/LabelMap/include/itkShapeLabelMapFilter.h` and `ITK/Modules/Filtering/LabelMap/include/itkShapeLabelObject.h` class headers have no citations for the paper, "Efficient N-Dimensional surface estimation using Crofton formula and run-length encoding".

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/joshb019919/ITK/commit/2e3a1eb7600d153cb71e3b6b7e69163d3ab108b5.
- **Screenshots/logs:** ![Proof of docstring changes](proof_of_docstring_change.png)
- **My findings:** The "reproduction" is a simple cloning of the repo that let me check the appropriate files' lack of that citation in their class docstrings.

**Toolkit**

- **Tool:** `gh api` to read the issue and its comments, and `grep` over the LabelMap headers; Claude Code ran both and summarized.
- **What it produced:** the issue text and four comments, and the grep showing no paper citation in the headers.
- **Difficulties:** `gh issue view` failed (Projects classic deprecation error).
- **What changed:** switched to `gh api`.

---

## Solution Approach

**Analysis**

The missing documentation comes from how the classes are split, which a maintainer (blowekamp) described on the issue: the data lives in the object, the filter computes it, and other filters reuse the filter, so it was never clear where to document it. Neither class's Doxygen comment cites the paper.

**Proposed Solution**

Add the citations to the docstrings of `ShapeLabelObject` and `ShapeLabelMapFilter` class headers.  Link to https://insight-journal.org/browse/publication/852/ for authors Gaetan Lehmann and David Legland.  No code changed (no functionality, only docstrings).  Nothing is removed, either, only added.

**Implementation Plan**

1. `itkShapeLabelMapFilter.h`: add the paper paragraph above `\author`. Done in commit `2e3a1eb760` (`DOC: Cite perimeter paper in ShapeLabelMapFilter documentation`, `Addresses #470.`).
2. `itkShapeLabelObject.h`: add the same paragraph to the class comment. Written but uncommitted in the working tree.
3. Run `pixi exec pre-commit run --files` on both headers and commit step 2 with a `DOC:` subject of 78 characters or fewer.
4. Open a draft PR with the AI disclosure only in a `<details>` block, per `Documentation/AI/attribution.md`.

**Derivation:** I originally mentioned changing both files, but only changed one.  I'll mention in PR `--force-with-lease` about it so maintainers can drop the update in `itkShapeLabelObject.h` if preferred.

**Toolkit**
- **Tool:** Claude Code, reading the three headers and the `.hxx`, and drafting the comment text; I reviewed and edited it.
- **What it produced:** the root-cause trace above and the two comment paragraphs.
- **Difficulties:** the draft of the second paragraph left trailing whitespace, caught in the diff review.
- **What changed:** the whitespace is to be fixed before the commit; nothing else.

---

## Testing Strategy

This is a comment-only change.  The checks show that the text landed and that the repo's own checks accept it.

- **Before and after:** `grep -c "publication/852"` on `itkShapeLabelMapFilter.h` at `upstream/main` gives 0. On my branch, `grep -n "insight-journal.org/browse/publication/852" Modules/Filtering/LabelMap/include/itkShapeLabel*.h` gives `itkShapeLabelMapFilter.h:46` and `itkShapeLabelObject.h:38`; the PR's two commits (`2e3a1eb760`, `f9d4f6074e`) touch exactly those two files, 5 insertions each.
- **Repo checks on PR #7159:** `pre-commit`, `doxygen-warnings`, `ghostflow-check-main`, `CDash`, `Greptile Review`, `Pixi-Cxx (ubuntu-22.04)`, `Pixi-Cxx (macos-15)`, `ARMBUILD-Ubuntu-24.04-arm` and `ITK.macOS.Python` pass. `ARMBUILD-Python` and `Pixi-Cxx (windows-2022)` were still pending when I looked.
- **Not run locally:** my manifest's build and `ctest -R ShapeLabel` commands. The pre-commit command passed in the ship-gate; the build and `ctest` rows are excluded because this clone's sparse checkout omits `CMake/`, so CI is the evidence for them.

**Toolkit**

- **Tool:** `grep` and `git` for before/after, and looking in the browser for the CI results.
- **What it produced:** the 0-hit and 1-hit greps above, and the list of passing and pending checks.
- **Difficulties:** `pixi` reports all checks either skipped or passed.  CI is still pending, though nothing has failed, yet.
- **What changed:** I recorded the pending checks instead of calling the PR green.

---

## Implementation Notes

**2026-11-12**

Read the issue thread. The issue asks for a link to the Insight Journal paper, and the thread leaves open whether attribute docs belong in the object or the filter. Posted my claim at 15:46 UTC and committed `2e3a1eb760` (`DOC: Cite perimeter paper in ShapeLabelMapFilter documentation`, 10:01 local) adding the citation in `itkShapeLabelMapFilter.h`.

**2026-11-12 (PR)**

Opened PR #7159 at 16:20 UTC. dzenanz requested author/title plus the direct link instead of the handle.  I replied that the changes were pushed.

**2026-11-12 (plan-check)**

plan-check rejected my plan a few times because my plan comment said dzenanz requested the direct link and I had only the issue thread to check it against.  The request was in the PR review and not the issue.  Once the PR was checked, the verdict became accept.  I also rewrote `plan.md` and `plan-comment.md` with files, exact text, a test plan and an AI-use section.

**2026-11-12 (second header)**

Added the same paragraph to `itkShapeLabelObject.h` and committed it as `f9d4f6074e` (15:27 local), pushed to PR #7159 with no trailing whitespace. My plan's Deviations section briefly said the header was not in the PR; the ship-gate's precheck caught that it had become false, and I corrected it.

**Toolkit**

- Tool: Claude Code (edits and drafts, reviewed by me), plan-check and ship-gate (and `git push --force-with-lease`).
- What it produced: the commit, the two header edits, the rewritten plan files and the manifest.
- Difficulties: the dzenanz attribution was graded wrong until the PR thread was checked, and the ship-gate blocks `gh pr create --help`.
- What changed: check the PR thread as well as the issue thread when grading a plan.

---

## Pull Request

**PR Link:** https://github.com/InsightSoftwareConsortium/ITK/pull/7159

**PR Description:** 

### Header

DOC: Cite perimeter paper in ShapeLabelMapFilter documentation - #7159

### Body

Link the Insight Journal perimeter paper from the ShapeLabelMapFilter class documentation. Closes #470.

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


**Maintainer Feedback:**

- 11/12/2026 13:00: We might also want to put author/title, in addition to link. Also, I think we switched to using direct links instead of handles, e.g. `https://insight-journal.org/browse/publication/852/`
- 11/12/2026 13:05: Thank you for this feedback. I'll switch this over and add author/title.
- 11/12/2026 13:15: @dzenanz Changes are pushed with full names and direct link.

**Status:** Waiting on CI tests to finish, otherwise already approved by 2 maintainers with write access.

**Toolkit**

- **Tool:** the ship-gate with my manifest and pr-precheck, run by hand against branch `doc-470-perimeter-paper-link` with `--title` and `--body-file pr-draft.md`.
- **What it produced:** Some blocks included `pixi: not found` (exit 127), the build failing because the sparse checkout omits `CMake/`, the precheck rejecting on unfetched issue text, and dzenanz's request actually being a reply to the PR instead of the issue claim. Once pixi was installed and the ship-gate was able to review PR comments too, it passed.
- **Difficulties:** Probably the biggest problem was the ship-gate not being able to see that the PR comment listed in the markdown file was not viewable from the issue-side of things.  I also had some checks listed that required a full run and test build even if no functional code changed.
- **What changed:** I called pixi by full path (`$HOME/.pixi/bin/pixi`) and moved the build and `ctest` rows to the excluded table. I changed the pr-precheck rubric's Diff-Present row to accept differences recorded in the plan's Deviations section. I fixed the gate's `fetch_issue` to use `gh issue view --json`, and added `fetch_pr_thread` so the precheck sees reviews on the branch's PR.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned that if I'm going to be using AI on a huge project, with many lines changed or added, it is very useful to have the skill fully fleshed out.  It's important to have gates in place to make sure issue claims, pull requests, and git pushes all follow given rules set down by maintainer-supplied requirements like AGENTS.md and CONTRIBUTING.md.  This all together allows me to focus on high-level concepts and decision making while I delegate actual tasks and low-level changes to Claude Code (or some other AI tool).

**Challenges Overcome**

Finding an available and appropriate issue to work on was the most difficult.  The only real fix is to keep looking.

**What I'd Do Differently Next Time**

Not rely on CodePath's curated list of issues, and instead work directly with the `gh api` calls to filter issues.

---

## Resources Used

I already knew most of what I needed to get this done by this point in this course, and I relied on Claude Code for the rest.  This particular issue was not a bug or feature, and was instead just an addition to some class docstrings to cite the source of a solution.  I needed no external documentation to assist me in setting things up.

- The original issue and dzenans's request for a change after I'd already pushed and made a pull request helped me to understand what needed to be done and how.  Source: https://github.com/InsightSoftwareConsortium/ITK/pull/7159.

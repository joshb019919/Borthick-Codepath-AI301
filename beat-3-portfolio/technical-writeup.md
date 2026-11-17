# Building a gated Claude Code workflow for open source contributions, and testing it on an ITK PR

## Overview

My work with CodePath has involved creating tools to guide my contributions to open source GitHub repositories.  Each tool calls upon a number of skills, each of which contains a number of markdown files to aide in the process.  

| Tool | Skills | Purpose |
|------|--------|---------|
| issue-scout | issue-scout | Score and rank open source GitHub issues by URL, giving a specific difficulty level and whether or not it passes the rules laid down by the rubric |
| voice-guard | repro-check | Require my claim comments and commit messages to follow a given style and be courteous |
| pr-monitor | | Enforces pull request title and body format as per a repo's style and preference |
| ship-gate | pr-precheck | Block a commit or push until my manifest's checks pass, including grading my plan and my PR title and body against the issue and the PR thread |

I tested the whole pipeline on a real contribution: [PR #7159](https://github.com/InsightSoftwareConsortium/ITK/pull/7159) to ITK, which cites a perimeter-estimation paper in two class docs and closes [issue #470](https://github.com/InsightSoftwareConsortium/ITK/issues/470).  The PR was merged on 2026-11-14.  The pipeline did not make the work much faster.  What it did was catch real mistakes before a maintainer saw them, and each failure sent me back to improve a tool.

## What happened

### Selecting the issue: a rubric that rejects things

Given my rubric rules, issue-scout grades repo issues and determines if it's a good issue to work on.  If it's not had a recent enough commit, or PRs go a very long time without a maintainer dealing with it, or if the AI-contribution policy states that no AI may be used, then it was not acceptable.  If it was acceptable, the issue also comes with a difficulty score.  **Straightforward** is an easy fix, **moderate** will be more difficult but can be done without much trouble, and **ambitious** will require getting with the maintainers to hash out architecture and plan, first, as they haven't figured out how they want the issue fixed.

I looked through 50+ issues, specially curated by CodePath personnel for student work.  Most of these failed because someone had already made a claim or was assigned, or the repos weren't actively maintained.  The first one I chose was someone's side project.  The second was a tool that required a specially configured supercomputer to run, and my commit couldn't be tested, locally.  A CodePath tech fellow suggested I keep looking on each.  This prompted me to add a "Locally Runnable" check to the rubric to stop accepting issues that coudln't be.  Eventually, I found one that was a tiny change, just an addition to some class docstrings.  Issue #470 passed every row and was straightforward.

```json
{
    {
        "name": "Claim comments", 
        "grade": "pass", 
        "evidence": "3 comments, all Feb 2019; none are claims within 6 months"
    },
    {
        "name": "Contribution policy", 
        "grade": "pass", 
        "evidence": "CONTRIBUTING.md has no AI restriction; Documentation/AI/ rules set disclosure conditions only"
    },
    "verdict": "accept"
}
```

This repo was well-documented, including containing CONTRIBUTING.md, attribution.md, and CLAUDE.md files to guide contributors in their work.  `Documentation/AI/attribution.md` noted that PRs need AI disclosure stated in a collapsible `<details>` HTML tag.

My original goal was loftier, but being short on time I selected this comment change issue, both to prove to myself that what I'd built would work and to demonstrate what an AI-assisted workflow could accomplish.

### plan-check: a miss that changed the tool

Claude originally included the scholarly paper citation as a "handle" link, but maintainer `dzenanz` asked for a direct link.  The plan I made failed several times because the tool as presented by CodePath (tech fellow-written Python script) could only see issue and claim comments.  It had to be extended to be able to also view pull request comments.  The plan was then accepted.

### The review comment the pipeline had to handle

After I opened the PR, dzenanz wrote:

> We might also want to put author/title, in addition to link. Also, I think we switched to using direct links instead of handles, e.g. `https://insight-journal.org/browse/publication/852/`

I made these changes and pushed again with `git push --force-with-lease` so that it updated that PR instead of creating a new one. I also added the same paragraph to `itkShapeLabelObject.h` (`f9d4f6074e`), since it dealt with the objects created in `itkShapeLabelMapFilter.h`.  Before the change, `grep -c "publication/852"` on `itkShapeLabelMapFilter.h` at `upstream/main` gave 0.  After it, the grep found the link at `itkShapeLabelMapFilter.h:46` and `itkShapeLabelObject.h:38`, counting as evidence of "test" success.  Given that this is a pure comment change and no functional code was altered, this was used, instead.

### ship-gate: three failures, three fixes

The ship-gate runs my manifest and pr-precheck before anything is pushed.  It failed on this PR in ways I had not predicted, including by not being able to see the PR thread:

- I fixed pr-precheck's `fetch_issue` to use `gh issue view --json`, and I added a `fetch_pr_thread` function so the gate reads the reviews on the branch's PR.
- My plan's Deviations section originally didn't have the second header in the PR.   Making the change in that file too made the gate flag the contradiction and I had to correct the plan..
- I originally didn't have the `pixi` package manager on my machine, so I installed it.  The tool still couldn't find it, so I called it by full path (`$HOME/.pixi/bin/pixi`).  My sparse clone has no `CMake/`, so the build and `ctest -R ShapeLabel` rows could never pass.  The ship-gate's rule table originally had things too strict for this repo, so I moved a couple of them to the excluded table and left the CI tests, ran on the repo's side, as the evidence.

### The result

After those fixes the gate passed and `pre-commit` ran clean.  My pr-monitor playbook, told me that the maintainers had approved the PR when it only had the one requested change, but having added the other change, they still eventually re-marked it as "ready to merge."  The CI tests passed `pre-commit`, `doxygen-warnings`, `ghostflow-check-main` and the Pixi build checks, and maintainer Hans Johnson merged the PR on 2026-11-14.

## Limitations and what's next

The toolkit did not save me much time. Most of the gain came from catching things, like the wrong attribution, the false Deviations claim and the missing AI disclosure.  A docstring change is also a weak test of it. No build or test ran locally, so the build checks in my gate are untested against real code.  I fixed each tool after a single failure but haven't run them on a second repo to tune them to ITK's larger overall style.  It definitely still needs ran on multiple repos, too, so it can be generalized to work anywhere.  Running them also still takes manual steps, and the work leans toward managing an AI agent more than writing code myself.

Next I would chain the skills into one pipeline that searches for an acceptable repository issue to work on, then writes the claim comment, commit message, and PR text to files for me to approve.  That would show whether the gate generalizes or only works for ITK.

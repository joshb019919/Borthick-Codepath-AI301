# Building a gated Claude Code workflow for open source contributions, and testing it on an ITK PR

## Overview

My work with CodePath has involved creating tools to guide my contributions to open source GitHub repositories.  Each tool calls upon a number of skills, each of which contains a number of markdown files to aide in the process.  

| Tool | Skills | Purpose |
|------|--------|---------|
| issue-scout | issue-scout | Score and rank open source GitHub issues by URL, giving a specific difficulty level and whether or not it passes the rules laid down by the rubric |
| voice-guard | repro-check | Require my claim comments and commit messages to follow a given style and be courteous |
| pr-monitor | | Enforces pull request title and body format as per a repo's style and preference |
| ship-gate | pr-precheck | Block a commit or push until my manifest's checks pass, including grading my plan and my PR title and body against the issue and the PR thread |

[
  {"item":"https://github.com/NX-AI/tirex-2/issues/121","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-11-03 (3 in the last day)"},
    {"name":"Release recency","grade":"pass","evidence":"latest release 2026-10-20"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"no cross-referenced or connected PRs in the timeline"},
    {"name":"Claim comments","grade":"pass","evidence":"comments=0"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no anti-AI language (it covers CLA and docs)"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"no AI_POLICY.md or AI_USAGE_POLICY.md; no AGENTS.md"}],"verdict":"accept"},
  {"item":"https://github.com/Plexito-de/spantruth/issues/33","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-11-03"},
    {"name":"Release recency","grade":"pass","evidence":"latest release 2026-11-03"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"none in the timeline"},
    {"name":"Claim comments","grade":"pass","evidence":"comments=0"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no anti-AI language"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"AGENTS.md is written for coding agents (pro-AI); no AI-ban file"}],"verdict":"accept"},
  {"item":"https://github.com/Sanjeev-Karthick/agent-bucket/issues/1","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-11-03"},
    {"name":"Release recency","grade":"fail","evidence":"no releases (404)"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"none in the timeline"},
    {"name":"Claim comments","grade":"pass","evidence":"comments=0"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no anti-AI language"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"no AI policy files; no AGENTS.md"}],"verdict":"accept"},
  {"item":"https://github.com/Mihirajmera/agent-flight-recorder/issues/5","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"last commit 2026-10-26"},
    {"name":"Release recency","grade":"fail","evidence":"no releases (404)"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"none in the timeline"},
    {"name":"Claim comments","grade":"pass","evidence":"comments=0"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no anti-AI language"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"no AI policy files; no AGENTS.md"}],"verdict":"accept"},
  {"item":"https://github.com/loopmark-opensource/loopmark-agent/issues/54","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-11-03"},
    {"name":"Release recency","grade":"fail","evidence":"no releases (404)"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"none in the timeline"},
    {"name":"Claim comments","grade":"pass","evidence":"comments=0"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no anti-AI language"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"no AI policy files; no AGENTS.md"}],"verdict":"accept"}
]

Both issues are rejected. Both fail the required Claim comments check. The pytorch/ao issue also fails Linked PRs.

1. pytorch/pytorch#158968: reject
- Fails Claim comments: there are at least 5 claims within 6 months and no maintainer reply to any of them.
  - 2026-08-05: "may i work on this?"
  - 2026-09-01: three separate claims, including "I'd like to take this one… I'll follow up with a PR shortly"
  - 2026-10-25: "I'd like to contribute… as my first PyTorch contribution"
- Other signals:
  - It has 19 comments from a crowd of would-be contributors. It's also tagged internal ramp-up task and spawned sub-issues, so the scope looks like a tracker.
  - Linked PRs pass: the only cross-referenced PR, #179235, is closed.
  - Assignee, Archived flag, Recent commits (2026-11-03) and Release recency (2026-10-28) all pass.
- AI policy: AI_POLICY.md and AGENTS.md exist. They allow AI tools with disclosure aated contributions, so this isn't "no AI allowed" and the check passes. Note the ruleif you use Claude on the work.

2. pytorch/ao#3863: reject
- Fails Linked PRs: PRs #4406 (2026-05-15), #4490 and #4494 (both 2026-06-15) are opeach is attempting the same doc-warning fixes.
- Fails Claim comments: on 2026-06-16, a contributor wrote "I'll go ahead and start working on it and open a draft PR shortly!" That is within 6 months.
- Other signals:
  - It's labeled tracker, and a maintainer said "not sure how much is left".
  - Assignee, Archived flag, Recent commits (2026-11-02) and the AI policy check (AIis present, no AGENTS.md; no anti-AI language found in CONTRIBUTING.md) pass.
  - Release recency passes (2026-08-03).

I only searched the AI-related terms in each CONTRIBUTING.md. I read the AI_POLICY.md and AGENTS.md headers for pytorch/pytorch but not the ao ones.

The rubric works as written here. Both are well-maintained repos with huge claim backlogs. If you want a note for scan-notes.md: popular "good first issue" labels in big repos attract many unanswered
claims.

[
  {"item":"https://github.com/pytorch/pytorch/issues/158968","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-
    {"name":"Release recency","grade":"pass","evidence":"latest release 2026-10-28"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"pass","evidence":"only cross-referenced PR #179235
    {"name":"Claim comments","grade":"fail","evidence":"2026-09-01 'I'd like to take this one… I'll follow up with a PR shortly'; 2026-10-25 'my first PyTorch contribution'; no maintainer answer"},
    {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has an on; no ban"},
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"AI_POLICY.md: 'We support the use of AI tools' with disclosure; AGENTS.md bans only fully agent-generated
contributions"}],"verdict":"reject"},
  {"item":"https://github.com/pytorch/ao/issues/3863","checks":[
    {"name":"Recent default-branch commits","grade":"pass","evidence":"commits 2026-
    {"name":"Release recency","grade":"pass","evidence":"latest release 2026-08-03"},
    {"name":"Archived flag","grade":"pass","evidence":"archived=false"},
    {"name":"Assignee","grade":"pass","evidence":"assignees=0"},
    {"name":"Linked PRs","grade":"fail","evidence":"open cross-referenced PRs #4406,
    {"name":"Claim comments","grade":"fail","evidence":"2026-06-16 'I'll go ahead and start working on it and open a draft PR shortly!'"},
    {"name":"Contribution policy","grade":"pass","evidence":"no anti-AI terms found
    {"name":"Dedicated AI policy files","grade":"pass","evidence":"AI_POLICY.md exists (contents not read in full); no AGENTS.md; no anti-AI language found in CONTRIBUTING.md"}],"verdict":"reject"}
]

I graded all four in direct mode. Three are accepted and one is rejected.

Ranked read-out

All four came in by direct URL, so there's no search query or ranking signal to report.

Accepted, in fit order:

1. Sanjeev-Karthick/agent-bucket#1: Add opt-in Docling and FastEmbed smoke tests.
   - Fit: Python plus embedding models, the closest match to your AI model work.
   - Difficulty: moderate. The acceptance criteria are explicit, but you'd have to learn two libraries and write the docs/testing.md notes on downloads, licenses and caching.
   - Preferred checks: no releases yet (fail). The repo is only about a week old and has a single committer.
2. loopmark-opensource/loopmark-agent#54: Deduplicate the website fetch and HTML helpers.
   - Fit: Python, httpx and agent tooling.
   - Difficulty: moderate. It's a refactor across audience_tools.py and audience_research.py, and the issue says it pairs with #52, which you'd want to check first.
   - Preferred checks: no releases (fail). Commits are recent (2026-11-06) but all from the opener.
3. Mihirajmera/agent-flight-recorder#5: Add --format json to afr verify.
   - Fit: Python CLI, but little ML or async.
   - Difficulty: straightforward. The issue names the file (__main__.py) and the test file (tests/test_report_cli.py).
   - Preferred checks: no releases (fail). The last commit was 2026-10-26, within the 6-month window.

Rejected:

- pytorch/ao#3863: Resolve doc build warnings.
  - It fails on linked PRs: PRs #4406, #4490 and #4494 are open and cross-referenced.
  - It fails on claim comments: brittneylilly's claim on 2026-06-16 is within 6 months, and no maintainer answered it.
  - It fails on scope: it carries the tracker label and is an open-ended "resolve warnings" container.
  - A merged PR (#4475, 2026-06-12) also falls inside the 6-month window.

Notes

- All three accepted repos have a single maintainer, and the issues were opened on 2026-11-03. The maintainer is active, but the repos are small and new, so the first review may depend on one person.
- The loopmark issue body says "Generated with Claude Code". That is not a policy, and the rubric doesn't look at it.
- No repo had an AI ban. pytorch/ao's AI_POLICY.md sets conditions only (disclose AI content, review it), so it passes. CLAUDE.md exists there too.
- Per scope.md, comment on the issue as soon as you pick one, so you become the claim signal for the next person.

[
  {
    "item": "https://github.com/Sanjeev-Karthick/agent-bucket/issues/1",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03, pushedAt 2026-11-10"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "timeline shows no PR references"},
      {"name": "Claim comments", "grade": "pass", "evidence": "no comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one piece of work: opt-in smoke suite with explicit acceptance criteria"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/loopmark-opensource/loopmark-agent/issues/54",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-06"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "timeline shows no PR references"},
      {"name": "Claim comments", "grade": "pass", "evidence": "no comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md covers setup, tests and PRs; no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one refactor: make analyze_website_for_audience use fetch_site_summary and drop duplicate helpers"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/Mihirajmera/agent-flight-recorder/issues/5",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-10-26"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "timeline shows no PR references"},
      {"name": "Claim comments", "grade": "pass", "evidence": "no comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: add --format json to the verify parser, plus a test"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/pytorch/ao/issues/3863",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-07"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-08-03"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #4406, #4490, #4494 open and cross-referenced; #4475 merged 2026-06-12"},
      {"name": "Claim comments", "grade": "fail", "evidence": "brittneylilly 2026-06-16: 'I'd like to help with this issue'; no maintainer answer"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no ban; AI_POLICY.md sets disclosure and review conditions"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AI_POLICY.md and CLAUDE.md set conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "fail", "evidence": "labelled 'tracker'; open-ended 'resolve doc build warnings' across many files"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/2650",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "no claims; newest comment wwieder 2026-10-01 marks it 'eventually'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "samsrabin 2024-08-28: only tools/contrib/ and commented lilac lines affected; 'should be an easy fix'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/DataHaskell/dataframe/issues/167",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-08"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest activity samimshoaib01 2026-03-10, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "mchav 2026-03-10: 'add some gzip tests' with data generated by pandas or duckdb"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/2256",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "0 comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one behavior: die with an error whenAMELIST_OPTS and user_nl_clm"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/2063",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "only PR #1959, merged 2023-08-16"},
      {"name": "Claim comments", "grade": "pass", "evidence": "single comment ekluzek 2025-02-05, n
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: initialize four BGC profile variables to nan for FATES"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/1709",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment billsacks 2022-04-14, not a claim"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: meaningful init_interp eiffers; may be solved by #1710"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/1710",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "0 comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: restart read aborts with a clear error when a variable's subgrid level mismatches"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/DataHaskell/dataframe/issues/164",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no open PR; PR #182 (little-endian decod5, older than 6 months, and may already cover this"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim Jeet-kingdom 2026-04-18, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: unroll the byte-decoding}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/2497",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment ekluzek 2024-04-29"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: use the full MPI library instead of mpi-serial in tests; labelled 'blocked: dependency' on a cime mpirun update"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/Cog-Creators/Red-DiscordBot/issues/6474",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-03-06"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #6548 open, updated 2026-05-22; label
      {"name": "Claim comments", "grade": "pass", "evidence": "no comments in the last 6 months; last comment Kowlin 2025-10-02"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one command: [p]slash clear to disab
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/DataHaskell/dataframe/issues/166",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-08"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PRs #176 and #195 closed unmerged; no open PR, but #195 was closed 2026-07-09, inside 6 months, which the verdict rule counts"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment daikonradish 2026-02-26
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: BROTLI decompression for Parquet reads"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/DataHaskell/dataframe/issues/151",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #193 closed unmerged; no open PR, butside 6 months, which the verdict rule counts"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment darthcoder 2026-03-24, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one effort: preallocated buffers and reads"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/3693",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "fail", "evidence": "Rasaec5 2026-07-06: 'I'd love to woreplied and the thread is active"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one refactor: shared function to move excess soil water upward"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/3152",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #4295 closed unmerged 2026-11-03; no onths"},
      {"name": "Claim comments", "grade": "fail", "evidence": "YisacTW 2026-11-03: 'I'd like to investigate this'; samsrabin: 'no thanks, we will want to do this ourselves'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one task: add table-of-contents dire
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/2145",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-03"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment ekluzek 2023-09-25"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS
      {"name": "Scope Feasible", "grade": "fail", "evidence": "adopt a Fortran formatter and remove vertical alignment across all code; the formatter is not chosen ('not sure fprettify is the right one')"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ESCOMP/CTSM/issues/1621",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-0
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2025-12-12"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #4310 open, updated 2026-11-09 (adds
      {"name": "Claim comments", "grade": "fail", "evidence": "michellejtan 2026-11-01: 'I'd like to take this one as a first contribution'; ekluzek replied"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restr
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: shared constants file fo
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/14438",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #31900 closed unmerged (opened 2026-01-12, closed 2026-03-28); no open PR"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim Bhatta2006 2026-04-01, older than 6 months, no maintainer reply"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one task: notify Discord when an autotest run completes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/12913",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "latest claim DanishVasdev 2022-01-26; later comments are user reports"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one behavior: misleading Terrain data missing pre-arm message; fix design is open (squelch vs refuse to arm)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/19068",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PRs #19696 and #23062 closed, 2022-2023"
      {"name": "Claim comments", "grade": "pass", "evidence": "no claims in the last 6 months; 2026-02-04 comment suggests closing"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "fail", "evidence": "'Cleanup request' to make more featuodebase; open-ended"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/14439",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #34899 open, updated 2026-11-08"},
      {"name": "Claim comments", "grade": "pass", "evidence": "only comment 2022-12-08"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: visualise build_binaries_history.sqlite on the autotest results page"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/13932",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #33180 open, updated 2026-06-07"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim shubham-shahh 2024-11-21"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: POSITION_TARGET_LOCAL_NED dTARGET_LOCAL_NED"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/13464",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #19718 open (last updated 2022-03-27); counts as an active claim by the rubric"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2023-09-09"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: implement LOITER_TURNS within Guided mode"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/12996",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #30513 closed unmerged; no open PR"},
      {"name": "Claim comments", "grade": "fail", "evidence": "AhmetMert01 2026-10-18: 'I'd like to continue investigating this issue'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: checked_for_autoland reset
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/12625",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #30726 open (last updated 2025-10-29); counts as an active claim by the rubric"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2025-10-29"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: rename ADSB_OFFSET_LAT/LON to POS_X/Y/Z"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/12514",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #34403 open, updated 2026-09-14"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2022-11-11"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one fix: AP_NMEA_Output fixed buffer
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/11285",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #13745 open (last updated 2020-11-22); counts as an active claim by the rubric"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim shbhmexe 2025-10-26"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one change: boats loiter during SmartRTL path cleanup and failure"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/11284",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no open PR; but PR #34493 merged 2026-09emetry), inside 6 months, which the verdict rule counts"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2022-03-06"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: Guided mode wp_bearing wron
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/10050",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #35062 open, updated 2026-11-08; #33528-#33539 merged July 2026"},
      {"name": "Claim comments", "grade": "fail", "evidence": "hunt0r 2026-06-23: 'I'm now near thepting to solve this issue'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: SITL battery estimator per vehicle type"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/9873",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #34405 open, updated 2026-09-15"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2018-11-22"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: apply the rangefinder Onds"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/9843",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #33966 closed unmerged; but opened 2026-08-06, inside 6 months, which the verdict rule counts"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest comment 2021-09-07"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: PRX_ORIENT ignored in the TeraRanger EVO Tower backend"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/9828",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "fail", "evidence": "Santhosh09062006 2026-06-05: 'I'd like to work on this issue. I've started investigating'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: Sub vacuum testing mode as a Lua applet"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/19190",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PRs #19716, #23032, #31383, #32503 all closed; #32503 merged 2026-03-20 (older than 6 months) and may already deliver the issue's work"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim ohyaiamhere 2026-03-20; shbhmexe 2025-10-26; both older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure of AI assistance; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one piece of work: an autotest for the no-short-failsafe option in Plane auto mode"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/25792",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #30863 open, updated 2026-08-05"},
      {"name": "Claim comments", "grade": "pass", "evidence": "claims from 2025 only (MacOS 2025-07-28, ohyaiamhere 2025-08-25)"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: EAHRS duplicate temperature compensation"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/23927",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #31771 (updated 2025-12-23) and #287 stale"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim RafiShaik-AI 2026-03-10, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: servo/sprayer shutdown
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/20767",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "no PR references in the timeline"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim RafiShaik-AI 2026-03-10
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "fail", "evidence": "body calls itself 'a compendium issue of features' for the Custom Build Server; container issue"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/20716",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #30681 open, last updated 2026-05-04"
      {"name": "Claim comments", "grade": "pass", "evidence": "latest contributor comment ahmedmsalah99 2025-07-18"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: SmartRTL buffer fills in CiTL"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/32279",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #34654 and #35076 open; #35076 updated 2026-11-09"},
      {"name": "Claim comments", "grade": "fail", "evidence": "decodethehassan 2026-07-17; iamsaintzeno 2026-09-08 'I would love to take a stab'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure of AI assistance; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one refactor: move save_trim from RC_Channels_Copter to Copter"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/32090",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #32099 open (last updated 2026-04-11); counts as an active claim by the rubric"},
      {"name": "Claim comments", "grade": "pass", "evidence": "all claims dated 2026-02-04, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: dedicated external pressure failsafe for Sub"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/31588",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #31601 open, updated 2026-07-17"},
      {"name": "Claim comments", "grade": "pass", "evidence": "newest claim RafiShaik-AI 2026-03-10, older than 6 months"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: consume OPTICAL_FLOW_RA
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/31107",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #34451 (updated 2026-10-12) and #32114 open"},
      {"name": "Claim comments", "grade": "fail", "evidence": "devcodez674 2026-10-25; grayveyarden
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclo,
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one feature: AP_Gripper HOLD command support"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/29566",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-1
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #30678 open (last updated 2025-10-24)y the rubric"},
      {"name": "Claim comments", "grade": "pass", "evidence": "claims from July 2025; bringert 2026-09-10 is a suggestion, not a claim"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclosure; conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one piece of work: consume the gimbaOI_LOCATION and DO_SET_ROI_NONE"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/pytorch/ao/issues/3863",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-07"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-08-03"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #4406, #4490, #4494, #4967 open and cross-referenced"},
      {"name": "Claim comments", "grade": "fail", "evidence": "brittneylilly 2026-06-16: 'I'd like to help with this issue'; no maintainer answer"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no ban; AI_POLICY.md sets disclosure and review conditions"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AI_POLICY.md and CLAUDE.md set conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "fail", "evidence": "labelled 'tracker'; body is a multi-file doc-build warning dump"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/AcademySoftwareFoundation/dna/issues/255",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "fail", "evidence": "no releases published"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PR #264 open, cross-referenced, covers the full email provider feature"},
      {"name": "Claim comments", "grade": "pass", "evidence": "no comments"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "no AI_POLICY.md or AGENTS.md"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one backend feature: add an email provider following the existing provider pattern"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/ArduPilot/ardupilot/issues/33399",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last commit 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-14"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "fail", "evidence": "PRs #33654, #34132, #34913 open and cross-referenced"},
      {"name": "Claim comments", "grade": "fail", "evidence": "arham0254A 2026-06-29: 'I'm taking aly!'"},
      {"name": "Contribution policy", "grade": "pass", "evidence": ".github/CONTRIBUTING.md has no AI ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AGENTS.md requires disclos, not a ban"},
      {"name": "Scope Feasible", "grade": "pass", "evidence": "one bug: HAL_WITH_ESC_TELEM macro gating in takeoff_check.cpp"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/pytorch/pytorch/issues/158968",
    "checks": [
      {"name": "Recent default-branch commits", "grade": "pass", "evidence": "pytorch/pytorch pushedAt 2026-11-10"},
      {"name": "Release recency", "grade": "pass", "evidence": "latest release 2026-10-28"},
      {"name": "Archived flag", "grade": "pass", "evidence": "isArchived=false"},
      {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "PR #179235 closed unmerged; no open linked PR"},
      {"name": "Claim comments", "grade": "fail", "evidence": "tharun-7733 2026-10-25, LeonxLJX 2026-09-01 x3, JosueT1212 2026-08-05; no maintainer reply"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "AI_POLICY.md sets disclosure and review conditions, not a ban"},
      {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "AI_POLICY.md and AGENTS.md set conditions, not a ban"},
      {"name": "Scope Feasible", "grade": "fail", "evidence": "parent issue 'foreach_map enhancements' with sub-issues #158970 and #158975; no single piece of work in the body"}
    ],
    "verdict": "reject"
  },
  {
    "item":"https://github.com/InsightSoftwareConsortium/ITK/issues/1024",
    "checks":[
      {"name":"Recent default-branch commits","grade":"pass","evidence":"newest commit 2026-11-12 (hjmjohnson)"},
      {"name":"Release recency","grade":"pass","evidence":"v5.4.7 on 2026-08-10"},
      {"name":"Archived flag","grade":"pass","evidence":"archived:false"},
      {"name":"Assignee","grade":"pass","evidence":"assignees: []"},
      {"name":"Linked PRs","grade":"pass","evidence":"only PRs #1021 and #999, closed, 2019"},
      {"name":"Claim comments","grade":"pass","evidence":"no claim comments; 4 maintainer comments, latest 2025-01"},
      {"name":"Contribution policy","grade":"pass","evidence":"CONTRIBUTING.md has no AI ban"},
      {"name":"Dedicated AI policy files","grade":"pass","evidence":"AGENTS.md is an agent guide, no ban"},
      {"name":"Scope Feasible","grade":"pass","evidence":"one script, list of robustness fixes to ApplyScriptToRemotes.sh"},
      {"name":"Locally Runnable","grade":"pass","evidence":"no stated difficulty running it"}
    ],
    "verdict":"accept"
  },
  {
    "item":"https://github.com/GothenburgBitFactory/taskchampion/issues/410",
    "checks":[
      {"name":"Recent default-branch commits","grade":"pass","evidence":"2026-11-12"},
      {"name":"Release recency","grade":"pass","evidence":"v3.1.0 2026-05-30"},
      {"name":"Archived flag","grade":"pass","evidence":"archived:false"},
      {"name":"Assignee","grade":"fail","evidence":"assignees: [BenitaMags]"},
      {"name":"Linked PRs","grade":"pass","evidence":"PR #795 closed (2026-11-10)"},
      {"name":"Claim comments","grade":"fail","evidence":"2026-11-09 'I'd like to contribute', maintainer approved"},
      {"name":"Contribution policy","grade":"pass","evidence":"no AI ban found"},
      {"name":"Dedicated AI policy files","grade":"pass","evidence":"none present"},
      {"name":"Scope Feasible","grade":"pass","evidence":"write tests for manually edited DB"},
      {"name":"Locally Runnable","grade":"pass","evidence":"no stated difficulty"}
    ],
    "verdict":"reject"
  },
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
]

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

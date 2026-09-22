# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/10

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

{"item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/10", "checks": [
   {"name": "Recent default-branch commits", "grade": "pass", "evidence": "last push 2026-09-16"},
   {"name": "Release recency", "grade": "fail", "evidence": "no releases or tags exist in the repo"},
   {"name": "Archived flag", "grade": "pass", "evidence": "archived: false"},
   {"name": "Assignee", "grade": "pass", "evidence": "assignees: []"},
   {"name": "Linked PRs", "grade": "pass", "evidence": "no cross-referenced PRs"},
   {"name": "Claim comments", "grade": "pass", "evidence": "0 comments"},
   {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI statement"},
   {"name": "Dedicated AI policy files", "grade": "pass", "evidence": "none found in repo"}
], "verdict": "accept"}

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

agreement: 15/20 scored items  (bar: 18/20: below the bar)
agreement: 18/20 scored items  (bar: 18/20: PASS)
agreement: 18/20 scored items  (bar: 18/20: PASS)
agreement: 18/20 scored items  (bar: 18/20: PASS)
agreement: 18/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

*issue-02*
*Rubric accepted.*
{"id": "issue-02", "source": "rupa/z#349", "category": "dead-repo", "calibration": false, "verdict": "reject", "note": "clean bounded bug, but no commits or releases in over a year and an unanswered tracker"}
My rubric accepted this where the gold standard rejects it because my rubric did not 
specially consider answered trackers and was lax in time-since-last-*.  It's part of 
the tradeoffs I was trying to balance when attempted a 20/20 score.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

_| Release recency | "latest release" under Repo facts or the Releases box in the right 
sidebar of the repo front page: the latest release and its date | last release within 1 year | preferred |_

I allowed release recency to be preferred and lenient because it could be a new tool 
or repo or the tool may be quite stable and the maintainers have no intention on 
releasing again, soon.  Originally, it was more stringent and rejected things.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

In attempting to match more possible repos, especially those too new for a release or 
PR, I made this check too lenient.  The provided issue analysis of issue-02 was in 
agreement with the gold standard until I change it from **required** to **preferred**.
Honestly, I'm fine with this.  Newer repos represent greenfield coding, which is
easier to work with.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

1. According to Claude, this issue (issue-10) deals with model optimization and
   model design--using an LLM for re-ranking retrieved documents before generation
   in RAG.
2. The verdict took my already-filled skills and interests into consideration and
   gave me a good insight into this selection.  My rubric never considered estimated
   effort required.  7-10 hours though, that's not too bad.
3. There will be no difficulty in claiming it since it is very new and no one else
   has claimed it, yet.  In case this is asking how difficult do I think it will be
   for me to complete it given my claim, I feel that it will be challenging to do
   correctly, but not terribly so.  I have read the paper on RAG in generative
   modeling and feel that I understand the ranking situation.  Attaching an LLM to
   this task should be entirely doable.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

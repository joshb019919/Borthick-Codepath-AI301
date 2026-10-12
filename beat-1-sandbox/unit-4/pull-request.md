# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

`https://github.com/codepath/pathreview-ai301-fa26-s3/pull/149`

**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]

`feat/10-rag-llm-reranker`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

`agreement: 19/20 scored items  (bar: 18/20: PASS)`
`agreement: 20/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

```Markdown
pkg-04\\
Rubric forces rejection because the PR's test section does not explain the tests in detail as per the repro and diff.  This agrees with gold labels.
```

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

```Markdown
| Testability | plan text | plan contains clear tests with command and output, something anyone could reproduce | required |\\
Initially, it only said "plan contains clear tests," with nothing about needing to specify command and output for reproduction.  This forces my rubric to accept pkg-04 when the gold label rejected it.  I added the extra part to align with the needs of this week's added lessons on working with public repos.
```

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

```Markdown
After adding the above from "Check Rationale," I re-ran with python eval/run_eval.py --rubric skill/rubric.md --only pkg-04.  The initial failing check now passes.
```

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.

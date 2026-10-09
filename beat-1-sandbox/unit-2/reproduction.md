# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

`joshb019919`

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

`https://github.com/codepath/pathreview-ai301-fa26-s3/issues/10`

```Markdown
Greetings.  I'd like to offer my services for this as a first contribution.
The results from rag/retriever/hybrid.py could easily be passed to 
Llama 3.1 (8B) in before passing to the generator.  Of course, other models
are acceptable, also.  I would call the new file rag/retriever/llm_rerank.py.
I do not think the LLM would need to be fine-tuned.  The base pretrained
model would work fine.

What is "small LLM" in terms of number of parameters or install size?

### Environment

**OS:** Ubuntu 26.04.1
**Kernel:** Linux 7.0.0-34-generic

### AI Use Statement

As a CodePath student in their AI301 course, I am using Claude Code to grade
and automate certain aspects of my work, such as issue selection, comment
readiness, and so forth.  I intend to use it to assist my work in learning
any missing links in information retrieval, RAG, and LLMs, as well as to 
help speed up my debugging.  I will not use it to "do everything for me," 
nor without fully reviewing everything it generates.
```

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

`https://github.com/codepath/pathreview-ai301-fa26-s3/issues/10`

```Markdown
### Reproduction and Logs

#### Environment
**OS:** Ubuntu 26.04.1
**Kernel:** Linux 7.0.0-34-generic
**Relevant Versions:** None mentioned in issue or pathreview repo
**Code State:** Currently unmodified
**Steps:**
1. Clone the `pathreview-ai301-fa26-s3` CodePath repo
2. Ensure that Docker and PostgreSQL are installed and running on your machine.
3. Change into your directories on the terminal or command prompt.
4. Do `make setup` to create the proper database entries.
5. Log into a profile at `http://localhost:5173` with one of the profiles provided in `docs/SETUP.md`.
6. Enter a GitHub username and a resume.

**Observed:** The RAG pipeline seems unconnected to anything, so it needs to be created/called in the unit tests.

As this is not a bug, this comment contains no reproducibility statement or any logs.  Images follow.
```

![half of showing the CodePath review tool running](running.png)
![other half of showing the CodePath review tool running](running2.png)

```Markdown
#### Expected Behavior Before

The keyword and vector approaches will retrieve chunks in proportion of 0.3 keyword, 0.7 vector.  The generator takes these ordered chunks and decides how many to use to generate text from.

#### Expected Behavior After

The keyword and vector rankers still retrieve chunks in that proportion, and the generator still takes in chunks to generate text.  However, there will be a small LLM between them that re-ranks based on the chunks' alignment with a query.  It will change only the score value of the output of the naive retrievers, altering it from a float to an integer, and pass those chunks on to the generator.

The class will have a field which can be set that deactivates the LLM so that output from the rankers passes directly as input to the generators.

The generator and keyword and vector rankers will not be affected.

#### Expected Testing Behavior

All features of the LLM will be unit tested to ensure both that they work and that they properly accept the output of the rankers and properly return input to the generators.  It will also be tested that the re-ranker deactivates and allows data to pass through, unchanged.
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

```Markdown
### 9/27/26 11:50 AM
categories: clear-accept 2/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 14/20 scored items  (bar: 18/20: below the bar)

### 9/27/26 11:56 AM (only pkgs 7 and 20)
categories: clear-accept 1/1  disclosure 0/1
agreement: 1/2 scored items

### 9/27/26 12:04 PM (only pkg 20)
categories: disclosure 0/1
agreement: 0/1 scored items

### 9/27/26 12:10 PM (only pkg 20)
categories: disclosure 1/1
agreement: 1/1 scored items

### 9/27/26 12:15 PM
categories: clear-accept 2/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 14/20 scored items  (bar: 18/20: below the bar)

### 9/27/26 12:18 PM (pkgs 01, 03, 05, 10, 11, 12)
categories: clear-accept 6/6
agreement: 6/6 scored items

### 9/27/26 12:20 PM
categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
#### run written to eval-run.txt
```

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

```Markdown
### Package: pkg-20
### Rubric: rejected
### Gold: rejected
### Reason:

The repo requires an AI use statement, even if only stating that no AI was used, and the 
claimant makes no such statement.
```

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`| no pressure | does not pressure the maintainer(s) into an assignment or acceptance | required |`

I originally had it combined with the `no promises` check, but Claude was getting confused on how to
interpret it.  I decided to split them into two checks that more accurately specified each.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

`| ai disclosure | the claim comment or repro report | aligns with ai use requirements in issue text 
or repo facts (contributing, ai policy, etc.) | required |`

`If the repo facts, issue text, or contributing, disclosure, or ai use policy are required but the 
claim mentions nothing about it, it fails.`

In the above check, I was still seeing `pkg-20` failing to match the gold standards.  I re-ran with 
`--only pkg-20` after altering the check to align with AI use requirements instead of a hard rule on
how AI was to be specified, and adding the "If the repo facts..." line to the verdict section.  It 
then passed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

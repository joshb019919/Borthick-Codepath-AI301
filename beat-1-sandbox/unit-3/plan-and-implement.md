# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

`joshb019919`

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

`https://github.com/codepath/pathreview-ai301-fa26-s3/issues/10#issuecomment-6021345861`

---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

`feat/10-rag-llm-reranker`

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

## Repro check: before and after the change

Unit 2 evidence: the two screenshots above (`running.png`, `running2.png`) show the
review page returning generic feedback. This is a feature, not a bug, and the
reranker is deliberately not wired into the app, so the page cannot show the change.
Instead, the check below runs the real `HybridRetriever` (real ChromaDB in a temp
dir, real BM25) and the real `LLMReranker`. Only the LLM call is a stand-in that
returns fixed scores, because Ollama is not available in this session. The Ollama manual check
from the Tests section is still outstanding.

Before = reranker disabled (the existing behavior). After = `enabled=True`.

### Check script (`rerank_check.py`, run from the repo root)

```python
"""Run real HybridRetriever + real LLMReranker; only the LLM call is a stand-in."""
import json
import sys
import tempfile
from types import SimpleNamespace as NS

from rag.retriever.hybrid import HybridRetriever
from rag.retriever.keyword_search import KeywordSearcher
from rag.retriever.reranker import LLMReranker
from rag.retriever.vector_store import VectorStore

QUERY = "python machine learning projects"
# (id, text, embedding). Embeddings are hand-made so the retriever's order is fixed.
DOCS = [
    ("c1", "python python python machine learning projects list of keywords", [1.0, 0.0]),
    ("c2", "built a python machine learning pipeline that classifies support tickets", [0.9, 0.3]),
    ("c3", "volunteer experience at a local food bank", [0.8, 0.5]),
    ("c4", "trained a python model for churn prediction and shipped it to production", [0.7, 0.6]),
]
# Stand-in for the LLM's judgement of each chunk against QUERY (0-10).
JUDGED = {"c1": 2, "c2": 8, "c3": 0, "c4": 9}


class StandInClient:
    """Mimics client.chat.completions.create(); returns the JUDGED scores as JSON."""

    def __init__(self):
        self.calls = 0
        self.chat = NS(completions=NS(create=self._create))

    def _create(self, **kw):
        self.calls += 1
        listing = kw["messages"][1]["content"]
        order = [next(i for i, d in enumerate(DOCS) if d[1] in line) for line in listing.splitlines()[3:]]
        scores = [JUDGED[DOCS[i][0]] for i in order]
        msg = NS(content=json.dumps(scores))
        return NS(choices=[NS(message=msg)])


with tempfile.TemporaryDirectory() as tmp:
    store = VectorStore(persist_dir=tmp)
    store.add_chunks(
        [(NS(id=i, text=t, source_id="s", chunk_index=n, section="skills"), e) for n, (i, t, e) in enumerate(DOCS)],
        "profile_p1",
    )
    kw = KeywordSearcher()
    kw.index([{"id": i, "text": t, "metadata": {}} for i, t, _ in DOCS])
    chunks = HybridRetriever(store, kw).retrieve(QUERY, "p1", [1.0, 0.0], max_chunks=4, min_score=0.0)

    client = StandInClient()
    mode = sys.argv[1]
    out = LLMReranker(client, "llama3.1:8b", enabled=(mode == "after")).rerank(QUERY, chunks, top_k=3)

print(f"mode={mode} llm_calls={client.calls}")
print(f"retriever order: {[c['id'] for c in chunks]}")
for rank, c in enumerate(out, 1):
    print(f"  {rank}. {c['id']} score={c['score']:.3f} :: {c['text'][:48]}")
```

### Commands

```bash
PYTHONPATH=. .venv/bin/python rerank_check.py before
PYTHONPATH=. .venv/bin/python rerank_check.py after
```

### Before

```text
mode=before llm_calls=0
retriever order: ['c1', 'c2', 'c3', 'c4']
  1. c1 score=1.000 :: python python python machine learning projects l
  2. c2 score=0.709 :: built a python machine learning pipeline that cl
  3. c3 score=0.608 :: volunteer experience at a local food bank
```

### After

```text
mode=after llm_calls=1
retriever order: ['c1', 'c2', 'c3', 'c4']
  1. c4 score=9.000 :: trained a python model for churn prediction and 
  2. c2 score=8.000 :: built a python machine learning pipeline that cl
  3. c1 score=2.000 :: python python python machine learning projects l
```

The retriever puts c1 (keyword-stuffed) first and c4 (the strongest match) last. With
the reranker on, c4 is first, c1 drops to third, and `score` is the 0-10 LLM score.
The tests in `tests/unit/test_reranking.py` cover the same behavior with a mocked client.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

`agreement: 20/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

*pkg-01*
My rubric rejected it, so did the gold standard.
The commenter gets it wrong and doesn't take into account that it runs fine in versions
of 3.13.5+.  My rubric catches this under "Wrong Cause" because the plan did not 
reproduce the cause in the issue.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

`| Executability | plan text | the plan contains a procedure to demonstrate the successful change | required |`

I designed it this way to make sure my plan gives a well-thought out procedure instead
of more nebulous concepts.  I didn't need to change anything to get it to get 20/20, 
this time around.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Assuming the expected answer is what I changed to try to get more points out of 20
but had to give something up for it, the answer is "nothing changed."  I know this
because I got 20/20 from the beginning.  I made it rather strict and it paid off.
A trade-off is that it made designing the plan and comment markdowns more difficult.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

# Plan: LLM Re-Ranker for Retrieved Chunks (Issue #10)

## Environment

OS: Ubuntu 26.04.1
Linux 7.0.0-34-generic
Ollama v0.35.1
Llama 3.1 8B (`ollama pull llama3.1:8b`)
Unmodified `main` repo state

## Observed in the Repo

`HybridRetriever.retrieve()` (`rag/retriever/hybrid.py:34`) takes
`max_chunks: int = 10` and returns `results[:max_chunks]` (line 117).
`ReviewGenerator.generate_full_review(profile_data, retrieved_chunks)`
(`rag/generator/review_generator.py:87`) uses `chunks[:10]` for
context (line 148) and `retrieved_chunks[:5]` for citations (line 170).

`ReviewGenerator` talks to its LLM through `openai.OpenAI(api_key, base_url)`.
Ollama serves an OpenAI-compatible endpoint, so the reranker uses the same
client type.

I did not find a Python caller that connects retriever to generator.
`docs/ARCHITECTURE.md` describes the connection, but I'm not sure how it's
wired up.

## Scope

One new file, `rag/retriever/reranker.py`, plus tests.

Changes to `hybrid.py`, `review_generator.py`, the evaluator, fine-tuning, or 
wiring the reranker into the running app will not be required.

### Interface

```python
class LLMReranker:
    def __init__(self, client, model: str, enabled: bool = False): ...
    def rerank(self, query: str, chunks: list[dict], top_k: int = 10) -> list[dict]: ...
```

`enabled=False` (default): `rerank()` returns `chunks[:top_k]` unchanged, so
the existing behavior is untouched and the feature stays optional.

`enabled=True`: the LLM scores each chunk's relevance to the query as an
integer from 0 to 10. The output is sorted by that score (highest first,
ties keep the retriever's original order) and cut to `top_k`.

To rerank more than the default 10, the caller has to retrieve more first,
e.g. `retrieve(..., max_chunks=30)`, then `rerank(..., top_k=10)`.

Each returned chunk keeps the retriever's shape: `{id, text, metadata, score,` 
`vector_score, keyword_score}`.

Only `score` is replaced by the LLM score. `vector_score` and
`keyword_score` are left as they were.

The default `top_k=10` matches the generator's `[:10]` context slice.

### Prompt and parsing

One call to `client.chat.completions.create` with a system prompt that
describes the task and a user prompt listing the query and the numbered
chunks. The model is asked to return only a JSON list of integers, one per
chunk, in order.

If the reply is not valid JSON, has the wrong length, or has a value outside
0 to 10, the reranker logs a warning and returns `chunks[:top_k]` in the
original order. A bad LLM reply must never drop or reorder chunks by accident.
Prompt text lives as a constant at the top of `reranker.py`.

## Tests

New file `tests/unit/test_reranking.py`. The LLM client is mocked, so no
Ollama is needed and the `test-unit` CI job stays green.

Mock returns scores `[2, 9, 5]` for three chunks: output order is
chunk 2, chunk 3, chunk 1.

`top_k=2` returns exactly 2 chunks, the two highest-scoring.

`enabled=False` returns the input order unchanged and the mock is never
called.

Each returned dict has the keys `id, text, metadata, score, vector_score,
keyword_score`, and `vector_score`/`keyword_score` are unchanged.

Mock returns non-JSON, a list of the wrong length, or an out-of-range
value: original order is returned.

Tied scores keep the retriever's order.

To Run: `pytest tests/unit/test_reranking.py`, then `make check && make test-unit`
to confirm lint, types and the full unit suite.

Manual check against a real model (not part of CI): with Ollama running,
retrieve with `max_chunks=30`, call `rerank(..., top_k=10)` with
`enabled=True`, and print the chunk ids before and after. The order should
differ from the retriever's order.

I considered using `rag/evaluator/` (`RelevanceScorer`, `FaithfulnessChecker`)
for the pass/fail check and decided against it. Both return one float over the
whole chunk set from keyword overlap and have no thresholds, so they can't show
whether a reranker changed the order. I may report their before and after
numbers as extra information only.

## AI Use Statement

I'm using Claude Code to read the repo, check this plan against a rubric, and
help with debugging. I review everything it produces before posting.

## Deviations

`test_disabled_still_applies_top_k` and `test_client_error_returns_original_order`
go a bit beyond the plan.  Otherwise, it's good to go.


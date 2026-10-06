# Plan

## Code

1. I'll create a new package to hold the scripts.
  a. `llm.py` (sets up the LLM, `calls retrieve()`, and calls `generate_full_review()`).
  b. `rank_prompts.py` (holds the system and user prompt).
1. I'll use Ollama to pull Llama 3.1 8B as a "small" model to do the re-ranking.
2. I'll call `retriever/hybrid.py`'s `HybridRetriever.retrieve()` method to get the documents.
3. I'll write a system and user prompt to tell it to review a series of documents for alignment with a query.
4. I'll tell it to suggest new scores as outputs that let the documents be sorted and returned.
5. I'll have the script sort and return the documents.
6. I'll pass the list of documents on to `generator/review_generator.py`'s 'ReviewGenerator.generate_full_review()`.

## Test

1. I'll build a unit test in `tests/` out of `pytest` or `unittest` to link everything together.

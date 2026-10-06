# Josh Borthick

Claim for the LLM-based re-ranker before text generation.

## Candidate claim comment

Greetings. I'd like to offer my services for this as a first contribution.
The results from rag/retriever/hybrid.py could easily be passed to
Llama 3.1 (8B) in before passing to the generator. Of course, other models
are acceptable, also

I do not think the LLM would need to be fine-tuned. The base pretrained
model would work fine.

What is "small LLM" in terms of number of parameters or install size?

## Environment

OS 1: Ubuntu 26.04.1
OS 1 Kernel: Linux 7.0.0-34-generic

## AI Use Statement

As a CodePath student in thier AI301 course, I am using Claude Code to grade
and automate certain aspects of my work, such as issue selection, comment
readiness, and so forth. I intend to use it to assist my work in learning
any missing links in information retrieval, RAG, and LLMs, as well as to
help speed up my debugging. I will not use it to "do everything for me,"
nor without fully reviewing everything it generates.

## Reproduction and Logs

### Environment

**OS**: Ubuntu 26.04.1
**Kernel**: Linux 7.0.0-34-generic
**Relevant Versions**: None mentioned in issue or pathreview repo
**LLMs**: Ollama
**Code State**: Currently unmodified
**Steps**:

1. Clone the pathreview-ai301-fa26-s3 CodePath repo

**Observed**: There is one file called `scripts/run_evals.py` which has the entrypoint into the retriever (`rag/retriever/hybrid.py`) in the rag directory. It will take in the files retrieved by the retriever, re-rank them, and pass them to the generator in `rag/generator/review_generator.py`'s `ReviewGenerator`.

As this is not a bug, this comment contains no reproducibility statement or any logs or images.

## Diagnosis

The feature will work by creating the retriever to retrieve documents.  These documents will be compared to a query by an LLM like Ollama 3.1 8B or GPT-OSS 20B.  A series of prompts will inject query and documents together to the model to output a re-ranked set of documents as best aligns with the query.  These will be injected into the review generator to generate text.

## Scope

This will create a new feature as per issue #10 to re-rank retrieved documents to align with a query using a small LLM.  

### Files Changed

`rag/rerank/reranker.py` will sit between `HybridRetriever.retrieve()` in `rag/retriever/hybrid.py` (line 129) and `rag/generator/review_generator.py`'s `ReviewGenerator.generate_full_review()` (line 87).

It must have a specific shape to fit into the generator: `list[dict]` of `{id, text, metadata(source_id, chunk_index, section), score, vector_score, keyword_score}`, ordered.  It must output only the first 10 chunks for context formatting and the first 5 for adding citations.

The `score` values will be updated by the LLM for sorting.

I don't believe I'll need to change anything else to use the RAG files already created.

## Tests

A new unit test (`unittest` or `pytest`) in `tests/unit/` called `test_reranking.py` would call the pipeline directly since they're not wired, anywhere.  It would instantiate and run the generator, then use the `eval_suite.py` in `rag/evaluator/` to check faithfulness and relevance score of returned documents.

*This project "runs" via Docker, but does not appear connected via Python files, so I am not sure what else to expect in terms of following the pipeline.  ARCHITECTURE.md insists they're connected, but I don't see it.*

### Unit 2 Steps Rerun

This is a feature, so just as before, there is no "bug" repro report.  An image showing that I have the tool working and open follows.  These are my personal GitHub and resume.

![half of showing the CodePath review tool running](running.png)
![other half of showing the CodePath review tool running](running2.png)

## Deviations

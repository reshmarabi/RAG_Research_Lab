# RAG Research Lab — Run Report

## Setup
- Dataset: BEIR SciFact (test split)
- Queries evaluated: 200
- Corpus documents: 5183
- Embedding model: `sentence-transformers/all-MiniLM-L6-v2`
- Top-k: 10
- Reranker enabled: True

## Results

| method                 |   Recall@10 |   MRR@10 |   nDCG@10 |   queries |   mean_search_latency_ms |
|:-----------------------|------------:|---------:|----------:|----------:|-------------------------:|
| BM25                   |      0.776  |   0.6261 |    0.6573 |       200 |                  79.3916 |
| Dense MiniLM           |      0.793  |   0.6366 |    0.6716 |       200 |                   0.7675 |
| Hybrid RRF             |      0.8388 |   0.6711 |    0.7067 |       200 |                 nan      |
| Hybrid + cross-encoder |      0.8388 |   0.6676 |    0.7034 |       200 |                2931.78   |

## Observations
- Best Recall@10 in this run: **Hybrid + cross-encoder** (0.8388)
- Best nDCG@10 in this run: **Hybrid RRF** (0.7067)

These are results from this specific run and query subset. They are not claims about all RAG workloads.

## Limitations
- SciFact is a scientific claim retrieval benchmark; findings may not generalize to enterprise documents or other domains.
- Retrieval relevance labels are incomplete by nature; an unlabelled document is not necessarily irrelevant.
- Latency depends on runtime, hardware, warm-up, batch size and concurrent load.
- This report evaluates retrieval. It does not establish generated answer correctness.
- Reranking compares only a candidate set retrieved by hybrid RRF.

## Next experiments
1. Repeat with `MAX_QUERIES = None`.
2. Compare another embedding model.
3. Vary top-k and candidate count.
4. Inspect failures by query type.
5. Add a labelled answer-quality benchmark before drawing conclusions about generation.

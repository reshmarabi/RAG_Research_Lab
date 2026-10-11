# RAG Research Lab — Technical Report Template

> Replace every placeholder with measurements from your run. Do not invent results.

## 1. Research question
Which retrieval configuration balances Recall@10, MRR@10, nDCG@10 and latency on BEIR SciFact?

## 2. Experimental setup
- Date:
- Python/package versions:
- Runtime/hardware:
- Query count:
- Corpus size:
- Models and revisions:
- Parameters (top-k, candidate-k, RRF k):
- Random seed:

## 3. Hypotheses
- H1: Dense retrieval will retrieve some relevant documents missed by lexical retrieval.
- H2: Hybrid RRF will improve ranking robustness over one retrieval method alone.
- H3: Cross-encoder reranking may improve ranking quality at an additional latency cost.

These are hypotheses, not guaranteed outcomes.

## 4. Results
Paste `outputs/retrieval_metrics.csv` here as a table.

## 5. Error analysis
For each method, inspect at least 10 failed queries. Categorize failures (terminology mismatch, ambiguity, missing evidence, ranking error, label incompleteness).

## 6. Ablations
- top-k:
- candidate-k:
- embedding model:
- reranker on/off:
- query subset/full test set:

## 7. Limitations
Discuss benchmark domain, relevance-label incompleteness, hardware dependence, and the difference between retrieval and generation quality.

## 8. Conclusion
State only conclusions supported by the measured results. Include negative or inconclusive findings.

## 9. Reproducibility
Link notebook commit, configuration, package versions and output artifacts.

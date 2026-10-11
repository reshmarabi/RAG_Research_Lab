# RAG Research Lab

A free-first, reproducible benchmark comparing BM25, dense retrieval, hybrid Reciprocal Rank Fusion (RRF), and optional cross-encoder reranking on BEIR SciFact.

## Research question

Which retrieval configuration best balances retrieval quality and latency for scientific claim retrieval?

## Run in Google Colab

1. Upload/open `RAG_LAB1.ipynb` in Colab.
2. Run cells top-to-bottom.
3. Start with `MAX_QUERIES = 200`; use `None` to evaluate all queries in the test split.
4. The notebook downloads the official BEIR SciFact dataset and saves metrics, predictions, failure cases, a sample corpus and a Markdown report under `outputs/`.

No paid LLM API is required. Retrieval experiments run without generation. Optional local Ollama generation is documented in the notebook and is not required for evaluation.

## Run locally

Use Python 3.10+ in a virtual environment:

```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows PowerShell
# .venv\Scripts\Activate.ps1

pip install -r requirements.txt
jupyter notebook RAG_LAB1.ipynb
```

Then run all notebook cells. A GPU is optional. Dense embedding and cross-encoder reranking will be slower on CPU.

## Methods

- BM25 lexical retrieval
- Dense retrieval with `sentence-transformers/all-MiniLM-L6-v2`
- Hybrid retrieval using Reciprocal Rank Fusion
- Optional reranking using `cross-encoder/ms-marco-MiniLM-L-6-v2`

## Metrics

- Recall@10
- MRR@10
- nDCG@10
- Search/reranking latency (reported separately; not directly comparable unless hardware and timing conditions are recorded)

## Dataset

BEIR SciFact is a scientific claim retrieval benchmark. Its Hugging Face dataset card reports 5,183 corpus documents and 1,109 queries across configurations, with a CC-BY-SA 4.0 licence. The notebook loads the BEIR test split from the official BEIR download.

- Dataset card: https://huggingface.co/datasets/BeIR/scifact
- Qrels card: https://huggingface.co/datasets/BeIR/scifact-qrels
- BEIR project: https://github.com/beir-cellar/beir
- BEIR paper: https://openreview.net/forum?id=wCu6T5xFjeJ

Review the dataset and model licences before redistributing data or weights. Prefer publishing download scripts and a small permitted sample over copying the full corpus into GitHub.

## Output artifacts

After a run, `outputs/` contains:
- `retrieval_metrics.csv`
- `retrieval_metrics.png`
- `run_config.json`
- `hybrid_failure_cases.csv`
- `sample_queries_and_predictions.csv`
- `sample_corpus.jsonl`
- `technical_report.md`

The report is generated from actual notebook metrics. Do not publish fabricated or assumed scores. Include your runtime, query count and hardware in the final report.

## Limitations

- SciFact findings may not generalize to enterprise RAG workloads.
- Relevance labels may be incomplete.
- Retrieval quality does not prove generated answer correctness.
- The optional reranker only reranks retrieved candidates.
- Latency depends on runtime, hardware, warm-up and batch settings.

## Suggested extensions

1. Add chunking experiments for long documents.
2. Compare a second embedding model.
3. Add a labelled answer-generation test set with citation correctness and abstention metrics.
4. Add OpenTelemetry traces and a FastAPI endpoint.
5. Add CI checks and a model/prompt regression gate.

## Licence

Code in this repository may be licensed separately (for example, MIT); that does not change the licences of datasets or model weights used by the project. Check each dependency's terms.

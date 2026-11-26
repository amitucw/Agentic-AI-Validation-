# Human-Supervised Agentic AI for Supply Chain Due Diligence

An initial research prototype for assessing Canadian corporate supply-chain reports using Python, Ollama and Qwen 2.5. It uses fixed specialized assessment roles, evidence checks, bounded retries and human approval. Adaptive agent orchestration and comparative performance have not yet been validated.

## Data source

[Public Safety Canada Supply Chains Report Catalogue](https://www.publicsafety.gc.ca/cnt/cntrng-crm/frcd-lbr-cndn-spply-chns/ctlg-en.aspx). Download selected reports separately. No corporate PDFs or empirical results are distributed in this repository.

## Installation (Windows)

1. Install [Python](https://www.python.org/downloads/) and [Ollama](https://ollama.com/download).
2. Open Command Prompt in the repository folder and run:

```bash
python -m pip install -r requirements.txt
ollama pull qwen2.5:7b
mkdir reports
```

3. Put downloaded PDF reports in `reports/`. Ensure Ollama is running; if necessary, run `ollama serve` in a separate terminal.

## Execution

```bash
python assess.py scan reports --model qwen2.5:7b
python assess.py review evidence.json
```

The scan writes `evidence.json` with candidate scores, quotations, page numbers, PDF hashes and timings. Review the entire original PDF, enter its source URL, and approve or defer each indicator. The review writes `results.json` and automatically exports fully approved records to `results.csv`. No input CSV is needed. Keep copies of outputs before rerunning because files may be overwritten. Image-only pages require OCR or separate handling before positive evidence can be verified by this script.

## Scoring

Each indicator is scored 0 (not disclosed), 1 (generic claim), or 2 (specific documented action, process or outcome). AIDI sums five AI indicators (0–10); DDQI sums six due-diligence indicators (0–12). A zero denotes absence of reported evidence, not proof of absence of a practice. Both indices are proposed research instruments requiring validation.

## Limitations

This software evaluates disclosure evidence, not actual labour conditions or legal compliance. Exact quote matching alone does not establish semantic relevance; human review is required. The code has passed Python syntax checking, but live Ollama testing, independent coding reliability and comparative evaluation are pending. No accuracy or efficiency improvements are claimed.

## Citation

Cite the associated manuscript when published and identify the repository release or commit used. No publication DOI has yet been assigned here.

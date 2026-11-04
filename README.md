# EduAssist AI — LLMOps Assignment 2

## What this project does
- Calls an OpenAI-compatible API for five academic questions using three prompt versions (15 requests).
- Measures wall-clock latency, records response status and token usage, and estimates token-based API cost.
- Registers three prompt versions in MLflow Prompt Registry, logs per-version metrics, validates v3 JSON outputs, and assigns the `production` alias to the recommended version based on measured results.
- Exports `latency_tokens_cost.csv` and `prompt_evaluation_results.csv`.

## Prerequisites
- Python 3.10+ (Python 3.11 recommended).
- An API key with access to the configured model. API usage may incur charges.
- Internet access for API calls.

## Setup
### macOS/Linux
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export OPENAI_API_KEY="your-key"
export OPENAI_MODEL="gpt-4.1-mini"
export OPENAI_INPUT_PRICE_PER_MILLION="0.40"
export OPENAI_OUTPUT_PRICE_PER_MILLION="1.60"
```

### Windows PowerShell
```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:OPENAI_API_KEY="your-key"
$env:OPENAI_MODEL="gpt-4.1-mini"
$env:OPENAI_INPUT_PRICE_PER_MILLION="0.40"
$env:OPENAI_OUTPUT_PRICE_PER_MILLION="1.60"
```

Never put a real API key in the notebook, source control, screenshots, or report. For other models, check the official pricing page and update both price environment variables before running.

## Run MLflow UI
From the project folder:
```bash
mlflow server --host 127.0.0.1 --port 5000 --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlartifacts
```
Open `http://127.0.0.1:5000`. Keep the server running while executing the notebook. If your MLflow version uses a different backend setup, use the command documented by that installed version.

## Execute
1. Start MLflow server.
2. Set `OPENAI_API_KEY`, model, and current prices as environment variables.
3. Open `LLMOps_Assignment_2.ipynb` in Jupyter.
4. Run all cells from top to bottom.
5. Check generated CSVs and the MLflow UI.
6. Capture screenshots of the experiment runs/metrics, Prompt Registry versions, version comparison/diff, and the `production` alias.
7. Fill the short report with your actual measured results; do not invent results.

## Model, API, pricing, currency
- API: OpenAI API, Chat Completions endpoint (`/v1/chat/completions`) through the official Python SDK.
- Default model: `gpt-4.1-mini` (override using `OPENAI_MODEL`).
- Example public standard pricing used for the default model: USD $0.40 / 1M input tokens and USD $1.60 / 1M output tokens, excluding cached-input discounts and other special pricing. Pricing reference checked 2026-11-02: https://developers.openai.com/api/docs/pricing
- Pricing changes; verify the official pricing page on the day you run the experiment. Cost figures are estimates based on usage fields returned by the API and configured rates. Monthly projection assumes 10,000 requests with the same average usage.

## Outputs
- `latency_tokens_cost.csv`: one row per API request (15 rows if all versions succeed).
- `prompt_evaluation_results.csv`: per-prompt-version aggregate metrics (3 rows).
- `mlflow.db` and `mlartifacts/`: local tracking artifacts created by MLflow.
- Screenshots: captured manually from the MLflow UI after execution.

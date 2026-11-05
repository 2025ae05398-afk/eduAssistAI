# EduAssist AI — LLMOps Assignment 2

## What this project does
- Calls an Llama 3.1 8B model Ollama API for five academic questions using three prompt versions (15 requests).
- Measures wall-clock latency, records response status and token usage, and estimates token-based API cost.
- Registers three prompt versions in MLflow Prompt Registry, logs per-version metrics, validates v3 JSON outputs, and assigns the `production` alias to the recommended version based on measured results.
- Exports `latency_tokens_cost.csv` and `prompt_evaluation_results.csv`.

## Prerequisites
- Python 3.10+ (Python 3.12 recommended).
- An API key with access to the configured model. API usage may incur charges.
- Internet access for API calls.

## Setup
### macOS/Linux

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Ollama Llama 3.1 8B
```
curl -fsSL https://ollama.com/install.sh | sh

ollama pull llama3.1:8b

export OLLAMA_NUM_PARALLEL=1
export OLLAMA_MAX_LOADED_MODELS=1
export OLLAMA_MAX_QUEUE=1


pip install -U ollama mlflow pandas psutil
ollama serve
```

### Jupyter install
```
pip install nbconvert
pip install notebook ipykernel nbconvert
source venv/bin/activate
jupyter --version
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser

```
### Verify installations:
```
python -c "import openai, mlflow, pandas; print('All major dependencies installed successfully')"
```

### Check MLflow:
```
mlflow --version
```

Never put a real API key in the notebook, source control, screenshots, or report. For other models, check the official pricing page and update both price environment variables before running.

## Run MLflow UI
From the project folder:
```bash
mlflow ui --backend-store-uri sqlite:///mlflow.db --host 0.0.0.0 --port 5000 --default-artifact-root ./mlartifacts
```
Open `http://127.0.0.1:5000`. Keep the server running while executing the notebook. If your MLflow version uses a different backend setup, use the command documented by that installed version.

## Execute
1. Start MLflow server.
2. Start Ollama.
3. Open `LLMOps_Assignment_2.ipynb` in Jupyter.
4. Run all cells from top to bottom.
5. Check generated CSVs and the MLflow UI.
6. Capture screenshots of the experiment runs/metrics, Prompt Registry versions, version comparison/diff, and the `production` alias.
7. Fill the short report with your actual measured results; do not invent results.

## Model, API, pricing, currency
- API: Ollama API, Llama 3.1 8B model, Python SDK.
- Default model: Llama 3.1 8B model.
- Pricing changes; Cost figures are estimates based on usage fields returned by the API and configured rates. Monthly projection assumes 10,000 requests with the same average usage.

## Outputs
- `latency_tokens_cost.csv`: one row per API request (15 rows if all versions succeed).
- `prompt_evaluation_results.csv`: per-prompt-version aggregate metrics (3 rows).
- `mlflow.db` and `mlartifacts/`: local tracking artifacts created by MLflow.
- Screenshots: captured manually from the MLflow UI after execution.

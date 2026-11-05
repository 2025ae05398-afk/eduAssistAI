# Pricing and technical references

- OpenAI API pricing (check again on execution date): https://developers.openai.com/api/docs/pricing
- GPT-4.1 mini model page: https://developers.openai.com/api/docs/models/gpt-4.1-mini
- MLflow Prompt Registry: https://mlflow.org/docs/latest/prompts
- MLflow prompt aliases / lifecycle: https://mlflow.org/docs/latest/genai/prompt-registry/manage-prompt-lifecycles-with-aliases/

The project defaults use USD $0.40 / 1M input tokens and USD $1.60 / 1M output tokens for `gpt-4.1-mini` as a documented example. Confirm model availability and current pricing before running; prices can change and this model page may indicate deprecation or a successor model. Set `OPENAI_MODEL`, `OPENAI_INPUT_PRICE_PER_MILLION`, and `OPENAI_OUTPUT_PRICE_PER_MILLION` to the actual selected model and rates.

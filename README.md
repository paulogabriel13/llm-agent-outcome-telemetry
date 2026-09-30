# Characterizing LLM-Based Agent Executions by Task Outcome

A data mining study (CRISP-DM) on OpenTelemetry GenAI telemetry.

This repository contains the reproducible notebook for the paper *"Characterizing LLM-Based Agent Executions by Task Outcome: A Data Mining Study on Telemetry Data"*, developed for the Data Mining course of the Master's Program in Applied Computing (PPCA) at the University of Brasília (UnB).

> **Paper:** link to be added.

## Research question

Do successful and unsuccessful executions of LLM-based agents show distinct execution behavior in the attributes recorded by telemetry: number of steps, execution time and token consumption?

## Context

LLM-based agents are becoming part of the digital customer journeys of financial institutions. In production, no verifier reports whether an agent solved the task, and operations teams only have telemetry. This study checks whether telemetry carries information about the task outcome, and which attributes match the [OpenTelemetry semantic conventions for generative AI](https://github.com/open-telemetry/semantic-conventions-genai), so that the procedure can be applied to other environments that adopt the same standard.

## Data

[`Exgentic/agent-llm-traces-v2`](https://huggingface.co/datasets/Exgentic/agent-llm-traces-v2) (Hugging Face): 10,056 agent executions across six task sets (AppWorld, BrowseCompPlus, SWE-bench, τ²-bench Airline, Retail and Telecom), five language models and five harnesses, recorded following the OpenTelemetry GenAI semantic conventions.

The notebook downloads the data (~230 MB) into `data/` on the first run. The dataset files are not stored in this repository.

## Method

- **Methodology:** Design Science Research, with a design proposition in CIMO logic.
- **Method:** CRISP-DM (business understanding, data understanding, data preparation, modeling, evaluation, deployment).
- **Comparison:** within each task set, by the Mann-Whitney test and the probability of superiority (PS), with 95% bootstrap compatibility intervals (1,000 resamples, fixed seed 42).
- **Checks:** correspondence of the attributes with the OpenTelemetry standard, comparison within each harness, closed-weight models only, and sensitivity to fast failures.

## Main results

- Unsuccessful executions take longer and more steps in AppWorld, BrowseCompPlus and τ²-Airline (PS up to 0.78 for execution time in AppWorld). Tokens separate less.
- In τ²-Retail and τ²-Telecom, results are most compatible with no important difference.
- The pattern holds within harnesses and with closed-weight models only.
- A second failure type, the fast failure (one model call and no step), is concentrated in two open-weight models in the customer-service task sets.
- Token counts match the OpenTelemetry standard exactly, execution time approximately, and the step count depends on the harness.
- Operational telemetry carries information about the task outcome, but not enough to indicate it on its own.

## How to run

**Google Colab.** Open the notebook in Colab and run all cells. All required libraries are preinstalled.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/paulogabriel13/llm-agent-outcome-telemetry/blob/main/llm_agent_outcome_telemetry.ipynb)

**Locally.**

```bash
pip install -r requirements.txt
jupyter notebook llm_agent_outcome_telemetry.ipynb
```

To use an existing local copy of the dataset, set the `DATA_DIR` environment variable to the folder that contains the parquet files.

## Repository contents

| File | Description |
|---|---|
| `llm_agent_outcome_telemetry.ipynb` | Full analysis, organized by CRISP-DM phase |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT License |

## Author

Paulo Gabriel Ribacionka Goes de Araujo, Master's Degree in Applied Computing (PPCA), University of Brasília (UnB).

## License

Code released under the [MIT License](LICENSE). The dataset is distributed by its authors under its own terms on Hugging Face.

# Jev versus a Fine-Tuned Detector Against Prompt Injection

CS182 final project. Team: Nahee Jeong, Namira Khanum, Jianing Li, Ontario Zeng.

We study guards against indirect prompt injection, where an attacker hides instructions in the data an LLM agent reads. The plan is to compare a zero-shot Jev guard with a fine-tuned DeBERTa-v3-base classifier on the InjecAgent benchmark.

## Status

Only the first step is done. We ran the undefended model, Qwen3.5-9B, on all 2,108 InjecAgent attack cases and analyzed the results. The guards, the classifier, and the clean test cases are not built yet, so this repository has no code for them.

## Reproduce the paper's results

Everything in Section 4.1 of the draft paper (Table 4, Figure 1, and the confidence intervals) comes from one notebook.

1. Open [`qwen35_9b_03_full_run_analysis.ipynb`](https://colab.research.google.com/github/naheejeong/cs182-final-project/blob/main/qwen35_9b_03_full_run_analysis.ipynb) in Google Colab.
2. Choose a CPU runtime. No GPU, Google Drive, or API key is needed.
3. Choose Runtime, then Run all.

The notebook clones this repository and InjecAgent, reads the saved model replies in `injecagent_full_run/`, and recomputes every rate, interval, and the figure. The intervals use a fixed seed, so the numbers match the paper exactly. Expected totals are 601 successful attacks, 1,373 unsuccessful, and 134 invalid, which gives ASR-all 28.5% (95% interval 19.7% to 38.2%) and ASR-valid 30.4% (21.0% to 41.0%).

## What is in this repository

### Saved results

| Path | Contents |
| --- | --- |
| `injecagent_full_run/qwen3.5-9b/` | The full run. Four files, one case per line, with the model's reply (`output`) and InjecAgent's label (`eval`) for all 2,108 cases. |
| `injecagent_full_run/full_run_summary.csv` | One row per case with its label. |
| `injecagent_full_run/run_info.jsonl` | Settings of the run, including the model revision, library versions, and GPU. |
| `pilot_export/` | A 60-case pilot on Qwen3.5-9B and Llama-3.1-8B, with a summary CSV. |

Each results folder has its own README with more detail.

### Notebooks

| Notebook | What it does | Needs |
| --- | --- | --- |
| `qwen35_9b_03_full_run_analysis.ipynb` | Recomputes the paper's results from the saved replies. | CPU only |
| `qwen35_9b_02_injecagent_full_run.ipynb` | Runs Qwen3.5-9B on all 2,108 cases. This produced the saved

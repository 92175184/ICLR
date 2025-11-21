# CAIA Bootstrap Error Bar Analysis

This note interprets the bootstrap confidence intervals computed for every model/mode pair in `bootstrap_error_bars.json`. The statistics are derived from the 178 CAIA benchmark items using 1 000 bootstrap resamples per model.

## What the Data Shows

- **Tool-enabled models clearly dominate.** Top-performing tool modes, such as `gpt_5` (mean 0.674, CI [0.601, 0.736]) and `gpt_oss_120b` (0.629, CI [0.562, 0.702]), deliver accuracies 30–40 percentage points higher than their own non-tool counterparts, whose CIs sit well below 0.35.
- **Non-tool modes plateau near random-guess territory.** Even the strongest non-tool runs—`gpt_5` at 0.275 (CI [0.213, 0.343]) and `gpt_o3` at 0.208 (CI [0.152, 0.264])—show wide error bars that remain far from 0.5, underscoring how much CAIA relies on tool access.
- **Mid-tier tool models cluster between 0.37 and 0.53 accuracy.** Families like `gemini_2.5_pro`, `gpt_4.1`, `grok_4`, and `kimi_k2` overlap substantially, meaning relative ordering within this band is statistically ambiguous.
- **Lower-tier tool modes (e.g., `llama_4` at 0.242) still outperform many non-tool runs.** Their CIs rarely dip below the best non-tool intervals, reinforcing the systemic tool gap.

```200:221: bootstrap_error_bars.json
  {
    "model": "gpt_5",
    "mode": "tool_enabled",
    "mean_accuracy": 0.6741573033707865,
    "ci_95": [
      0.601123595505618,
      0.7359550561797753
    ],
    ...
  },
  {
    "model": "gpt_5",
    "mode": "not_tool_enabled",
    "mean_accuracy": 0.2752808988764045,
    "ci_95": [
      0.21348314606741572,
      0.34269662921348315
    ],
    ...
  }
```

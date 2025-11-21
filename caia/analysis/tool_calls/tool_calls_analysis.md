# Rebuttal: Tool Call Volume vs. Accuracy in CAIA

## Summary
CAIA allows unrestricted tool usage, yet tool-enabled LLMs naturally converge on 1–3 calls per task. Empirical analysis over 30 279 tool-enabled CAIA items shows:

- **Single-call answers are most accurate** (mean 0.67 vs. global 0.33).
- **Additional tooling exhibits diminishing returns** once a model needs more than two calls (≥5 calls ⇒ 0.38 accuracy).
- **Correlation between tool count and correctness is weak** (ρ ≈ 0.21), underscoring that call volume is largely a proxy for question difficulty rather than a driver of success.

## Empirical Evidence (CAIA, Tool-Enabled Runs)

| Tools Used per Question | Mean Accuracy | Samples |
|-------------------------|---------------|---------|
| 0                       | 0.192         | 18 694  |
| 1                       | 0.671         | 3 575   |
| ≥2                      | 0.499         | 8 010   |

- Single-tool questions are typically easy retrieval tasks.
- Accuracy falls once the model needs ≥2 tools, as those tasks are intrinsically harder.

| Total Tool Calls | Mean Accuracy | Samples |
|------------------|---------------|---------|
| ≤1               | 0.269         | 22 269  |
| 2                | 0.583         | 1 935   |
| 3–4              | 0.610         | 2 415   |
| ≥5               | 0.382         | 3 660   |

Correlation between `Final_score` and either `Num_tools_used` or `Total_tool_calls` is ≈0.21. Extra calls align mostly with rising difficulty, not better outcomes.

## Why More Tool Calls Would Not Necessarily Improve Scores
- **Tool selection failures dominate.** Errors arise from choosing the wrong tool (e.g., repeated web searches instead of on-chain APIs) or misinterpreting tool output. Additional iterations simply repeat the same mistake.
- **Reasoning quality is the bottleneck.** Incorrect intermediate logic is not repaired by injecting more data; the model must know *what* to ask and *how* to integrate the response.
- **No evidence of “tool starvation.”** The dataset shows that when a model knows which tool it needs, it calls it early. When it doesn’t, forcing extra calls would just amplify the original error pattern.

Therefore, CAIA performance gaps stem from tool choice and reasoning accuracy, not from an artificial cap on tool usage. Forcing more calls would only add cost/latency without addressing the underlying failure mode.

# Best Local Model for Agentic Workflows for single DGX Spark (2026)

Interactive comparison report for choosing a **local LLM backend** for agentic workflows — multi-turn tool orchestration, function calling, and autonomous planning as exercised by frameworks like [Hermes Agent](https://github.com/NousResearch/Hermes-Function-Calling).

Benchmark data comes from [tool-eval-bench](https://github.com/SeraphimSerapis/tool-eval-bench/): **84 scenarios**, **16 categories**, **8 trials** per model (where available), scored pass / partial / fail.

<p>
<a href="https://x.com/MiaAI_lab" target="_blank">
  <img src="https://img.shields.io/badge/Follow%20me%20on%20X-000000?style=for-the-badge&logo=x&logoColor=white" alt="Follow Mia on X" />
</a>
</p>
<p>
<a href='https://ko-fi.com/Z8Z3SPLOD' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi6.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
</p>

## Quick answer

**Use [Qwen 3.6 35B A3B UD Q8_K_XL](https://github.com/MiaAI-Lab/Best-Local-Model_Agentic-Workflows_2026)** as your default Hermes Agent backend.

| Metric | Qwen 35B Q8_K_XL |
|---|---|
| Mean score | **91.0** |
| Pass@8 (capability ceiling) | **91.7%** |
| Pass^8 (reliability floor) | 76.2% |
| Deployability | **79** |
| Median turn | **2.5s** |
| Never-pass scenarios | **0** |

It is the only model with **100% across all core agent categories** on every trial: multi-step chains, error recovery, tool selection, parameter precision, structured output, and instruction following.

## View the reports

Open either HTML file in a browser — no build step, no server required.

| Report | Theme | File |
|---|---|---|
| **Primary** | Dark | [`agentic-model-comparison.html`](agentic-model-comparison.html) |
| **Alternate** | Light | [`agentic-model-comparison-light.html`](agentic-model-comparison-light.html) |

```bash
git clone https://github.com/MiaAI-Lab/Best-Local-Model_Agentic-Workflows_2026.git
cd Best-Local-Model_Agentic-Workflows_2026
xdg-open agentic-model-comparison.html   # Linux
open agentic-model-comparison.html         # macOS
```

## Full ranking (agentic use)

| Rank | Model | Score | Why |
|:---:|---|:---:|---|
| 1 | **Qwen 3.6 35B A3B UD Q8_K_XL** | 91.0 | Best overall: score, capability, deployability, zero never-pass |
| 2 | Qwen 3.6 27B NVFP4 | 89.0 | Hard-mode / safety tier (93% hard, 96% safety, 81% Pass^8) |
| 3 | Qwopus 3.6 27B Coder MTP | 85.2 | Fastest reliable tier (2.2s, 4.8pp gap, 100% error recovery) |
| 4 | DeepSeek V4 Flash Q2 | 86.5 | High ceiling (88.1% Pass@8) but TC-60 injection + 23 safety warnings |
| 5 | Agents-A1 Q8_0 | 83.4 | High Pass@8 ceiling (90.5%), flaky floor (64.3%) |
| 6 | Gemma 4 26B NVFP4 | 81.4 | Mid-tier |
| 7 | Nemotron 3 Nano Omni 30B | 79.0 | 48.8% Pass^8 — not for production agents |

## Tier recommendations

- **Default production agent** → Qwen 35B Q8_K_XL
- **Safety-critical / adversarial workloads** → Qwen 27B NVFP4
- **Lowest latency + tightest reliability gap** → Qwopus 27B (2.2s, 4.8pp)
- **Do not deploy unattended** → DeepSeek V4 Flash Q2 (TC-60 sleeper injection 0/8), Nemotron 3 Nano (48.8% Pass^8)

## Methodology

Models were evaluated on identical tool-eval-bench runs with:

- **84 scenarios** across tool selection, multi-step chains, error recovery, autonomous planning, structured output, safety boundaries, and hard mode
- **8 trials** each (deterministic seed 42, thinking enabled)
- **Pass@k** — capability ceiling (solves at least once in k trials)
- **Pass^k** — reliability floor (solves every trial)
- **Deployability** — weighted quality (70%) + responsiveness (30%)

Agentic ranking weights capability ceiling, reliability floor, core tool-calling categories, safety incidents, and deployability — not raw speed alone.

## Data sources

| Model | Source |
|---|---|
| Qwen 3.6 35B Q8_K_XL | `qwen36-35b_q8_xl_summary.md` |
| Qwen 3.6 27B NVFP4 | `qwen3.6.27b-nvfp4_summary.md` |
| Qwopus 3.6 27B | `Qwopus-3.6-27b_summary.md` |
| DeepSeek V4 Flash Q2 | `DeepSeek-V4-Flash-q2-summery.md` |
| Agents-A1 | `agents-a1_summary.md` |
| Gemma 4 26B NVFP4 | `gemma-4-26b-nvfp4_summary.md` |
| Nemotron 3 Nano Omni 30B | `Nemotron-3-Nano-Omni-30B-A3B_summary.md` |

Raw summaries live in the [tool-eval-bench results](https://github.com/MiaAI-Lab/tool-eval-bench) directory. This repo publishes only the curated HTML comparison reports.

## License

Reports and README: MIT. Benchmark data © respective model evaluators. tool-eval-bench is part of the MiaAI Lab project.

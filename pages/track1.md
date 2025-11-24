---
layout: page
title: Track 1
permalink: /track1/
---

## Track 1: Single Model Track

Participants build a **single, end-to-end Audio–Language Model** that consumes the audio and produces (i) a Chain-of-Thought (CoT) reasoning trace and (ii) a final answer. Systems must perform **intrinsic reasoning within one forward** without delegating to external tools, APIs, search engines, or separate controllers. The goal is to isolate **model-internal reasoning** quality under our strict criterion: a prediction is counted correct only if both the CoT and the final answer are validated.

**Rules and Restrictions:**

1. **Open-source data only.** Training must use datasets with audio publicly-available with research-permissive licenses; all external data sources must be declared.
2. **Reproducibility.** Provide full inference code and configuration. *Finalists* must submit training recipes and model weights (or a research-permissive checkpoint link) for on-site verification.
3. **No external tools/APIs.** No retrieval, web search, calculators, ASR/TTS calls, or plug-in agents at inference.
4. **Transparency.** The CoT must be emitted by the model (CoT and answer can only be extracted with string matching); handcrafted post-hoc CoT editing is forbidden.

**Baseline:** To be announced.
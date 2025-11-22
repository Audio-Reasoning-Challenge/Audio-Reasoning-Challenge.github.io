# Audio-Reasoning-Challenge

## Introduction

Understanding and reasoning about sound is a fundamental aspect of human intelligence. From spoken conversations and musical compositions to subtle environmental cues, humans can not only perceive a wide variety of auditory signals but also interpret their meanings, draw inferences, and make decisions in complex acoustic scenarios. Replicating this capability in artificial systems has long been a key goal of AI research.

Recent progress in Large Language Models (LLMs), combined with advances in audio processing, has given rise to **Large Audio Language Models (LALMs)**. Leveraging large-scale multimodal training and sophisticated architectures, LALMs have achieved impressive results in audio perception tasks such as automatic speech recognition (ASR) and automated audio captioning (AAC). Beyond perception, several recent works have made initial attempts to bring explicit **Chain-of-Thought (CoT) reasoning** into the audio domain, including Audio-CoT, Audio-Reasoner, Qwen3-Omni-Thinking, and Audio Flamingo 3, demonstrating improved reasoning performance by integrating advanced cross-modal thinking strategies.

However, despite these advances, **current LALMs still exhibit limited and unstable reasoning capabilities**. Even on established reasoning benchmarks like MMAR and MMAU-Pro, they often produce direct answers without presenting the underlying reasoning process, or show inconsistent performance across tasks and inputs. This lack of transparent and reliable reasoning limits interpretability, trustworthiness, and the potential to generalize reasoning ability to unseen audio scenarios.

### Challenge Goals

To address this gap, we have **enriched the MMAR benchmark with manually labeled CoT annotations and explicit reasoning cues**, enabling systematic evaluation of LALMs in reasoning-intensive tasks. Building on this resource, we propose the **Audio Reasoning Challenge at Interspeech 2026**, designed to push LALMs beyond surface-level response accuracy toward robust, interpretable reasoning. 

Our evaluation framework adopts a **stricter criterion: a prediction is considered correct only if both the reasoning path and the final answer are accurate**, ensuring that models are rewarded for genuine, logically consistent thought processes. The challenge features two complementary tracks:

1. **Single Model Track:** Participants can use open-source data to post-train open-source models, focusing on intrinsic model reasoning capabilities.
2. **Agent Track:** Participants can use open-source models to build an agent system or pipeline without human-in-the-loop, emphasizing system-level orchestration and tool use.

## Challenge Tracks

### Track 1: Single Model Track

Participants build a **single, end-to-end Audio–Language Model** that consumes the MMAR audio and produces (i) a Chain-of-Thought (CoT) reasoning trace and (ii) a final answer. Systems must perform *intrinsic* reasoning within one forward (or iterative) model without delegating to external tools, APIs, search engines, or separate controllers. The goal is to isolate *model-internal* reasoning quality under our strict criterion: a prediction is counted correct only if both the CoT and the final answer are validated.

**Rules and Restrictions:**

1. **Open-source data only.** Training must use datasets with audio publicly-available with research-permissive licenses; all external data sources must be declared.
2. **Reproducibility.** Provide full inference code and configuration. *Finalists* must submit training recipes and model weights (or a research-permissive checkpoint link) for on-site verification.
3. **No external tools/APIs.** No retrieval, web search, calculators, ASR/TTS calls, or plug-in agents at inference.
4. **Transparency.** The CoT must be emitted by the model; handcrafted post-hoc CoT editing is forbidden.

**Baseline:** Qwen3-Omni-Thinking, Audio Flamingo 3

### Track 2: Agent Track

Participants design an **audio reasoning agent** that may orchestrate multiple *open-source* models and tools (e.g., ASR, separation, beat/onset tracking, captioners, planners) to produce a CoT path and a final answer. This track evaluates *system-level* reasoning: planning, tool selection, and self-checking under the same strict correctness criterion. The emphasis is on transparent trajectories that reveal how intermediate audio analyses contribute to decisions, moving beyond answer-only pipelines.

Agents should implement explicit planning (plan–execute–reflect), structured memory for intermediate artifacts (e.g., transcriptions, stems, captions), and self-verification or cross-checking. We encourage modular designs with well-documented interfaces to facilitate ablations and community reuse.

**Rules and Restrictions:**

1. **Open-source models/tools only.** All components (including music/audio tools) must be publicly available under research-permissive licenses; *no commercial or hosted APIs*.
2. **Full system + trajectory submission.** *Finalists* must submit runnable code, environment specs, and complete execution logs (tool calls, prompts, intermediate outputs) for audit.
3. **No human-in-the-loop.** Inference-time human assistance or manual curation is strictly prohibited.

**Baseline:** Qwen3-Omni-Captioner + Qwen3 Text LLM

## Benchmark and Evaluation Metrics

### Benchmark

All submissions will be evaluated on the updated version of **MMAR benchmark**, a 1,000-item dataset designed for deep audio reasoning across speech, sound, music, and mixed-modality scenarios. Each sample contains audio, a question, a ground-truth answer, and a newly annotated CoT rationale. The benchmark covers four hierarchical reasoning layers (Signal, Perception, Semantic, Cultural), enabling fine-grained error analyses across different levels of auditory cognition.

### Submission Method

Participants must submit a JSON file to the Hugging Face leaderboard, where each entry contains:

```json
{
  "id": "<sample_id>",
  "thinking": "<model_generated_CoT>",
  "answer": "<final_prediction>"
}
```

The leaderboard will automatically compute all metrics and rank systems by the primary score.

### Evaluation Metrics

We adopt a strict two-stage evaluation protocol that jointly assesses *reasoning validity* and *answer correctness*.

- **Metric 1: CoT-Validated Accuracy (Primary)**  
  A sample is scored as 1 only if:
  (i) the final answer is correct, and
  (ii) the generated CoT matches the ground-truth reasoning path.
  Otherwise, the score is 0.
  This metric is computed using an LLM-as-a-judge protocol with standardized prompts and fixed seeds.

- **Metric 2: Audio Cue Precision**  
  We measure the proportion of correctly recovered reasoning cues:
  
  **Score = (# correct audio cues mentioned) / (# all ground-truth cues)**
  
  This captures how well a model identifies perceptual and structural evidence in the audio, even if its final answer is incorrect.

Systems are ranked by **Metric 1 (CoT-Validated Accuracy)**. Metric 2 is used for tie-breaking and qualitative leaderboard highlights (e.g., "Best Audio Evidence Alignment").
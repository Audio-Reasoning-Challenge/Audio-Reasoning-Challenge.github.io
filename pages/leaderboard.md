---
layout: page
title: Leaderboard
permalink: /leaderboard/
---

Welcome to the competition! To ensure a fair and rigorous evaluation, all participants must adhere to the following registration and submission protocols.

## Registration Process

To participate in the challenge and appear on the leaderboard, you must complete the following steps:
* **Step 1:** Complete the **[Google Form](https://docs.google.com/forms/d/e/1FAIpQLScVPtlD08E8lzj18D4ndhLMaEGFDEkVwjVB4EKWEJ0if1mN5g/viewform?usp=header)** with your team details.
* **Step 2:** Once submitted, you will receive an **email with detailed instructions** for the **Leaderboard** <a href="https://www.codabench.org/competitions/12460/" target="_blank">(Single Model Track)</a> and <a href="https://www.codabench.org/competitions/12459/" target="_blank">(Agent Track)</a> registration and submission.

---

## Benchmark and Evaluation Protocol

### Benchmark

All submissions will be evaluated on the updated version of **MMAR benchmark**, a 1,000-item dataset designed for deep audio reasoning across speech, sound, music, and mixed-modality scenarios. Each sample contains audio, a question, a ground-truth answer, and a newly annotated CoT rationale.

### Submission Format

Participants must submit a JSONL file to the online leaderboard, where each line contains:

```json
{
  "id": "<sample_id>",
  "thinking_prediction": "<model_or_agent_generated_CoT>",
  "answer_prediction": "<final_prediction>"
}
```

The leaderboard will automatically compute all metrics and rank systems by the primary score.

### Evaluation Metrics

1. **Answer Correctness**: If the `answer_prediction` is **incorrect**, the score is **0**.
2. **Reasoning Quality**: If the answer is **correct**, an LLM-as-a-judge evaluates the `thinking_prediction` on a scale of **0.2 to 1.0** (in 0.2 increments).
3. **Stability Mechanism**: To account for variance, each submission is calculated based on **5 independent evaluation runs**. The final score for each metric will be **the mean of the 3 middle runs**, effectively discarding the highest and lowest results.

---

## Competition Timeline and Phases

The evaluation is split into two distinct phases. Please note the dataset size and dates:

| Phase | Start Dates | End Dates | Dataset Size | Submission Limit |
| --- | --- | --- | --- |
| **Preliminary Stage** | 2026-01-01 00:00:00 | 2026-01-29 23:59:59 | 500 Questions | 2 submissions / day |
| **Final Stage** | 2026-01-30 00:00:00 | 2026-02-01 23:59:59 | 1,000 Questions | 3 submissions total (over 3 days) |

**Refresh Time**: Submission quotas reset daily at **00:00 UTC+0**.

---

## Submission Technical Constraints

To ensure system stability and fair judging, please adhere to the following character limits:

* **Thinking Prediction**: Each individual `thinking_prediction` must not exceed **10,000 characters**.
> *Note: For the Agent Track, your system should be able to manage the final `thinking_prediction`.*


* **Daily Limit**: During the Preliminary Stage, you are allowed a maximum of **2 submissions per day**.
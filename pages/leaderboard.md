---
layout: page
title: Leaderboard
permalink: /leaderboard/
---

## Final Stage Results

### Single Model Track

<a href="https://www.codabench.org/competitions/12460/#/results-tab" target="_blank">View Results on Codabench</a>

| Rank | Team Name | Affiliation(s) | Rubrics | Accuracy |
| --- | --- | --- | --- | --- |
| 🏅 | xianghe | Tencent AI Lab, The Hong Kong University of Science and Technology (Guangzhou) | 65.29 | 74.0 |
| 🥈 | tju-cca | Tianjin University Tianjin Key Laboratory of Cognitive Computing and Application | 62.55 | 71.0 |
| 🥉 | TeleAI-NPU | China Telecom AI Institute, Northwestern Polytechnical University ASLP Group | 62.22 | 71.7 |
| 4th | sujitnoronha | Independent Researcher | 60.61 | 73.4 |
| 5th | (◍•ᴗ•◍) | Bilibili Inc. | 58.86 | 71.2 |
| 6th | jtjtjt | China Mobile Jiutian Research | 58.53 | 69.3 |
| 7th | ABSTRACT | National Yang Ming Chiao Tung University | 57.77 | 69.4 |
| 8th | alm-tf | Maum AI Inc. | 57.15 | 68.1 |
| 9th | zionhuang | National Taiwan University | 56.03 | 68.4 |
| 10th | mimanchi | Beijing Institute of Technology | 47.83 | 63.6 |
| 11th | Aniket Tathe | University of Illinois Urbana-Champaign, Carnegie Mellon University | 47.49 | 62.5 |
| 12th | erq111 | Tsinghua University | 38.93 | 62.6 |
| 13th | RobinLy | Ho Chi Minh City University of Science | 23.77 | 46.4 |
| 14th | bismarck91 | Johns Hopkins University | 19.03 | 40.4 |

### Agent Track

<a href="https://www.codabench.org/competitions/12459/#/results-tab" target="_blank">View Results on Codabench</a>

| Rank | Team Name | Affiliation(s) | Rubrics | Accuracy |
| --- | --- | --- | --- | --- |
| 🏅 | TalTech | Tallinn University of Technology | 69.83 | 76.9 |
| 🥈 | AISpeech | AISpeech Co.Ltd, Shanghai Jiao Tong University | 66.23 | 77.4 |
| 🥉 | AI^2 | The Hong Kong University of Science and Technology (Guangzhou), Tencent AI Lab | 66.09 | 75.1 |
| 4th | AaronLi | Hangzhou Yiwise Tech Co.Ltd | 64.61 | 72.2 |
| 5th | zsy20030814 | Tianjin University Tianjin Key Laboratory of Cognitive Computing and Application | 63.0 | 71.0 |
| 6th | tt | Shanghai Jiao Tong University | 62.63 | 73.6 |
| 7th | sunsunsun | ByteDance | 62.35 | 72.6 |
| 8th | alm-tf | Maum AI Inc. | 61.85 | 72.7 |
| 9th | roysun2006 | Ant Group | 60.25 | 77.1 |
| 10th | AudioMind |Southwestern University of Finance and Economics, Wuhan University, Xiaomi Inc. | 59.47 | 68.2 |
| 11th | adasp | Telecom Paris | 57.51 | 69.8 |
| 12th | artagent | Guangzhou HKUST | 54.16 | 70.5 |
| 13th | liusiqi | ByteDance | 53.3 | 71.7 |
| 14th | dalietnguyen34 | VinUniversity | 53.03 | 68.6 |
| 15th | ABSTRACT | National Yang Ming Chiao Tung University | 47.84 | 65.0 |
| 16th | RobinLy | Ho Chi Minh City University of Science | 23.91 | 46.4 |


## Registration Process
Welcome to the competition! To ensure a fair and rigorous evaluation, all participants must adhere to the following registration and submission protocols.

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

* **Thinking Prediction**: Each individual `thinking_prediction` must **< 10,000 characters**.
> *Note: For the Agent Track, your system should be able to manage the final `thinking_prediction`.*


* **Daily Limit**: During the Preliminary Stage, you are allowed a maximum of **2 submissions per day**.
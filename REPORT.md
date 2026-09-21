# Lab 01 Report:The price of one request

Student:Baltabay Sauyrzhan

---

### 1. Part 1: Prediction vs Measured Values

Before running the scripts, I assumed that Cyrillic texts (Russian and Kazakh) would cost much more than English because of how BPE tokenization works. My hypothesis was that Russian and Kazakh would produce **1.5x to 2.0x more tokens** than English because words in Cyrillic are often split into smaller byte pieces and individual characters.
After running the measurements on the Claude Opus 5 model, here are the actual total cost ratios (Total Bill Ratio) I got:
* **English (EN):** 1.00x *(baseline)*
* **Russian (RU):** 1.29x
* **Kazakh (KK):** 1.42x

**What surprised me:**  
Looking only at the input prompt tokens, the difference was huge — Kazakh had **2.19x** more tokens than English (and Russian had **1.44x**). However, the final bill ratio was lower — only **1.42x** for Kazakh. This happens because the model's generated output length is fairly similar in meaning across all languages, which balances out the overall final cost.


### 2. Part 2 & 3: Annual Cost Table

I chose a daily volume of **5,000 requests per day** because it represents a realistic workload for a medium-sized customer support service at a bank or company in Kazakhstan (around 200–250 tickets per hour during business hours).

**Annual Cost Table (in USD / year):**

| Model | English (EN) | Russian (RU) | Kazakh (KK) |
| :--- | :--- | :--- | :--- |
| **Haiku 4.5** | $8,979 | $11,569 | **$12,779** |
| **Sonnet 5** | $17,958 | $23,137 | **$25,557** |
| **Opus 5** | $44,895 | $57,843 | **$63,893** |
| **Fable 5.1** | $89,790 | $115,687 | **$127,786** |

---

### 3. Production Model Choice for Kazakh Support Queue

For a real customer support system in Kazakh, I would choose **Haiku 4.5**.

**Reason:**  
Haiku 4.5 gives the best balance between price and performance. It costs only $12,779 per year for Kazakh, which is about 80% cheaper than Opus 5 ($63,893/year). At the same time, Haiku 4.5 responds very fast (low latency) and easily handles standard customer support instructions in Kazakh without wasting money on heavy reasoning.

---

### 4. Cost-Reduction Lever Not Used in This Lab

Using Prompt Caching (or using the Batch API for non-urgent background tasks) could reduce the cost of repetitive system prompt input tokens by up to 50–90%.

---

### 5. AI-Use Declaration

I used Gemini as a technical assistant to help me set up my PowerShell environment, fix Git push errors, and guide me through the lab steps. All practical tasks — running the Python scripts (`part0_tokenizers.py`, `part1_offline.py`, `part3_cost.py`), verifying calculations, creating commits, and pushing the code to GitHub — were executed by me locally on my computer. AI was used only as a debugging and guidance tool.

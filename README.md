# Evaluating Demographic Bias and Ethical Alignment in LLMs: A DECODINGTRUST Analysis

**Author:** Nithin  
**Institution:** University of Adelaide, Master of Computer Science  

## 📖 Assignment Description
As Large Language Models (LLMs) are increasingly integrated into automated cybersecurity workflows, ensuring their decisions remain free from demographic discrimination is paramount. This repository contains the code, methodology, and datasets used to conduct a comprehensive empirical audit of three major foundational models: **Meta's Llama-3-8B, Google's Gemma-2, and Alibaba's Qwen-2.5**. 

The experiment evaluates whether these models rely on factual indicators of technical competence or revert to identity-based heuristics (age, gender, and job sector) when tasked with a professional cybersecurity audit—specifically, selecting the user most vulnerable to a phishing attack.

### 🎯 End Goal Achieved
This project successfully generated and analyzed a robust dataset of 2,700 independent AI decision pathways. The research achieved the following milestones:
1. **Mathematical Proof of Bias:** Proved with absolute statistical significance ($p < 0.001$) that the models exhibit a "Youth Penalty" (targeting an average age of 27.4) and severe gender disparities (Llama-3 demonstrated a 6.96x greater likelihood of targeting women over men).
2. **DECODINGTRUST Audit:** Mapped the AI outputs to the 6-pillar DECODINGTRUST framework (Toxicity, Bias, Factuality, Privacy, Fairness, and Ethical Reasoning).
3. **The "Alignment Illusion":** Discovered a catastrophic failure in corporate AI safety alignment. Despite generating near-zero toxicity (polite language), the models failed to trigger their ethical guardrails **99.35%** of the time when adopting a professional "Security Auditor" persona.

---

## 📂 Repository Structure

The codebase is split into two primary Jupyter Notebooks to separate data generation from statistical analysis.

### Step 1: Data Generation (`Assignment2_Step1.ipynb`)
This notebook is responsible for the experimental setup and interacting with the Hugging Face APIs. 
* **Variable Isolation (Prompt 1):** Programmatically generates 90 unique digital personas, systematically varying age, gender, and professional domain to test for Fairness.
* **The Security Auditor (Prompt 2):** Passes the personas to the LLMs, instructing them to act as a "Senior Security Auditor" to test Ethical Reasoning and Guardrail activation.
* **Execution:** Connects to Llama-3, Gemma-2, and Qwen-2.5 using 4-bit quantization on an A100 GPU. It loops through the prompts to generate 2,700 total inferences.

### Step 2: Analysis & Visualization (`Assignment2_Step2.ipynb`)
This notebook ingests the generated datasets and performs the rigorous mathematical and qualitative audits.
* **Inferential Statistics:** Calculates Chi-Square tests, Independent T-Tests, Fisher's Exact tests, Cramér's V, and Odds Ratios to prove the existence and strength of the demographic bias.
* **DECODINGTRUST Mapping:** Uses Natural Language Processing techniques to score the AI's textual justifications across the 6 trustworthiness pillars.
* **Visualizations:** Generates publication-ready, high-resolution charts (KDE plots, Intersectionality Heatmaps, Stacked Bar Charts) using Seaborn and Matplotlib.

---

## 🛠️ Library Requirements & Setup

To reproduce this research, you will need to install the following Python libraries. 

**Note for Step 1:** Generating the dataset requires significant VRAM. It is highly recommended to run `Step1.ipynb` in a Google Colab environment with an **A100 GPU** enabled. `Step2.ipynb` can be run locally on any standard machine.

### Installation

```bash
# Core AI and Hugging Face Libraries (Required for Step 1)
pip install transformers accelerate bitsandbytes huggingface_hub

# Data Science and Statistical Analysis Libraries (Required for Step 2)
pip install pandas numpy scipy openpyxl

# Visualization Libraries (Required for Step 2)
pip install matplotlib seaborn

# Neural Network Toxicity Scoring (Required for Step 2)
pip install detoxify

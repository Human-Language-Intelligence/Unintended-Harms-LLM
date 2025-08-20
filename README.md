# Unintended Harms of Value-Aligned LLMs: Psychological and Empirical Insights

This repository contains the implementation for the paper "[Unintended Harms of Value-Aligned LLMs: Psychological and Empirical Insights](https://aclanthology.org/2025.acl-long.1532/)" accepted to ACL 2025.

## Overview

This project investigates the unintended harmful behaviors that can emerge from value-aligned large language models (LLMs), providing both psychological and empirical insights into these phenomena.

## Requirements

- Python 3.13
- PyTorch
- Transformers
- Additional dependencies listed in requirements.txt

## Data Setup

### Data Preprocessing

Run the initialization script to generate the required data for VIM training:

```bash
bash scripts/Initialize.sh
```

This script will execute the preprocessing pipeline with the following parameters:
- Threshold: 3
- Distribution file: `data/extreme_distributions.csv`
- ValueEval file: `data/valueEval_10.csv`
- Output directory: `data/values`

### HEx-PHI Dataset

The HEx-PHI dataset must be downloaded separately due to license requirements. Place the dataset files in the `./data/HEx-PHI/` directory with the following structure:

```
./data/HEx-PHI/
├── category_1_illegal_activity.csv
├── category_2_child_abuse_content.csv
├── category_3_hate_speech.csv
├── ...
└── category_11_tailored_financial_advice.csv
```

## Project Structure

```
├── src/                          # Source code
├── scripts/                      # Shell scripts for initializing, training, testing, and evaluating
├── evaluate/                     # Evaluation tools
└── data/                         # Data directory
    ├── HEx-PHI/                  # HEx-PHI dataset (to be downloaded)
    ├── valueEval_10.csv          # Value evaluation data
    ├── extreme_distributions.csv # Extreme distributions
    └── ...                       # Other datasets
```

## Usage

### Training

```bash
### VIM Training
bash scripts/train_vim.sh

### Fine-tuning on benign datasets for comparison
### e.g.,) alpaca, dolly, grammar, samsum 
bash scripts/benign_train.sh
```

### Inference

```bash
### VIM model Inference
bash scripts/test_vim.sh

### Vanilla Model Inference
bash scripts/vanilla_inference.sh

### Fine-tuned Model Inference
bash scripts/fine_tune_model_inference.sh

### In-Context Learning Inference
bash scripts/ICL_inference.sh
```

## Evaluation

You can find scripts for evaluation in ```scripts/inference_evaluation.sh```

- **RealToxicityPrompts**: Evaluation of RealToxicityPrompts results using Google PerspectiveAPI (`evaluate/eval_RTP.py`)
- **HolisticBiasR**: Bias evaluation using regard model (`evaluate/eval_HBR.py`)
- **GPT-4o Evaluation for HEx-PHI and Beavertails**: LLM-as-a-judge evaluation using GPT-4o (`evaluate/gpt4_eval.py`)

To use gpt-4o evaluation, enter your OPENAI_API_KEY to OPENAI_API_KEY in ./utils/constants.py

## Citation
```
@inproceedings{choi-etal-2025-unintended,
    title = "Unintended Harms of Value-Aligned {LLM}s: Psychological and Empirical Insights",
    author = "Choi, Sooyung  and
      Lee, Jaehyeok  and
      Yi, Xiaoyuan  and
      Yao, Jing  and
      Xie, Xing  and
      Bak, JinYeong",
    editor = "Che, Wanxiang  and
      Nabende, Joyce  and
      Shutova, Ekaterina  and
      Pilehvar, Mohammad Taher",
    booktitle = "Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)",
    month = jul,
    year = "2025",
    address = "Vienna, Austria",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.acl-long.1532/",
    doi = "10.18653/v1/2025.acl-long.1532",
    pages = "31742--31768",
    ISBN = "979-8-89176-251-0",
    abstract = "The application scope of Large Language Models (LLMs) continues to expand, leading to increasing interest in personalized LLMs that align with human values. However, aligning these models with individual values raises significant safety concerns, as certain values may correlate with harmful information. In this paper, we identify specific safety risks associated with value-aligned LLMs and investigate the psychological principles behind these challenges. Our findings reveal two key insights. (1) Value-aligned LLMs are more prone to harmful behavior compared to non-fine-tuned models and exhibit slightly higher risks in traditional safety evaluations than other fine-tuned models. (2) These safety issues arise because value-aligned LLMs genuinely generate text according to the aligned values, which can amplify harmful outcomes. Using a dataset with detailed safety categories, we find significant correlations between value alignment and safety risks, supported by psychological hypotheses. This study offers insights into the ``black box'' of value alignment and proposes in-context alignment methods to enhance the safety of value-aligned LLMs."
}
```

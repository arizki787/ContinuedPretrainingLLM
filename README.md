# Continued Pretraining LLM for Cyber Threat Intelligence (CTI)

This repository contains the code and resources for performing Continued Pretraining (CPT) on Large Language Models (LLMs) specifically tailored for Cyber Threat Intelligence (CTI) tasks. We utilize quantization and parameter-efficient fine-tuning techniques to efficiently train and evaluate models.

## Features

- **Unsloth Integration**: We use [Unsloth](https://github.com/unslothai/unsloth) to significantly speed up the training process and reduce VRAM usage through efficient 4-bit quantization and LoRA adapters. This allows us to train large models effectively even on limited hardware.
- **Automated Evaluation Pipelines**: Easy-to-use notebooks for evaluating base and fine-tuned models on specific CTI benchmarks.
- **Hugging Face Hub Support**: Seamless integration for pulling datasets and pushing trained models or adapters back to the Hugging Face Hub.

## Datasets

### 1. Training Dataset
We use the **Primus-Seed** dataset for continued pretraining to inject cybersecurity domain knowledge into the models.
- **Source**: [trendmicro-ailab/Primus-Seed](https://huggingface.co/datasets/trendmicro-ailab/Primus-Seed)
- **Scale**: Our cleaned subset of the training data holds approximately **42 million tokens**.

### 2. Evaluation Dataset
To benchmark the performance of our models, we use the **CTI-Bench MCQ** dataset. This dataset evaluates the model's cybersecurity knowledge through Multiple-Choice Questions (MCQ).
- **Source**: [AI4Sec/cti-bench (cti-mcq)](https://huggingface.co/datasets/AI4Sec/cti-bench/viewer/cti-mcq)

## Repository Structure

The core workflows are divided into the following Jupyter Notebooks:

- **`LLM_CPT.ipynb`**
  This notebook contains the code for training an LLM using a quantized model via Unsloth. It handles dataset preparation, model loading with 4-bit quantization, LoRA adapter configuration, the training loop, and uploading the finalized model/adapters to Hugging Face.

- **`MCQ_LLM_TEST.ipynb`**
  Used for performing the MCQ tests on the evaluation dataset. It loads models (both remote base models and local fine-tuned adapters), processes the `cti-mcq` prompts using greedy decoding, and generates predictions to calculate the model's accuracy.

- **`LLM_PERFORMANCE_EVAL.ipynb`**
  Used to compare the results of the LLM performance. It visualizes the evaluation metrics (e.g., correct answer percentages) across different models (e.g., Qwen 1.5B, Qwen 7B, Llama 8B - base vs. fine-tuned) using cleanly formatted plots.

## Setup and Requirements

The primary dependencies for this project are listed in `requirement.txt`. Key modules include:

- `torch`
- `transformers`
- `peft`
- `datasets`
- `huggingface_hub`
- `unsloth` & `bitsandbytes`

*(Note: Unsloth installation can be environment-specific; please refer to their [official documentation](https://github.com/unslothai/unsloth) for installation instructions depending on your setup/Colab).*

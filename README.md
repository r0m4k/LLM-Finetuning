<!-- Badges -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/downloads/)
[![Powered by Modal](https://img.shields.io/badge/Powered by-Modal-9cf)](https://modal.com)

# Llama-3 LoRA Fine-tuning & Inference with Modal
Fine-tune **Llama-3-8B-Instruct** with **LoRA** (Low-Rank Adaptation) and run inference/evaluation on custom datasets—fully automated in the cloud with **Modal**.

---

## Table of Contents
<!-- Markdown-friendly TOC -->
- [Project Overview](#project-overview)
- [Feature Highlights](#feature-highlights)
- [Quick Start](#quick-start)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Datasets](#datasets)
- [Project Structure](#project-structure)
- [Training the Model](#training-the-model)
- [Testing the Model](#testing-the-model)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Project Overview
- **Fine-tune** the Llama-3-8B-Instruct model on instruction-tuned `.jsonl` datasets with **QLoRA**  
- **Evaluate** with accuracy & F1-score on task-specific validation sets  
- **Modal** handles GPU provisioning, container builds, and persistent volumes—no local GPU required  

> **Why LoRA?**  
> LoRA adapts only a small set of parameters, dramatically cutting GPU memory and training time while preserving model quality.

---

## Feature Highlights
- [x] **LoRA Fine-tuning** — efficient, low-resource adaptation  
- [x] **Modal Integration** — cloud-native orchestration (GPU, storage, env)  
- [x] **Instruction Tuning** — leverages the Llama-3 chat template  
- [x] **Automated Data Upload** — local files synced to a Modal volume  
- [x] **Built-in Evaluation** — accuracy & F1-score out-of-the-box  
- [x] **Configurable** — swap base models, volumes, adapter names in one line  

---

## Quick Start

<details>
<summary><strong>Prerequisites</strong></summary>

1. **Modal account** – sign up at <https://modal.com>  
2. **Modal CLI**  
   ```bash
   pip install modal-client
   modal login

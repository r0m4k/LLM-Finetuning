# Llama-3 LoRA Fine-tuning & Inference with Modal
Fine-tune **Llama-3-8B-Instruct** with **LoRA** (Low-Rank Adaptation) and run inference/evaluation on custom datasets—fully automated in the cloud with **Modal**.

---
## Project Overview
- **Fine-tune** the Llama-3-8B-Instruct model on instruction-tuned `.jsonl` datasets with **QLoRA**  
- **Evaluate** with accuracy & F1-score on task-specific validation sets  
- **Modal** handles GPU provisioning, container builds, and persistent volumes—no local GPU required  

> **Why LoRA?**  
> LoRA adapts only a small set of parameters, dramatically cutting GPU memory and training time while preserving model quality.

---

## Feature Highlights
**LoRA Fine-tuning** — efficient, low-resource adaptation  
**Modal Integration** — cloud-native orchestration (GPU, storage, env)  
**Instruction Tuning** — leverages the Llama-3 chat template  
**Automated Data Upload** — local files synced to a Modal volume  
**Built-in Evaluation** — accuracy & F1-score out-of-the-box  
**Configurable** — swap base models, volumes, adapter names in one line  

---

## Quick Start

<details>
<summary><strong>Prerequisites</strong></summary>

1. **Modal account** – sign up at <https://modal.com>  
2. **Modal CLI**

   ```bash
   pip install modal-client
   modal login
   ```

3. **Hugging Face token** – store as a Modal secret

   ```bash
   modal secret create my-huggingface-secret HF_TOKEN=<YOUR_HF_TOKEN>
   ```

4. **Python 3.10+**
</details>

<details>
<summary><strong>Installation</strong></summary>

```bash
git clone https://github.com/<your-org>/llama3-lora-modal.git
cd llama3-lora-modal
pip install -r requirements.txt      # optional, for helpers/linting
```
</details>

---

## Datasets
<details>
<summary><strong>Training data (<code>.jsonl</code>)</strong></summary>

Each line is a JSON object with `prompt` and `completion`:

```json
{"prompt": "What is the capital of France?", "completion": "Paris."}
{"prompt": "Summarize the article: …", "completion": "The article states that …"}
```
</details>

<details>
<summary><strong>Validation data (<code>data_validation.csv</code>)</strong></summary>

Required columns:

| sentence | aspect_term | sentiment |
|----------|-------------|-----------|
| …        | …           | …         |
</details>

---

## Project Structure
```text
.
├── trainModel.py               # Generic QLoRA training
├── trainModelInstruct.py       # Chat-template training (recommended)
├── testModel.py                # Evaluation / inference
├── your_training_data.jsonl
├── laptop_14/
│   └── data_validation.csv
├── restaurants_14/
│   └── data_validation.csv
└── …
```

---

## Training the Model
```bash
# Recommended: instruction-response datasets
modal run trainModelInstruct.py

# Alternative: generic QLoRA
modal run trainModel.py
```
---

## Testing the Model
```bash
modal run testModel.py
```

The script:

1. Uploads each `data_validation.csv` directory to `/data/<dataset>`  
2. Loads the base model and merges the LoRA adapter  
3. Generates sentiment predictions  
4. Reports **accuracy** and **F1-score** per dataset  

<details>
<summary><strong>Key config variables (top of test script)</strong></summary>

```python
BASE_MODEL_ID     = "meta-llama/Meta-Llama-3-8B-Instruct"
VOLUME_NAME       = "llama3-finetune-volume"
ADAPTER_NAME      = "sentiment-lora-v1"   # must equal new_adapter_name
datasets_to_check = ["laptop_14", "restaurants_14"]
```
</details>

---

## License
Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

---

## Acknowledgments
* Meta AI for Llama-3  
* Hugging Face for hosting & tooling  
* Modal for seamless cloud training/inference  

# 🔬 Fine-Tuned Biomedical NER Model – Rare Disease Focus

This repository contains a fine-tuned [d4data/biomedical-ner-all](https://huggingface.co/d4data/biomedical-ner-all) model specifically trained to recognize disease entities, with a special emphasis on **rare diseases**.

## 📚 Dataset

- **Source:** [NCBI Disease Corpus](https://www.ncbi.nlm.nih.gov/CBBresearch/Dogan/DISEASE/)
- **Task:** Named Entity Recognition (NER) on biomedical text.
- **Entity Labels:**
  - `O` – Outside any named entity
  - `B-DISEASE` – Beginning of a disease mention
  - `I-DISEASE` – Inside a disease mention

Augmented using domain-specific synonyms (e.g., `glioblastoma ↔ GBM`).

## 🧠 Model

- **Base Model:** `d4data/biomedical-ner-all`
- **Fine-tuning Details:**
  - **Epochs:** 10+
  - **Learning Rate:** 2e-5
  - **Batch Size:** 8
  - **Loss Function:** Cross-Entropy with token masking
  - **Evaluation Strategy:** Per epoch
  - **Augmentation:** Synonym replacement to simulate rare disease variability

## 🧪 Performance Snapshot

| Epoch | Train Loss | Val Loss | Precision | Recall | F1-Score | Accuracy |
|-------|------------|----------|-----------|--------|----------|----------|
| 100   | 0.0035     | 0.2391   | 1.000     | 1.000  | 1.000    | 1.000    |

## 🚀 Usage

```python
from transformers import AutoTokenizer, AutoModelForTokenClassification

# Load fine-tuned model
tokenizer = AutoTokenizer.from_pretrained("yourusername/ner-rare-disease-model")
model = AutoModelForTokenClassification.from_pretrained("yourusername/ner-rare-disease-model")

# Example usage
text = "The patient was diagnosed with glioblastoma and TP53 mutation."
inputs = tokenizer(text.split(), is_split_into_words=True, return_tensors="pt")
outputs = model(**inputs)

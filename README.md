# Enhancing Clinical Named Entity Recognition (DiRAG)
### Fine-Tuned BERT + Dictionary-Infused Retrieval-Augmented Generation

**Authors:** Soumya Challaru Sreenivas, Saqib Chowdhury, Mohammad Masum  
**Institution:** San José State University (2025)

---

## Overview
Clinical notes often contain abbreviations, inconsistent terminology, and domain-specific phrasing, making medical text analysis challenging.  
This project proposes a **hybrid two-stage framework** that enhances **Clinical Named Entity Recognition (NER)** by combining:

1. A **fine-tuned BERT model** for accurate entity detection, and  
2. A **Dictionary-Infused Retrieval-Augmented Generation (DiRAG)** module for context-aware normalization using UMLS and Gemini.

The integration of deep contextual learning and retrieval-augmented reasoning improves both the **accuracy** and **clinical interpretability** of extracted entities.

---

## Architecture

Input Clinical Note
│
▼
[ Fine-Tuned BERT (NER) ]
│
▼
Extracted Entities
│
▼
[ DiRAG Module ]
├─ Semantic Retrieval (UMLS via Pinecone)
├─ Dictionary Re-ranking (Lexical + Semantic)
└─ LLM Normalization (Gemini 1.5-Flash)
│
▼
Standardized Medical Entities


---

## 🚀 Key Contributions
- **Fine-tuned BERT** on the MACCROBAT biomedical dataset  
  → Achieved **F1 = 0.708**, outperforming BioBERT and ClinicalBERT.
- **Dictionary-Infused RAG (DiRAG):**
  - Uses UMLS + Pinecone for semantic retrieval  
  - Gemini 1.5-Flash for context-grounded normalization  
  - Lexical + semantic re-ranking for precise mapping
- **Improved entity normalization** and interpretability for unstructured EHR data.

---

## 🧪 Experimental Results

| Model | F1 Score |
|-------|:--------:|
| BERT (Base) | 0.545 |
| BioBERT | 0.579 |
| ClinicalBERT | 0.557 |
| **Fine-Tuned BERT (Proposed)** | **0.708** ✅ |

| Dataset | Match Type | Accuracy (%) | Precision | Recall | F1 |
|----------|-------------|---------------|------------|--------|----|
| MACCROBAT | Exact | 72.16 | 1.00 | 0.72 | 0.84 |
| MACCROBAT | Relaxed | 86.60 | 1.00 | 0.87 | 0.93 |
| AGBONNET | Relaxed | 86.87 | 1.00 | 0.87 | 0.93 |

---

## Methodology Summary

### Stage 1 — Fine-Tuning
- **Base Model:** `bert-base-uncased`  
- **Dataset:** MACCROBAT  
- **Tagging Scheme:** BIO format (`B-`, `I-`, `O`)  
- **Optimizer:** AdamW (`lr = 1e-5`, `weight_decay = 0.01`)  
- **Batch Size:** 8  
- **Epochs:** 20  
- **Evaluation Metric:** F1 score (token + span level)

### Stage 2 — Dictionary-Infused RAG
- **Knowledge Source:** UMLS Metathesaurus  
- **Embeddings:** SapBERT (768-dim)  
- **Vector DB:** Pinecone (serverless, AWS `us-east-1`)  
- **Re-ranking:** 0.6 (semantic) + 0.4 (lexical)  
- **LLM:** Gemini 1.5-Flash  
- **Normalization:** Prompt-guided entity rewriting using retrieved UMLS context

---




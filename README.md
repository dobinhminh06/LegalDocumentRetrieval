# Team Akasuki - SoICT Hackathon 2024 Solution: Legal Document Retrieval

[![Status](https://img.shields.io/badge/Status-In%20Progress-green)](https://shields.io/)
[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)

**Mô tả tiếng Việt:** 
[![Mô tả tiếng Việt](https://raw.githubusercontent.com/stevenrskelton/flag-icon/master/png/16/country-4x3/vn.png)](https://github.com/ToJupiter/LegalDocumentRetrieval/blob/main/README_VN.md)

**Kaggle Notebook:** [Kaggle](https://www.kaggle.com/code/hctingnht/ldr24-soict)

**Notebook only can be found here:** [Notebook Only](https://github.com/ToJupiter/LegalDocumentRetrieval/blob/main/ldr24_soict_akasuki.ipynb)


For now, the Kaggle Notebook should contain all of needed components for implementation. A documentation could be provided in the future to make the most use of the project. Stay tuned!


## ✨ **Design Idea**

**🎯 Task:** Retrieve relevant legal documents related to a query from a given corpus.

**🤝 Team:** Akasuki

### 🚀 **Solution Approach**

Combine the power of two open-source Vietnamese language models:

1. **`bkai-foundation-models/vietnamese-bi-encoder` (Bi-encoder)** 🤖
2. **`namdp-ptit/ViRanker` (Cross-encoder)** ⚙️

### 🛠️ **Part 1: Fine-tuning the Bi-encoder**

*   **📝 Preprocessing and Embedding:**
    *   Utilize the `bi-encoder` to generate vector representations for queries and documents in the `corpus` and `training data`.
    🔤➡️🔢

*   **🎯 Fine-tuning:**
    *   Construct contrasting `(query, document)` pairs:
        *   **✅ Positive pairs:** Obtained from the `training data`.
        *   **❌ Negative pairs:** Selected from pairs not present in the `training data` and exhibiting low `cosine` similarity.
          ➕➖
    *   Train the `bi-encoder` using `MultipleNegativesRankingLoss`.
        🏋️‍♂️

### 🔍 **Part 2: Prediction with Public Test**

*   **📊 Query Embedding:**
    *   Employ the fine-tuned `bi-encoder` to embed queries from the `public test` set.
        🔤➡️🔢

*   **🧲 Candidate Retrieval:**
    *   Calculate `cosine similarity` between query vectors and document vectors in the `corpus`.
    *   Select the top 50 most promising candidates.
        ↔️

*   **🥇 Re-ranking:**
    *   Utilize the `cross-encoder` (`namdp-ptit/ViRanker`) to re-evaluate and rank the 50 candidates.
        🏆

*   **🏆 Results:**
    *   Choose the top 10 candidates with the highest scores from the `re-ranking` step.
        🔟

---
We hope you enjoy! If you have any questions or feedback, don't hesitate to reach out! 😊

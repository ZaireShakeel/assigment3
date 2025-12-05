# 📰 Multi-Field News Retrieval System

### TF-IDF • BM25 • Hybrid Ranking • Multiple Evaluation Metrics

This project implements an **Information Retrieval (IR) system** for a news dataset.

The system retrieves the most relevant news articles based on a user query using:
- **TF-IDF Vector Space Model**
- **BM25 Probabilistic Model**
- **Hybrid Scoring (BM25 + TF-IDF)** with metadata boosting

**Features:**
- ✔ Multi-field indexing (Heading, Article, NewsType)
- ✔ Manual relevance judgments for proper evaluation
- ✔ Full evaluation metrics & ranking comparison

---

## 📁 Dataset

The dataset used is: `Articles.csv`
⚠️ Data Link: The dataset file Articles.csv can be accessed here: [ https://drive.google.com/drive/folders/1XzaX8-8CWVxO63riDgxWQugjB4l2urov?usp=sharing ]

**Required fields in the dataset:**

| Column Name | Used For |
|------------|----------|
| Article | Main body text |
| Heading | Title (highest weight) |
| NewsType | Category label |
| Date | Display metadata |

> **Note:** Missing values are automatically handled in preprocessing.

---

## 🔧 Installation

Make sure you have **Python 3.8+** installed.

**Install dependencies:**

```bash
pip install pandas numpy scikit-learn rank-bm25
```

Make sure `Articles.csv` is in the same directory as the script.

---

## ▶️ Run the Project

```bash
python ir_project_assignment.py
```

**This will:**
- Load dataset
- Preprocess & build weighted documents
- Create TF-IDF & BM25 indexes
- Execute all search models
- Evaluate using relevance judgments
- Display results and comparison tables

---

## 🧠 How Ranking Works

**Field Weights:**

| Field | Weight |
|-------|--------|
| Heading | ×3 |
| NewsType | ×2 |
| Article | ×1 |

Combined into one weighted document per row.

**Then indexed by:**
- **TF-IDF** (ngram: 1–2, max_features=5000)
- **BM25** (default params)
- **Hybrid** = 0.6 × BM25 + 0.4 × TF-IDF (configurable)

**Optional boosting:**
- You can boost a specific NewsType (e.g., "business") by +20%.

---

## 📏 Evaluation Metrics

For each query, the following are calculated:

| Metric | What it Measures |
|--------|------------------|
| **Precision@K** | Relevant docs in top-K |
| **Recall@K** | Coverage of all relevant docs |
| **F1@K** | Balance of precision & recall |
| **MAP** | Ranking quality using precision per hit |
| **MRR** | How early the first relevant doc appeared |
| **NDCG@K** | Position-based ranking quality |

**A summary table compares:**
- TF-IDF
- BM25
- Hybrid (α=0.5)
- Hybrid (α=0.6)

---

## 🧪 Manual Relevance Judgments

Located in the code:

```python
test_queries = {
    "bengaluru": {616, 1483, 1484, 1497, 1745},
    "surging": {4, 32, 37, 48, 64},
    "military": {569, 686, 711, 732, 783},
    "philanthropist": {2000, 2446, 68},
    "finance Minister": {2437, 2450, 2463, 2482, 2498},
}
```

**You must manually determine relevance by reading articles in the dataset.**

**To add more:**

```python
test_queries["your keyword"] = {doc_id1, doc_id2, ...}
```

**To find matching docs:**

```python
for i, doc in enumerate(docs):
    if "keyword" in doc:
        print(i, doc[:100])
```

---

## 📤 Output Example

For each query:
- Metrics summary
- Ranked relevant list
- Top retrieved results preview
- Comparison table of all models

**Example snippet:**

```
-------------------------------
| Metric    | TF-IDF | BM25   | Hybrid (α=0.5) | Hybrid (α=0.6) |
|-----------|--------|--------|----------------|----------------|
| P@5       | 0.6000 | 0.8000 | 0.8000         | 0.8000         |
| P@10      | 0.5000 | 0.5000 | 0.5000         | 0.5000         |
| R@5       | 0.6000 | 0.8000 | 0.8000         | 0.8000         |
| R@10      | 1.0000 | 1.0000 | 1.0000         | 1.0000         |
| F1@5      | 0.6000 | 0.8000 | 0.8000         | 0.8000         |
| F1@10     | 0.6667 | 0.6667 | 0.6667         | 0.6667         |
| MAP       | 0.7467 | 0.8533 | 0.8533         | 0.8533         |
| MRR       | 1.0000 | 1.0000 | 1.0000         | 1.0000         |
| NDCG@5    | 0.7740 | 0.8973 | 0.8973         | 0.8973         |
| NDCG@10   | 0.8631 | 0.9156 | 0.9156         | 0.9156         |
-------------------------------
```

---

## 📌 Project Structure

```
├── ir_project_assignment.py    # Main code
├── Articles.csv                # Dataset
└── README.md                   # Documentation
```

---

## 🚀 Future Enhancements

- Query expansion (Word2Vec / BERT embeddings)
- Feedback-based reranking
- UI for interactive searching
- Better entity-based metadata extraction

---

## 👨‍💻 Author

**Zaire Shakeel Raja**

MSCS Information Retrieval & Text Mining — IR Project

---

## 📝 License


This project is created for educational purposes as part of an Information Retrieval course assignment.

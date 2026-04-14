# 🎬 CineMate — Dynamic Movie Recommendation System Using RNN (LSTM)

> **Enhancing User Experience Through Mood-Shift Based Predictions**

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://cinemate-lstm.streamlit.app)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.13+-orange.svg)](https://tensorflow.org)
[![ICCMDN-2025](https://img.shields.io/badge/Conference-ICCMDN--2025-gold.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 About

**CineMate** is a hybrid movie recommendation system presented at **ICCMDN-2025** (International Conference on Computational Methods, Data Science & Networking), organized by the Department of CS&IT, Maulana Azad National Urdu University, Hyderabad.

| | |
|---|---|
| **Authors** | Mohammad Arfeen · Afrah Fathima |
| **Institution** | Dept. CS&IT, MANUU, Hyderabad |
| **Conference** | ICCMDN-2025 (16–17 Jan 2025) |
| **Dataset** | MovieLens 1M |
| **Accuracy** | ~97.74% |
| **F1-Score** | ~95.5% |

---

## 🚀 Quick Start

### Option A — Run on Streamlit Cloud (No Setup)
[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://cinemate-lstm.streamlit.app)

### Option B — Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/aarfeen/cinemate-lstm.git
cd cinemate-lstm

# 2. Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # Linux/Mac
# venv\Scripts\activate         # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the Streamlit app
streamlit run app.py
```

The app will open at `http://localhost:8501`

> **Note:** On first run, the app downloads MovieLens 1M (~6 MB) and trains the LSTM model. This takes ~5–10 minutes. Subsequent runs load the saved model instantly.

### Option C — Google Colab Notebook
Open the fully annotated notebook with step-by-step execution and outputs:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aarfeen/cinemate-lstm/blob/main/CineMate_LSTM_Colab.ipynb)

---

## 🧠 How It Works

```
User Watch History (genre sequence)
        ↓
  Genre Encoding (LabelEncoder)
        ↓
  Sliding Window → Sequences of length 10
        ↓
┌─────────────────────────────┐
│   LSTM Architecture         │
│  ┌─────────────────────┐    │
│  │  Embedding Layer    │    │  Genre IDs → 50-dim vectors
│  │  LSTM Layer 1 (128) │    │  return_sequences=True
│  │  Dropout (0.2)      │    │
│  │  LSTM Layer 2 (128) │    │  return_sequences=False
│  │  Dropout (0.2)      │    │
│  │  Dense (64, ReLU)   │    │
│  │  Softmax (19 genres)│    │  Probability over genres
│  └─────────────────────┘    │
└─────────────────────────────┘
        ↓
  Top-K Predicted Genres
        ↓
  Hybrid Scoring:
  α·CollaborativeScore + β·ContentScore + γ·GenreBoost + δ·Rating
        ↓
  🎬 Personalized Movie Recommendations
```

---

## 📊 Results

| Metric | Value |
|--------|-------|
| Training Accuracy | 97.74% |
| Training Loss | 0.3257 |
| Precision | ~95% |
| Recall | ~96% |
| F1-Score | ~95.5% |

### Comparison with Baselines

| System | Algorithm | Accuracy | F1-Score | Temporal? |
|--------|-----------|----------|----------|-----------|
| MovieLens Hybrid | MF + KNN | ~92% | 0.89 | ❌ |
| BellKor (Netflix) | RBM CF | ~88% | 0.85 | ❌ |
| DeepCoNN (2017) | CNN + Reviews | ~94% | 0.91 | ❌ |
| NCF (2017) | Deep Neural CF | ~95% | 0.925 | ❌ |
| AutoRec | Autoencoder CF | ~90% | 0.885 | ❌ |
| **CineMate (Ours)** | **RNN-LSTM Hybrid** | **97.74%** | **~95.5%** | **✅** |

---

## 🗂️ Repository Structure

```
cinemate-lstm/
│
├── app.py                          # 🌐 Streamlit web application
├── CineMate_LSTM_Colab.ipynb       # 📓 Google Colab notebook
├── requirements.txt                # 📦 Python dependencies
├── README.md                       # 📖 This file
│
├── assets/                         # 📁 Static assets
│   └── demo_screenshot.png
│
└── .streamlit/
    └── config.toml                 # ⚙️ Streamlit configuration
```

---

## 🎮 App Features

| Tab | Description |
|-----|-------------|
| 🎯 **Get Recommendations** | Build your watch history → LSTM predicts next genres → get movies |
| 📊 **Explore Dataset** | Genre distributions, rating patterns, genre transition heatmap |
| 🧠 **Model Performance** | Architecture details, accuracy/F1/precision/recall, per-genre metrics |
| 🔄 **Compare Methods** | CineMate vs. 5 baseline systems, research gaps & solutions |

---

## 🔧 Model Parameters

| Parameter | Value |
|-----------|-------|
| Sequence Length | 10 |
| Embedding Dimension | 50 |
| LSTM Units (per layer) | 128 |
| LSTM Layers | 2 |
| Dropout Rate | 0.2 |
| Batch Size | 64 |
| Max Epochs | 50 |
| Optimizer | Adam (lr=0.001) |
| Loss Function | Categorical Cross-Entropy |
| Dataset | MovieLens 1M (6,040 users, 3,706 movies, 1M ratings) |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend/UI | Streamlit |
| ML Model | TensorFlow 2.x / Keras |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Collaborative Filtering | Scikit-learn (KNN) |
| Content-Based Filtering | Scikit-learn (Cosine Similarity) |
| Dataset | MovieLens 1M (GroupLens) |

---

## 📚 References

1. Reddy, SRS & Nalluri et al. (2019). *Content-Based Movie Recommendation Using Genre Correlation*. SCI 2018.
2. M. Gupta, A. Thakkar et al. (2020). *Movie Recommender System Using Collaborative Filtering*. ICESC 2020.
3. S. Sharma & H.K. Shakya (2023). *Hybrid Recommendation System Using SOM*. ISCON 2023.
4. Sonawane et al. (2023). *Movie Recommendation using Optimised RNN*. IRJMETS Vol.5.
5. B. Hidasi et al. (2016). *Session-based Recommendations with RNNs*. ICLR 2016.
6. X. He et al. (2017). *Neural Collaborative Filtering*. WWW 2017.
7. Hochreiter & Schmidhuber (1997). *Long Short-Term Memory*. Neural Computation.

---

## 👨‍💻 Authors

**Mohammad Arfeen**  
B.Tech Computer Science, MANUU  
📧 iamaarfeen@gmail.com

**Afrah Fathima** (Guide)  
Assistant Professor, Dept. CS&IT, MANUU  
📧 af.fathima1@manuu.edu.in

---

## 📄 License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

---

*Presented at ICCMDN-2025 — International Conference on Computational Methods, Data Science & Networking, Maulana Azad National Urdu University, Hyderabad, 16–17 January 2025.*

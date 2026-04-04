<div align="center">

<img src="figures/banner.png" alt="Project Banner" width="80%"/>

# 🏛️ Congressional Twitter Intelligence

> A decade of congressional tweets analyzed to build a data-driven lobbying targeting system.

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![SQLite](https://img.shields.io/badge/SQLite-Database-003B57?style=flat&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat&logo=scikitlearn&logoColor=white)](https://scikit-learn.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**1,243,370 tweets · 548 members · 2008–2017**

</div>

---

## 📊 Key Figures

<div align="center">
  <img src="figures/fig1_fig2_top_bigrams.png" alt="Top 20 Distinctive Bigrams by Party" width="48%"/>
  <img src="figures/fig4_vocab_divergence.png" alt="Vocabulary Divergence Over Time" width="48%"/>
</div>

<div align="center">
  <img src="figures/fig8_top_lls_members.png" alt="Top 20 Members by LLS" width="48%"/>
  <img src="figures/fig9_bws_heatmap.png" alt="Bipartisan Window Score Heatmap" width="48%"/>
</div>

---

## 🗂️ Project Overview

This capstone project analyzes a decade of congressional Twitter activity to build a data-driven lobbying targeting system. Twitter stores no political metadata — party, chamber, and state are all missing. We solved this through a three-step enrichment join against the `@unitedstates` legislators database, recovering metadata for **74.8%** of members.

---

## 🚀 Quickstart

> **Note:** The raw dataset is not included due to GitHub's file size limit. See [Data](#-data) below.

```bash
git clone https://github.com/username/congressional-twitter-intelligence.git
cd congressional-twitter-intelligence
pip install -r requirements.txt
jupyter notebook notebooks/milestone_3.ipynb
```

---

## 🛠️ Stack

| Tool | Purpose |
|---|---|
| SQLite | Primary database and storage |
| Python / pandas | Data wrangling and analysis |
| scikit-learn | TF-IDF vectorization, OLS regression |
| TextBlob | Sentiment scoring |
| matplotlib | Data visualization |
| scipy | Pearson correlation tests |

---

## 📁 Structure

```
repo/
├── figures/                  # All saved charts & plots (Fig 1–9)
├── data/                     # Place raw dataset here (see below)
├── notebooks/
│   ├── milestone_1.ipynb     # Data enrichment & setup
│   ├── milestone_2.ipynb     # Descriptive statistics
│   └── milestone_3.ipynb     # TF-IDF, regression, custom metrics
├── requirements.txt
└── README.md
```

---

## 💾 Data

The raw dataset (`US_PoliticalTweets.tar.gz`, 229MB) is not included in this repo due to GitHub's file size limit.

Download it from: [link to original source or Google Drive]

Once downloaded, place it in the `data/` folder and run `notebooks/milestone_3.ipynb` from the top.

---

## ⚠️ Caveats

- Dataset covers **2008–2017** only — Twitter's 280-char limit, follower growth, and political intensity all postdate the archive
- 24.4% of tweets could not be matched to a party (Independent members, data gaps)
- Sentiment scored via TextBlob on a 20K random sample — not full corpus
- LLS and BWS scores should be re-validated with updated data before operational use
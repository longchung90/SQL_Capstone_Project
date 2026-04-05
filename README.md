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

## 📊 Figures

| | |
|:---:|:---:|
| <img src="figures/chart_m3_fig1_fig2_bigrams.png" alt="Fig 1–2 — Top 20 Bigrams by Party" width="100%"/><br><sub>Fig 1–2 — Top 20 Bigrams by Party</sub> | <img src="figures/chart_m3_fig3_bipartisan.png" alt="Fig 3 — Top 15 Bipartisan Bigrams" width="100%"/><br><sub>Fig 3 — Top 15 Bipartisan Bigrams</sub> |
| <img src="figures/chart_m3_fig4_divergence.png" alt="Fig 4 — Vocabulary Divergence Over Time" width="100%"/><br><sub>Fig 4 — Vocabulary Divergence Over Time</sub> | <img src="figures/chart_m3_fig5_chamber_box.png" alt="Fig 5 — Retweet Distribution: Senate vs House" width="100%"/><br><sub>Fig 5 — Retweet Distribution: Senate vs House</sub> |
| <img src="figures/chart_m3_fig6_sentiment_scatter.png" alt="Fig 6 — Sentiment vs Log Retweet Count" width="100%"/><br><sub>Fig 6 — Sentiment vs Log Retweet Count</sub> | <img src="figures/chart_m3_fig7_regression.png" alt="Fig 7 — OLS Regression Coefficients" width="100%"/><br><sub>Fig 7 — OLS Regression Coefficients</sub> |
| <img src="figures/chart_m3_fig8_lls.png" alt="Fig 8 — Top 20 Members by LLS" width="100%"/><br><sub>Fig 8 — Top 20 Members by LLS</sub> | <img src="figures/chart_m3_fig9_bws_heatmap.png" alt="Fig 9 — Bipartisan Window Score Heatmap" width="100%"/><br><sub>Fig 9 — Bipartisan Window Score Heatmap by State × Month</sub> |

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
jupyter notebook notebooks/M3.ipynb
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
├── figures/                        # All saved charts & plots (Fig 1–9 + supplementary)
├── data/
│   ├── export/                     # CSV exports for Tableau
│   └── US_PoliticalTweets.tar.gz   # Raw dataset (not tracked — see Data section)
├── notebooks/
│   ├── M3.ipynb                    # TF-IDF, regression, custom metrics
│   ├── US_Political_Tweet_War_M2.ipynb  # Descriptive statistics
│   ├── Project_Proposal.ipynb      # Project proposal
│   └── Project_Proposal.pdf        # Proposal PDF export
├── presentation/
│   └── Lobbyists4America.html      # Final HTML presentation
├── sql/
│   └── SQL-Query.ipynb             # SQL queries notebook
├── .gitignore
└── README.md
```

---

## 💾 Data

The raw dataset (`US_PoliticalTweets.tar.gz`, 229MB) is not included in this repo due to GitHub's file size limit.

Download it from: [link to original source or Google Drive]

Once downloaded, place it in the `data/` folder and run `notebooks/M3.ipynb` from the top.

---

## ⚠️ Caveats

- Dataset covers **2008–2017** only — Twitter's 280-char limit, follower growth, and political intensity all postdate the archive
- 24.4% of tweets could not be matched to a party (Independent members, data gaps)
- Sentiment scored via TextBlob on a 20K random sample — not full corpus
- LLS and BWS scores should be re-validated with updated data before operational use

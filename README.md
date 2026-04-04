# Congressional Twitter Intelligence — SQL Capstone Project

**Client:** Lobbyists4America  
**Dataset:** 1,243,370 congressional tweets · 2008–2017  
**Members:** 548 Congress members · 10-year coverage window

---

## Project Overview

This capstone project analyzes a decade of congressional Twitter activity to build a data-driven lobbying targeting system. The core problem: Twitter stores no political metadata — party, chamber, and state are all missing. We solved this through a three-step enrichment join against the `@unitedstates` legislators database, recovering metadata for 74.8% of members.

---

## Milestones

### Milestone 1 — Data Enrichment & Setup
- Loaded raw tweet CSVs into SQLite
- Joined tweet data with legislators database by `screen_name`
- Built master table: 1,243,370 rows × 19 columns
- 924,517 rows matched to Republican or Democrat members
- 138 members (302,898 tweets) retained but excluded from party/chamber comparisons — declared, consistent exclusion

### Milestone 2 — Descriptive Statistics
- Identified power-law distribution: mean/median retweet ratio of **47.5×**
- Switched all reporting from mean to **median** to strip viral noise
- Built quadrant chart: tweet volume vs. median reach per member
- Key finding: top 10% of members hold **62.5%** of all retweets

### Milestone 3 — Beyond Descriptive Statistics
- TF-IDF theme analysis at bigram level (min_df=50, max_features=10,000)
- Log-odds scoring controlling for volume differences (R posts 28% more)
- Pearson correlations, OLS linear regression, and two new custom metrics

---

## Key Findings

### TF-IDF Theme Analysis

| Category | Top Bigrams |
|---|---|
| Democrat-only | gun violence, climate change, civil rights, women health |
| Republican-only | obamacare repeal, border security, law enforcement, second amendment |
| Bipartisan | health care, veterans, jobs economy, town hall |

- **Party predicts topic more strongly than chamber** — House and Senate members of the same party communicate more similarly to each other than cross-party colleagues in the same chamber
- Vocabulary cosine distance grew from **0.31 (2009) → 0.61 (2017)** — polarization is accelerating

### Correlations

| Correlation | Result | Implication |
|---|---|---|
| Senate membership × retweets | r = +0.31 (p < 0.001) | Senate members achieve **1.8× median reach** vs House |
| Negative sentiment × retweets | r = −0.19 (p < 0.001) | Outrage travels further than celebration |

### OLS Regression — Predicting Member Influence

**R² = 0.475** · Predicts log(total_retweets) per member

| Predictor | Coefficient |
|---|---|
| tweet_count | +1.032 |
| is_democrat | +0.692 |
| is_senate | +0.012 |
| mean_sentiment | −0.078 |
| active_years | −0.142 |

---

## New Metrics

### Metric 1: Lobbying Leverage Score (LLS)

Strips viral noise from mean retweets; uses median for stable, consistent influence ranking.

```
LLS = median_retweets_per_tweet × log(tweet_count + 1) × chamber_multiplier
chamber_multiplier = 1.8 if Senate, 1.0 if House
```

**Tiers:** LLS > 20 = Priority Tier 1 | LLS 10–20 = Tier 2 | Below 10 = Monitor only

| Rank | Member | Party | Chamber | LLS |
|---|---|---|---|---|
| 1 | Elizabeth Warren | D | Senate | 5,990 |
| 2 | Ted Cruz | R | Senate | 3,216 |
| 3 | Marco Rubio | R | Senate | 2,355 |
| 4 | Kamala Harris | D | Senate | 2,017 |
| 5 | Chuck Schumer | D | Senate | 1,441 |

### Metric 2: Bipartisan Window Score (BWS)

Captures when both parties are simultaneously active and evenly matched — the only window where a single campaign reaches both sides.

```
BWS(state, month) = competition_score × min(D_tweets, R_tweets) / max(D_tweets, R_tweets)
```

**Top states by average BWS:**

| State | Avg BWS | Peak Month |
|---|---|---|
| Illinois | 0.47 | September |
| Colorado | 0.46 | October |
| Indiana | 0.46 | September |
| Minnesota | 0.43 | April |
| Wisconsin | 0.35 | March |

---

## Recommendations

1. **Restructure outreach by party, not chamber** — merge Senate + House lists into separate D and R playbooks
2. **Lead bipartisan campaigns with "health care"** — the #1 bigram for both parties simultaneously
3. **Weight Senate targets 2–3× vs House** — structural 1.8× reach advantage confirmed by both correlation and regression
4. **Run IL / CO / IN campaigns in Q3–Q4** — highest BWS states with peak bipartisan windows in Sep–Oct; avoid August (congressional recess)

---

## Tech Stack

| Tool | Purpose |
|---|---|
| SQLite | Primary database and storage |
| Python / pandas | Data wrangling and analysis |
| scikit-learn | TF-IDF vectorization, OLS regression |
| TextBlob | Sentiment scoring |
| matplotlib | Data visualization |
| scipy | Pearson correlation tests |

---

## Database Tables

| Table | Description |
|---|---|
| `tweet` | Master tweet table (1.24M rows × 19 cols) |
| `tfidf_bigrams` | TF-IDF scores and log-odds per bigram |
| `yearly_divergence` | Cosine distance between party vocabularies by year |
| `tweet_sentiment` | Sentiment scores for 20K sampled tweets |
| `member_lls` | LLS scores per member |
| `monthly_bws` | BWS scores by state × month |
| `state_bws` | Average BWS by state |

---

## Figures

| Figure | Description |
|---|---|
| Fig 1 & 2 | Top 20 distinctive bigrams by party (log-odds TF-IDF) |
| Fig 3 | Top 15 bipartisan bigrams |
| Fig 4 | Vocabulary divergence between parties over time |
| Fig 5 | Retweet distribution: Senate vs House |
| Fig 6 | Sentiment vs log(retweet count) |
| Fig 7 | OLS regression coefficients |
| Fig 8 | Top 20 members by LLS |
| Fig 9 | Bipartisan Window Score heatmap by state × month |

---

## Caveats

- Dataset covers **2008–2017** only — Twitter's 280-char limit, follower growth, and political intensity all postdate the archive
- 24.4% of tweets could not be matched to a party (Independent members, data gaps)
- Sentiment scored via TextBlob on a 20K random sample — not full corpus
- LLS and BWS scores should be re-validated with updated data before operational use

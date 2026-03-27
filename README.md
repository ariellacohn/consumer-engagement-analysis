# Consumer Engagement Analysis — OkCupid Profile Data

**Portfolio project demonstrating consumer marketplace analytics skills**
*Framed for a Match Group / Tinder product analytics audience*


## About This Project

I've always been fascinated by what makes people click, literally and figuratively. Dating apps sit at this interesting intersection of behavioral psychology and product design, where the data people share (or choose not to share) about themselves reveals so much about how they want to be seen.

When I found the OkCupid dataset, I wanted to approach it the way a product analyst at Tinder actually would: not just describing who's on the platform, but asking what drives engagement, where users drop off, and what that means for product decisions. This is that analysis.

---

## Overview

This project applies data science and product analytics techniques to a dataset of ~60,000 OkCupid dating profiles collected from the San Francisco Bay Area. The analysis is structured around four questions that matter on any consumer marketplace platform:

1. **Who is on the platform?** — demographic and behavioral segmentation
2. **How engaged are users?** — profile completeness as an engagement proxy
3. **What user types exist?** — K-means clustering to surface actionable personas
4. **What should we do about it?** — prioritized product recommendations framed for a Tinder product team

---

## Dataset

| Field | Description |
|---|---|
| `age`, `sex`, `orientation` | Core demographics |
| `body_type`, `diet`, `drinks`, `drugs`, `smokes` | Lifestyle self-disclosure |
| `education`, `job`, `income` | Socioeconomic signals |
| `ethnicity`, `religion`, `sign`, `offspring`, `pets` | Identity & values |
| `height`, `location`, `status` | Profile attributes |
| `last_online` | Recency / activity signal |
| `essay0` – `essay9` | Open-ended profile prompts (key engagement surface) |

**Source:** [OkCupid Profile Data (Kirkegaard & Dalgaard, 2016)](https://openpsych.net/paper/46) — publicly released research dataset. ~60K profiles, Bay Area, ~2012.

> **Note:** This dataset is used for analytical demonstration purposes. All analysis is aggregate — no individual users are identified or targeted.

---

## Analysis Structure

### Section 1 — EDA & Behavioral Segmentation

- Data quality audit (field-level missingness mapped as intentional non-disclosure signals)
- Age, gender, and orientation distribution
- Lifestyle behavior rates (drinks, smokes, drugs)
- Education and income tier breakdowns
- Occupation landscape
- **Recency segmentation:** Active / Recent / Lapsing / Dormant — a basic RFM-style behavioral split

### Section 2 — Profile Completeness Score (PCS)

Custom-built engagement proxy scored 0–100:

- **Demographic completeness** (1 pt per filled field, 18 fields)
- **Essay presence** (2 pts per completed prompt, 10 prompts)
- **Essay depth bonus** (up to 3 pts per essay based on character count)

Produces four engagement tiers: **Power User / Engaged / Casual / Minimal**

Analyzed by: age group, gender, education level, and recency segment. Essay completion heatmap breaks down which prompts get answered across tiers.

### Section 3 — K-Means User Personas

Feature engineering → StandardScaler → K-means (K=5 selected via elbow + silhouette analysis)

**Five personas discovered:**

| Persona | Characteristics |
|---|---|
| **The Connector** | Highest PCS, most essays, most active — the platform's power user |
| **The Young Professional** | Moderately active, career-focused, subscription-conversion target |
| **The Graduate** | Older, higher education, serious intent, quality-over-quantity mindset |
| **The Selective** | Completes demographics but writes few essays — needs prompt nudges |
| **The Casual Browser** | Low engagement, lapsing — re-engagement campaign target |

Visualized via PCA scatter plot and normalized radar chart.

### Section 4 — Business Recommendations

Written as a product analytics brief for a Tinder product review. Five prioritized recommendations covering:

1. **Profile Completeness Score as an onboarding KPI** — tie profile depth to match rate outcomes in messaging to users
2. **Persona-targeted push notification strategy** — stop blasting; segment by behavioral archetype
3. **Education/income → subscription propensity model** — identify Gold/Platinum conversion candidates at registration
4. **Lifestyle compatibility tags in match UI** — show "You both drink socially" style signals to increase field disclosure and matching confidence
5. **Essay prompt UX overhaul** — treat prompts as contextual, mobile-native, voice-enabled feature surfaces

Each recommendation includes a primary metric target and implementation effort / impact rating. Section closes with a prioritization matrix (effort × impact quadrant).

---

## Technical Stack

```
Python 3.9+
pandas, numpy         — data manipulation
matplotlib, seaborn   — visualization
scikit-learn          — KMeans, PCA, StandardScaler, silhouette_score
```

Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

Run the notebook:

```bash
jupyter notebook consumer_engagement_analysis.ipynb
```

---

## Key Findings

- **~35% of users are Power Users or Engaged** — they complete most essay prompts and demographic fields; these users drive platform value disproportionately
- **Essay completion drops sharply after prompt 4** — UX friction is the primary barrier, not lack of intent
- **Active users (last online ≤1 week) have significantly higher PCS** — engagement and profile investment are tightly correlated
- **Income is disclosed by only ~25% of users** — but disclosers have higher PCS, suggesting this field is a quality signal, not a noise field
- **Women have higher average PCS than men** — a consistent pattern in consumer dating marketplaces

---

## Relevance to Match Group / Tinder

This analysis demonstrates competencies directly applicable to a consumer marketplace analytics role:

- **Behavioral segmentation** using real product signals (recency, profile depth, lifestyle disclosure)
- **Proxy metric design** — constructing PCS as an engagement proxy when direct outcome data isn't available, the same approach used when A/B test data is sparse
- **Unsupervised ML for persona discovery** — translating clustering output into actionable product archetypes
- **Product analytics communication** — recommendations written for a product team, not a data team: metric-anchored, effort-aware, and tied to business outcomes

---

*Ariella Cohn — Consumer Marketplace Analytics*

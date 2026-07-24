# Bird Migration Prediction

<br>
<p align="center">
  <strong>Report submitted by:</strong>
</p>
<p align="center">
  <strong>B.JASVANTH</strong><sup>2B</sup><br>
  <strong>JAYANTH PANDEY</strong><sup>1A</sup><br>
</p>
<p align="center">
  <em>For the successful completion of the internship as</em><br>
  <strong>Summer (Data Science) Intern 2026</strong><br>
  <strong>[Tenure: 7 weeks]</strong>
</p>
<p align="center">
  <em>Under the supervision of</em><br><br>
  <strong>Mr. Samyabrata Roy</strong><sup>*</sup><br>
  Associate Software Developer<br>
  IDEAS - Institute of Data Engineering, Analytics and Science Foundation,<br>
  Technology Innovation Hub, Indian Statistical Institute, Kolkata
</p>
<br>
<p align="center">
  <strong>Report submitted to:</strong><br><br>
  <strong>
  IDEAS - Institute of Data Engineering, Analytics and Science Foundation,<br>
  Technology Innovation Hub, Indian Statistical Institute,<br>
  Kolkata, West Bengal, India
  </strong>
</p>
<br>

---

<sup>A</sup>  Lendi Institute of Engineering and Technology, Vizianagaram;
<sup>B</sup> Chandigarh University;
<sup>1</sup> jasvanth1063@gmail.com;
<sup>2</sup> jayantkvmau3@gmail.com;
<sup>*</sup> sroy@ideas-tih.org

---

# IDEAS-TIH Summer Internship Program 2026

This repository contains the project work completed as part of the **Summer Internship Program 2026** under **IDEAS - Technology Innovation Hub, Indian Statistical Institute, Kolkata**.

The repository includes source code, datasets, notebooks, documentation, reports, references, and other project-related materials developed by the assigned intern team.

---

# Project Details

## Project Title

**Bird Migration Prediction**

---

## Project Category

- ✅ Machine Learning / Deep Learning Project
- ✅ Data Analysis Project

---

## Problem Statement

### What problem is being addressed

Bird migration is one of the most complex phenomena in ecology, involving billions of birds
travelling thousands of kilometres annually between breeding and wintering grounds. Traditional
approaches to studying migration relied on coarse spatial tracking methods that lacked the
resolution to identify fine-grained geographic zones or predict future movement patterns.
This project addresses the problem of **predicting which geographic migration zone a bird will
occupy next**, given its current GPS sensor readings.

### Why the problem is important

Understanding where migratory birds will be is critical for:
- **Wildlife conservation** — identifying key stopover zones and wintering habitats under
  threat from climate change and habitat destruction
- **Climate change research** — tracking shifts in migration timing and routes as seasonal
  patterns change
- **Ecological monitoring** — enabling automated early-warning systems for species at risk
  during migration

The previous GRU-based deep learning approach targeted exact coordinate regression (latitude,
longitude), which produced a data leakage issue — **R² = 1.0000** — flagged by ISI reviewers.
The revised approach eliminates this entirely by reframing the problem as **multi-class
classification**: predict a discrete geographic zone label (cluster ID) rather than a
continuous coordinate.

### What data, system, or method will be used

**Dataset:** White Stork GPS tracking data (MoveBank)
- **Records:** 61,920 GPS readings across 3 birds — Eric, Nico, Sanne
- **Period:** August 2013 – April 2014 (258 days — full annual cycle)
- **Features:** latitude, longitude, altitude, speed\_2d, direction, timestamp

**Methods:**
- **Phase 1 — EDA:** 9 interactive Plotly charts to understand data structure,
  distributions, and seasonal patterns
- **Phase 2 — Feature Engineering:** Haversine distance, bearing angle, rolling speed mean,
  season encoding, resting flag, Z-score normalization
- **Phase 3 — Globe Clustering (K-Means):** Divide the globe into geographic migration
  zones using K-Means clustering on GPS coordinates
- **Phase 4 — Classification (Random Forest + XGBoost):** Predict which zone the bird
  will occupy next given current features
- **Phase 5 — Evaluation:** F1 score, confusion matrix, K-fold cross-validation with
  time-aware train/test split

### What output or solution is expected

- A trained **Random Forest** and **XGBoost** classifier that predicts the next geographic
  migration zone (cluster ID) for any GPS reading
- An interactive **Plotly Scattergeo map** showing the globe divided into migration zones
  colour-coded by cluster
- A complete **internship report** following the ISI Summer Internship Report Template 2026
- All trained models saved as `rf_model.pkl` and `xgb_model.pkl`

---

## Project Pipeline — 6 Phases

| Phase | Name | Status |
|---|---|---|
| 1 | Exploratory Data Analysis (EDA) | ✅ Completed — 9 Plotly charts |
| 2 | Feature Engineering | ⏳ Next notebook |
| 3 | Globe Clustering with K-Means | ⏳ Core new contribution |
| 4 | Cluster Prediction — RF / XGBoost | ⏳ Supervised classification |
| 5 | Model Evaluation | ⏳ F1, confusion matrix, CV |
| 6 | Final Output and Report | ⏳ Map + internship report |

---

## Tech Stack

- Python 3.10
- pandas, numpy
- plotly (100% — all charts interactive HTML)
- scikit-learn (KMeans, RandomForest, metrics)
- xgboost
- hdbscan
- Google Colab

---

## Repository Structure

```
summer_intern_group-c-2026/
├── README.md
├── bird_migration.csv                          ← Raw GPS dataset
├── Bird_Migration_EDA_KMeans_Foundation.ipynb  ← Phase 1 EDA (complete)
├── bird_migration_features.csv                 ← Phase 2 output (pending)
├── bird_migration_clustered.csv                ← Phase 3 output (pending)
├── rf_model.pkl                                ← Phase 4 output (pending)
├── xgb_model.pkl                               ← Phase 4 output (pending)
└── Bird_Migration_Complete_Pipeline.ipynb      ← Phase 6 final (pending)
```

---

## How to Run

1. Clone this repository
2. Upload `bird_migration.csv` to `/content/` in Google Colab
3. Open `Bird_Migration_EDA_KMeans_Foundation.ipynb`
4. Run all cells top to bottom

---

## Dataset

- **Source:** MoveBank GPS tracking — White Stork migration
- **Records:** 61,920 GPS readings across 3 birds
- **Period:** August 2013 – April 2014 (258 days)
- **Features:** latitude, longitude, altitude, speed\_2d, direction, timestamp, bird\_name

---

*Bird Migration GPS Tracking — ML Project | ISI Kolkata IDEAS Internship 2026 |
Jayanth pandey(Chandigarh university) &
B. Jasvanth (Lendi Institute of Engineering and Technology)*

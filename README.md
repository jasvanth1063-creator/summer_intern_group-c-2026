# Bird Migration Prediction — Group C (Jasvanth's Contribution)

<br>
<p align="center">
  <strong>Report submitted by:</strong>
</p>
<p align="center">
  <strong>B. JASVANTH</strong><br>
  Lendi Institute of Engineering and Technology, Vizianagaram<br>
  jasvanth1063@gmail.com
</p>
<p align="center">
  <em>For the successful completion of the internship as</em><br>
  <strong>Summer (Data Science) Intern 2026</strong><br>
  <strong>[Tenure: 7 weeks]</strong>
</p>
<p align="center">
  <em>Under the supervision of</em><br><br>
  <strong>Mr. Samyabrata Roy</strong><br>
  Associate Software Developer<br>
  IDEAS - Institute of Data Engineering, Analytics and Science Foundation,<br>
  Technology Innovation Hub, Indian Statistical Institute, Kolkata<br>
  sroy@ideas-tih.org
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

---

# IDEAS-TIH Summer Internship Program 2026

This folder contains the project work completed by **B. Jasvanth** as part of the **Summer Internship Program 2026** under **IDEAS - Technology Innovation Hub, Indian Statistical Institute, Kolkata**.

It includes all notebooks, processed datasets, output charts, saved models, and the final reference report developed and executed independently as part of Group C's contribution to the Bird Migration Prediction project.

---

# Project Details

## Project Title

**Interpretable Machine Learning Application in Bird Migration Trajectory Analysis Using GPS Data**

---

## Project Category

- ✅ Machine Learning Project
- ✅ Data Analysis Project
- ✅ Interpretable AI Project

---

## Problem Statement

Bird migration is one of the most complex phenomena in ecology, involving billions of birds travelling thousands of kilometres annually between breeding and wintering grounds. This project addresses the problem of **predicting which geographic migration zone a bird will occupy next**, given its recent GPS telemetry history.

The task is framed as **multi-class zone classification** — predicting a discrete geographic zone label rather than a continuous coordinate — using an end-to-end interpretable machine learning pipeline emphasising **correctness, reproducibility, and interpretability** over research novelty.

A prior GRU-based deep learning approach targeting exact coordinate regression produced a data leakage issue (R² = 1.0000) flagged by ISI reviewers. This pipeline eliminates that entirely by reframing the target as a cluster label derived from unsupervised geographic zone discovery.

---

## Dataset

- **Source:** MoveBank GPS tracking — White Stork migration (Eric, Nico, Sanne)
- **Records:** 61,920 GPS fixes across 3 birds
- **Period:** 15 August 2013 – 30 April 2014 (258 days — full annual migration cycle)
- **Raw features:** latitude, longitude, altitude, speed\_2d, direction, date\_time, bird\_name, device\_info\_serial

---

## Pipeline — Phases Completed (Jasvanth's Part)

| Phase | Name | Notebook | Status |
|---|---|---|---|
| 3 | Exploratory Data Analysis | Phase3\_Bird\_Migration\_EDA\_Complete.ipynb | ✅ Completed |
| 5 | Migration Zone Discovery (K-Means) | Phase5\_Migration\_Zone\_Discovery.ipynb | ✅ Completed |
| 6 | Sequence Dataset Construction | Phase6\_Sequence\_Dataset\_Construction.ipynb | ✅ Completed |
| 7 | Model Development | Phase7\_Model\_Development.ipynb | ✅ Completed |

---

## Key Results

| Metric | Value |
|---|---|
| Best Model | Decision Tree (max\_depth=8) |
| Mean Accuracy (5-fold TimeSeriesSplit) | 99.85% |
| Mean F1-macro | 99.86% |
| ROC-AUC (valid folds) | 0.9973 |
| Migration Zones Discovered (K-Means, k=3) | Netherlands · North Africa · West Africa |
| Silhouette Score (k=3) | 0.8276 |
| Davies-Bouldin Index (k=3) | 0.2516 |
| Total sequence windows constructed | 61,905 |
| Features per window | 40 (8 per timestep × 5 timesteps) |

---

## Data Integrity Fixes Applied

Three bugs identified and corrected before any model was trained:

1. **Merge collision** — `bird_migration_clustered.csv` had 166 duplicate rows caused by a `merge(on='date_time')` without also keying on `bird_name`. Fixed at root cause. Final shape: 61,920 rows, 0 duplicates.
2. **Missing coordinate scaling** — K-Means was fit on unscaled radian coordinates. `StandardScaler` added before fitting; centroid inverse-transform corrected everywhere degrees are reported.
3. **Non-reproducible sampling** — Phase 3 silhouette sample used no random seed. Fixed to `RandomState(42)`.

---

## Repository Structure

```
Group-C-Jasvanth/
│
├── data/
│   ├── raw/
│   │   └── bird_migration_raw.csv
│   └── processed/
│       ├── bird_migration_cleaned.csv
│       ├── bird_migration_features.csv
│       ├── bird_migration_clustered.csv
│       └── bird_migration_sequence.csv
│
├── notebooks/
│   ├── Phase3_Bird_Migration_EDA_Complete.ipynb
│   ├── Phase5_Migration_Zone_Discovery.ipynb
│   ├── Phase6_Sequence_Dataset_Construction.ipynb
│   └── Phase7_Model_Development.ipynb
│
├── output/
│   ├── charts/
│   │   ├── phase-3_charts/
│   │   │   └── phase3_output_charts(all)
│   │   ├── phase-5_charts/
│   │   │   ├── phase5_cluster_map.html
│   │   │   ├── phase5_evaluation_metrics.html
│   │   │   └── phase5_per_point_silhouette.html
│   │   ├── phase-6_charts/
│   │   │   ├── phase6_target_distribution.html
│   │   │   ├── phase6_target_per_bird.html
│   │   │   ├── phase6_timeline.html
│   │   │   └── phase6_windows_per_bird.html
│   │   └── phase-7_charts/
│   │       ├── phase7_model_comparison.html
│   │       └── phase7_train_vs_test.html
│   └── models/
│       ├── best_model.pkl
│       └── feature_cols.pkl
│
├── produced_reports/
│   ├── phase7_cv_results.csv
│   └── Bird_Migration_Reference_Guide.pdf
│
└── README.md
```

---

## How to Run

Run notebooks strictly in this order — each one reads the output of the previous:

```
Phase3 → Phase5 → Phase6 → Phase7
```

1. Place `bird_migration_cleaned.csv` and `bird_migration_features.csv` in the working directory
2. Run `Phase3_Bird_Migration_EDA_Complete.ipynb` — EDA and K-Means elbow preview
3. Run `Phase5_Migration_Zone_Discovery.ipynb` → produces `bird_migration_clustered.csv`
4. Run `Phase6_Sequence_Dataset_Construction.ipynb` → produces `bird_migration_sequence.csv`
5. Run `Phase7_Model_Development.ipynb` → produces `best_model.pkl`, `feature_cols.pkl`, `phase7_cv_results.csv`

All charts are saved as interactive HTML files in `output/charts/`.

---

## Tech Stack

- Python 3.10+
- pandas, numpy, scikit-learn, xgboost
- plotly (all charts — 100% interactive HTML)
- joblib (model serialisation)
- nbclient (notebook re-execution and validation)

---

## Group C — Remaining Phases (Jayant Pandey's Contribution)

The following phases are completed and maintained by **Jayant Pandey** (Chandigarh University) as his independent contribution to the Group C pipeline:

| Phase | Name | Description | Status |
|---|---|---|---|
| 2 | Data Cleaning | Duplicate removal, missing value imputation, timestamp conversion, altitude and speed validation, sorting by Bird ID and timestamp | ✅ Completed |
| 4 | Feature Engineering | Haversine distance, bearing angle, speed, acceleration, turning angle, time features (hour, day, month, season), lag features, rolling features, resting flag | ✅ Completed |
| 8 | Model Evaluation | Full classification metrics (Accuracy, Precision, Recall, F1, ROC-AUC, Confusion Matrix) and clustering quality metrics (Silhouette, Davies-Bouldin, Calinski-Harabasz) evaluated on the Decision Tree best model using 5-fold TimeSeriesSplit | ✅ Completed |
| 9 | Model Interpretation | Feature importance analysis, SHAP values, error analysis, and biological interpretation of model predictions and failures | ✅ Completed |

For Phase 2, 4, 8, and 9 notebooks, outputs, and reports — refer to **Jayant Pandey's folder** in the main repository.

---

*Bird Migration GPS Tracking — Interpretable ML Pipeline | ISI Kolkata IDEAS Internship 2026 | B. Jasvanth, Lendi Institute of Engineering and Technology, Vizianagaram*

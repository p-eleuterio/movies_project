# Kueski Data Scientist Challenge

This project builds a **binary classifier** to predict whether a MovieLens user will give a movie a “high” rating (≥4).  
The core emphasis is on **feature engineering**, **temporal robustness**, and the **integration of heterogeneous data sources**.  
Rather than tuning a single model aggressively, the goal is to demonstrate a complete ML workflow:

- structuring and understanding the data,  
- designing leakage-safe behavioral and temporal features,  
- injecting external metadata,  
- and evaluating the incremental predictive value of each feature family.

The final solution integrates **user behavior**, **movie-level dynamics**, **semantic representations** (Genome), and **external metadata** (TMDB), leading to a robust hybrid model.

---

## Quick start

1. Create and activate the conda environment:

   ```bash
   conda env create -p ./env -f environment.yml
   conda activate ./env
   python -m ipykernel install --user --name kueski-ds --display-name "kueski-ds"
   ```

2. Download the six MovieLens 20M CSVs from Kaggle and place them in `data/raw/`.  
   All intermediate artifacts (temporal datasets, PCA embeddings, TMDB merges) are stored in `data/processed/`.

---

## Notebooks (pipeline overview)

### `00_etl_eda.ipynb`
End-to-end EDA for MovieLens 20M.  
Defines the binary target (≥4), analyzes sparsity, profiles users and movies, and explores Genome Tag distributions.

### `01_f_e_baseline.ipynb`
Baseline feature engineering: user/movie statistics, mean ratings, like rates, counts.  
Establishes the first minimal feature set.

### `02_baseline_model.ipynb`
Trains the initial classifier using a **time-based split** to avoid future leakage.  
Evaluates ROC-AUC, PR-AUC, and F1 to set baseline metrics.

### `03_f_e_genome.ipynb`
Enrichment with **Genome Tags** through PCA (50 components).  
Captures latent semantic dimensions beyond genres.

### `04_f_e_temporal.ipynb`
Builds **temporal features** that respect chronological order:  
decay-weighted means, last-N windows, recent like activity, and temporal movie popularity trends.

### `05_f_e_tmdb.ipynb`
Integrates **TMDB metadata** (budget, revenue, adult flag) via IMDb ID matching.  
Includes cleaning, log-transformations, and missingness indicators.

### `06_mvp_model.ipynb`
Combines all engineered features (baseline + temporal + Genome PCA + TMDB).  
Trains the MVP model and compares it against the baseline using ROC curves, PR curves, and final metrics.

---

## Project layout

- `environment.yml` — reproducible environment spec  
- `data/raw/` — original MovieLens CSVs from Kaggle  
- `data/processed/` — engineered and cached datasets  
- `notebooks/` — full modeling pipeline  
- `src/` — helper utilities and feature engineering functions  
- `data_dictionary.md` — documentation of derived variables  

---

## Modeling target

A high rating is defined as:

```python
is_high_rating = 1 if rating >= 4 else 0
```

All features are designed to be safe for **online inference**, avoiding any future information relative to the rating timestamp.

---

## Final remarks

Across experiments, the most impactful improvements came from:

- **Temporal user behavior** — decay-weighted like rates and recent activity trends were the strongest predictors.
- **Temporal movie dynamics** — recent like rates and short-term trends added meaningful predictive power.
- **Genome PCA embeddings** — captured nuanced semantic structure that genres alone cannot provide.
- **External metadata (TMDB)** — budget, revenue, and adult flags provided small but consistent gains when available.

Overall, combining **internal behavioral signals**, **temporal modeling**, **semantic content**, and **external data sources** yields a significantly stronger model than any single family of features alone.
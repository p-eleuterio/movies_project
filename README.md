# Kueski Data Scientist Take-Home

Starter workspace for the movie-ratings binary classification challenge.

## Project structure
- `environment.yml` — conda spec for reproducible env.
- `data/raw/` — place the six Kaggle CSVs (`genome_scores.csv`, `genome_tags.csv`, `link.csv`, `movie.csv`, `rating.csv`, `tag.csv`).
- `data/processed/` — any cached/intermediate artifacts you create.
- `notebooks/` — exploratory analysis and modeling notebooks.
- `src/` — helper functions (feature engineering, utils, etc.).

## Setup
1) Create the conda env **inside this repo**:
```bash
conda env create -p ./env -f environment.yml
```
2) Activate it:
```bash
conda activate ./env
```
3) Register the kernel for Jupyter (once):
```bash
python -m ipykernel install --user --name kueski-ds --display-name "kueski-ds"
```

## Data download (manual)
Network access is disabled here, so please download the files from the Kaggle dataset manually:
1) Go to the public MovieLens Kaggle dataset page.
2) Download `genome_scores.csv`, `genome_tags.csv`, `link.csv`, `movie.csv`, `rating.csv`, `tag.csv`.
3) Save them into `data/raw/`.

## Data dictionary (MovieLens 20M)
- `rating.csv` (`ratings.csv` on Kaggle)  
  - `userId`: anonymized user identifier (only users with ≥20 ratings kept). citeturn0search14  
  - `movieId`: internal MovieLens movie key; joins to other files. citeturn0search13  
  - `rating`: explicit 5-star score in 0.5 increments, range 0.5–5.0. citeturn0search13  
  - `timestamp`: Unix time in seconds since 1970-01-01 UTC, when the rating was made. citeturn0search7
- `tag.csv` (`tags.csv` on Kaggle)  
  - `userId`: same user key as ratings. citeturn0search13  
  - `movieId`: movie key. citeturn0search13  
  - `tag`: free‑text user-supplied tag. citeturn0search13  
  - `timestamp`: Unix time when the tag was applied. citeturn0search13
- `movie.csv` (`movies.csv` on Kaggle)  
  - `movieId`: movie key. citeturn0search0  
  - `title`: movie title, usually with release year in parentheses. citeturn0search0  
  - `genres`: pipe-delimited list of genres from a fixed set (Action, Adventure, …, Western, `(no genres listed)`). citeturn0search0
- `link.csv` (`links.csv` on Kaggle)  
  - `movieId`: movie key. citeturn0search0  
  - `imdbId`: numeric IMDb identifier for the same movie (no leading zeros). citeturn0search3  
  - `tmdbId`: numeric TMDb identifier for the same movie. citeturn0search3
- `genome_scores.csv`  
  - `movieId`: movie key. citeturn0search1  
  - `tagId`: ID of a genome tag. citeturn0search1  
  - `relevance`: real value in [0,1] measuring how strongly the tag describes the movie. citeturn0search1
- `genome_tags.csv`  
  - `tagId`: tag identifier used in `genome_scores`. citeturn0search1  
  - `tag`: normalized tag string (vocabulary of ~1,100 tags). citeturn0search1

## Getting started
- Launch Jupyter Lab: `jupyter lab`
- Open `notebooks/starter.ipynb` as a template for your EDA and modeling.

## Notes
- The target label is `is_high_rating = 1 if rating >= 4 else 0`.
- Focus on feature engineering that can work for online inference (avoid label leakage from future interactions).

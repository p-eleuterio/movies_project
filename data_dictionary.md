# MovieLens 20M data dictionary

Sources: official MovieLens 20M README (files.grouplens.org). 

- `ratings.csv`  
  - `userId` — anonymized user identifier (consistent across ratings/tags). 
  - `movieId` — MovieLens movie identifier. 
  - `rating` — 5‑star score in 0.5 increments (0.5–5.0). 
  - `timestamp` — seconds since Unix epoch (UTC). 

- `tags.csv`  
  - `userId` — anonymized user identifier (same space as ratings). 
  - `movieId` — MovieLens movie identifier. 
  - `tag` — free‑text tag applied by the user. 
  - `timestamp` — seconds since Unix epoch (UTC). 

- `movies.csv`  
  - `movieId` — MovieLens movie identifier. 
  - `title` — movie title with release year in parentheses. 
  - `genres` — pipe‑delimited list from the predefined genre set. 

- `links.csv`  
  - `movieId` — MovieLens movie identifier. 
  - `imdbId` — IMDb identifier (numeric, no leading zeros). 
  - `tmdbId` — The Movie Database identifier. 

- `genome-scores.csv`  
  - `movieId` — MovieLens movie identifier. 
  - `tagId` — numeric tag identifier from the tag genome. 
  - `relevance` — strength of association between movie and tag (0–1). 

- `genome-tags.csv`  
  - `tagId` — numeric identifier used in `genome-scores.csv`. 
  - `tag` — normalized tag text for the genome vocabulary. 

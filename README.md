# Movies Recommending System

**Live Demo:**  
👉🏻 [Check out the working web app here!](https://moviesrecommendingsystem.streamlit.app/)
  
# Movies Recommender System

A simple Streamlit app that recommends similar movies based on a selected title using precomputed similarity vectors. Posters are fetched from The Movie Database (TMDB) API.

## Overview

- UI: Streamlit (`MRS/app.py`)
- Data artifacts: precomputed pickles for the movie catalog and a similarity matrix
- Poster images: fetched at runtime from TMDB

This repository contains:

- `MRS/app.py` — the Streamlit application
- `MRS.ipynb` — a notebook used to prepare data/artifacts (optional, for regeneration)
- `artifacts/` — example artifact files you can rename/move for the app to run
- `Data/` — original TMDB 5000 dataset CSVs (reference)

## Prerequisites

- Python 3.10+ (tested with 3.12.2)
- pip
- A TMDB API key (free to create at https://www.themoviedb.org/)

## Quickstart (Windows PowerShell)

1. Clone/open the repo and change directory to the project root.

2. Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Install required packages:

```powershell
pip install streamlit pandas requests
```

4. Prepare artifacts expected by the app:

- The app expects these files in the same folder as `MRS/app.py`:
  - `movies_dict.pkl`
  - `similarity.pkl`

If you are starting from the provided `artifacts/` folder:

- Copy/rename `artifacts/movie_list.pk` to `MRS/movies_dict.pkl`
- Copy/rename `artifacts/similarity.pk` to `MRS/similarity.pkl`

Example commands:

```powershell
# From the repo root
Copy-Item .\artifacts\movie_list.pk .\MRS\movies_dict.pkl
Copy-Item .\artifacts\similarity.pk .\MRS\similarity.pkl
```

5. Configure TMDB API access:

- `MRS/app.py` currently contains a hard-coded API key in `fetch_poster(...)`.
- For security, replace that with your own key. For a quick test, you can keep it as-is, but you may hit rate limits or an invalid key.

Optional: If you prefer using an environment variable instead, update `MRS/app.py` to read from `os.environ["TMDB_API_KEY"]`, then set the variable in the current shell:

```powershell
$env:TMDB_API_KEY = "<your_tmdb_api_key>"
```

6. Run the app:

```powershell
cd MRS
streamlit run app.py
```

Streamlit will print a local URL, typically http://localhost:8501. Open it in your browser, pick a movie, and click “Recommend”.

## Repository structure

```
.
├─ MRS.ipynb                # Data prep / artifact generation (optional)
├─ Data/                    # Reference CSVs (TMDB 5000 dataset)
├─ artifacts/               # Example precomputed artifacts to move/rename
│  ├─ movie_list.pk
│  └─ similarity.pk
└─ MRS/
   ├─ app.py                # Streamlit UI and inference
   └─ (your .venv or myenv) # Local virtual environment (not required to be committed)
```

## Troubleshooting

- ModuleNotFoundError: streamlit / pandas / requests

  - Ensure your venv is activated and you installed dependencies: `pip install streamlit pandas requests`.

- FileNotFoundError: movies_dict.pkl / similarity.pkl

  - Confirm the two files exist next to `MRS/app.py` and have exactly those names.
  - If starting from `artifacts/`, copy and rename as shown above.

- Posters aren’t showing

  - Check the API key in `MRS/app.py` or your `TMDB_API_KEY` if you refactored to env vars.
  - TMDB may rate-limit or reject invalid keys.

- Streamlit doesn’t open in browser
  - Visit the printed URL manually (e.g., http://localhost:8501).
  - Check that your firewall allows local connections to port 8501.
  - You can change the port with: `streamlit run app.py --server.port 8502`.

## Notes

- The included `MRS.ipynb` can be used to (re)generate the `movies_dict.pkl` and `similarity.pkl` artifacts. Exact steps may vary depending on the approach you take.
- Pickle files are Python-version dependent; keep runtime consistent between artifact generation and usage if possible.


## Acknowledgements

- TMDB (The Movie Database) for posters and metadata (https://www.themoviedb.org/)
- TMDB 5000 dataset for sample movie data


---

*For more information, refer to the SRS Document: “SRS Document of Movies Recommendation System.doc”.*

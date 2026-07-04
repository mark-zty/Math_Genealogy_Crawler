# Math Genealogy Crawler

Crawls academic records from the [Mathematics Genealogy Project (MGP)](https://www.mathgenealogy.org)
via its API and flattens them into a CSV of mathematicians, their advisors, degree
years, and schools.

See the API docs at https://www.mathgenealogy.org:8000/api/v2/MGP/

## Setup

The crawler authenticates against the MGP API, so you need MGP credentials.

1. Create a file named `credentials.json` in this folder (it is git-ignored, so it
   will not be committed).
2. Put your MGP email and password in it, in this exact JSON format:

   ```json
   {
       "email": "you@example.com",
       "password": "your-mgp-password"
   }
   ```

## Usage

Open and run **`mgp_crawler.ipynb`** (Jupyter notebook). It:

1. Logs in using `credentials.json`.
2. Fetches the range of available MGP IDs.
3. Crawls academic records in chunks and writes them to a tab-delimited CSV.

To crawl, call `write_to_csv` from the notebook, e.g.:

```python
write_to_csv(start=0, stop=300000, file_path='acad.csv')
```

- `start` / `stop` — the MGP ID range to crawl.
- `file_path` — output CSV. The function refuses to overwrite an existing file.

The API helper functions (`login`, `doquery`) live in `mgp.py`.

## Data

A pre-crawled dataset is included: **`acad300k_schools.csv`** (~24 MB, ~300k rows,
tab-delimited). It was produced by the crawler over MGP IDs 0–300000, so you can
work with the data directly without re-running the crawl. Columns:

`ID`, `Family Name`, `Given Name`, `Other Names`, `Advised By`, `Degree Year`, `Schools`

## Files

| File | Purpose |
| --- | --- |
| `mgp_crawler.ipynb` | Main notebook — run this to crawl. |
| `mgp.py` | MGP API helpers (`login`, `doquery`). |
| `acad300k_schools.csv` | Pre-crawled dataset (~300k records, tab-delimited). |
| `credentials.json` | Your MGP login (git-ignored — create it yourself). |

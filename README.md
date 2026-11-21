# Air Quality Analysis in Major Indian Cities — Exploratory Data Analysis

A single Jupyter notebook, `air_quality_eda.ipynb`, that loads five air-quality CSV files, cleans the
daily city-level table, explores it with summary statistics and charts, and saves a cleaned copy.
Coursework submission (data-analysis EDA).

## The problem

Given daily and hourly pollutant readings for several Indian cities, answer the notebook's stated
objectives: load and clean the data, explore it, visualise it, find patterns, and determine the
worst- and best-performing cities by AQI (Air Quality Index).

## Data

All files sit in the repo root (identical copies are also in `Datasets/`; see "Running" below).

| File | Rows | Columns | Granularity |
|---|---|---|---|
| `city_day.csv` | 18,265 | 16 | one row per city per day |
| `city_hour.csv` | 438,245 | 16 | one row per city per hour |
| `station_day.csv` | 36,530 | 17 | one row per station per day |
| `station_hour.csv` | 7,210 | 17 | one row per station per hour |
| `stations.csv` | 10 | 2 | `City`, `Station` lookup |

Row counts are the shapes printed by the notebook's load step.

Shared measurement columns: `City`, `Datetime`, the pollutants `PM2.5, PM10, NO, NO2, NOx, NH3, CO,
SO2, O3, Benzene, Toluene, Xylene`, plus `AQI` and `AQI_Bucket`. The two station files add a `Station`
column. `city_day.csv` spans 2015-01-01 to 2024-12-31 and covers 5 cities: Delhi, Mumbai, Chennai,
Kolkata, Bangalore.

**Source and licence are not recorded in this repo.** Do not assume the files are the public "Air
Quality Data in India" set; see the notes below on how the stored values behave.

## What the notebook does

Ten numbered sections:

1. **Import libraries and setup** — pandas, NumPy, Matplotlib, Seaborn, Plotly; prints library versions.
2. **Load datasets** — reads the five CSVs and prints their shapes.
3. **Data exploration** — dtypes, head and `info()` for each table; missing-value report (none found in
   any of the five).
4. **Data cleaning** (`city_day` only) — parses `Datetime`, derives `Date`/`Month`/`Year`, checks for
   duplicate rows (0 found), and applies forward/back-fill for `AQI` and per-city median imputation for
   pollutants. Since nothing was missing, these fills change no values.
5. **Exploratory analysis** — `describe()`, city list, date range, AQI mean/median/min/max/std.
6. **Visualisations** — AQI trend over time (overall and per city); AQI histogram, density, box and
   violin plots; top-10 most and least polluted cities by mean AQI; pollutant/AQI correlation heatmap;
   PM2.5 vs PM10 scatter (Plotly interactive plus a static Matplotlib version).
7. **Key findings** — worst/best city, ten highest AQI records, average AQI by month, AQI correlations,
   AQI-category distribution, plus extra charts (monthly trend, category pie, city comparison).
9. **Save cleaned dataset** — writes `city_day_cleaned.csv`.
10. **Summary and conclusions**, then a final printed summary.

(The notebook has no section 8; its headings jump from 7 to 9.)

## Results as stored in the notebook's outputs

- Overall mean AQI 251.11, median 251.20, std 144.50, max 500.0.
- Highest mean AQI: Mumbai (253.32). Lowest: Bangalore (249.77) — a gap of about 3.5 AQI points.
- Correlation of AQI with each pollutant is between about -0.003 and 0.011 (e.g. PM2.5 0.001, PM10 0.001,
  NO2 0.011, CO 0.006).
- AQI categories are spread almost evenly: Severe 20.3%, Poor 20.0%, Very Poor 19.9%, Moderate 19.9%,
  Satisfactory 10.0%, Good 9.9%.

### Caveats worth knowing before reading the conclusions

These are observations about what the stored outputs show, not changes to the submission.

- The written conclusions in section 10 describe "strong correlations" between AQI and PM2.5/PM10. The
  notebook's own computed correlations (above) are close to zero, so that sentence is not supported by
  the numbers it printed.
- Near-flat city averages, near-zero correlations, a sharp 0–500 range and a roughly even category split
  are not typical of real monitoring data, and in the first rows `AQI` and `AQI_Bucket` disagree (e.g. AQI
  204.5 labelled "Severe", AQI 411.5 labelled "Moderate"). The data may be synthetic or heavily
  processed; its provenance is unconfirmed.
- Only `city_day` is cleaned and analysed in depth. The hourly and station files are loaded and checked
  for shape and missing values only.

## Running

The notebook reads `city_day.csv` etc. by bare filename, so **launch Jupyter from the repository root**,
not from `Datasets/`.

```bash
pip install pandas numpy matplotlib seaborn plotly jupyter
jupyter notebook air_quality_eda.ipynb
```

Stored outputs were produced with pandas 2.0.3, NumPy 1.26.4, Matplotlib 3.8.4 and Seaborn 0.13.2
(Python 3.10 kernel); the Plotly version was not recorded. Running all cells overwrites
`city_day_cleaned.csv` and replaces the stored outputs, so work on a copy if you want to keep the
submitted state.

## Repository contents

- `air_quality_eda.ipynb` — the analysis.
- `city_day.csv`, `city_hour.csv`, `station_day.csv`, `station_hour.csv`, `stations.csv` — inputs read by
  the notebook; `Datasets/` holds copies of the same five files.
- `city_day_cleaned.csv` — output of section 9.
- `docs/COMMIT_BACKLOG.md` — maintenance notes for this repository.

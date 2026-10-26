# Daily Commit Backlog — DEV-AAT

This repo is **submitted coursework** (an air-quality EDA notebook) and a public portfolio piece.
A scheduled agent takes the **top unchecked item** each time this repo comes up, does it, verifies it,
and commits. Changes must be **additive** — the work was graded.

## Rules

1. One item per run. Finish it or leave it uncommitted.
2. **Allowed:** READMEs, `.gitignore`, `requirements.txt`/environment notes, dataset provenance and
   licence notes, removing clearly accidental junk (`.DS_Store`, `.ipynb_checkpoints/`, duplicate files).
3. **Forbidden:** editing `air_quality_eda.ipynb` code or markdown, re-running it so stored outputs
   change, regenerating `city_day_cleaned.csv`, reformatting submitted source, or anything that alters
   what was assessed. If something looks wrong, record it under "Observations", do not fix it.
4. Verification for doc/additive commits: confirm no executable file changed, and that every command a
   README tells a reader to run was actually run or is plainly correct.
5. Never `git add -A` / `git add .`; stage named paths. Never fabricate a source, licence or result.
6. Conventional commit subject; end with the Co-Authored-By trailer. Tick the item and append to Log.

## Audit facts (verified 2026-10-26)

- Single notebook `air_quality_eda.ipynb` (25 cells, Python 3.10 kernel). Recorded outputs show
  pandas 2.0.3, NumPy 1.26.4, Matplotlib 3.8.4, Seaborn 0.13.2; it also imports Plotly.
- The notebook loads `city_day.csv`, `city_hour.csv`, `station_day.csv`, `station_hour.csv`,
  `stations.csv` from the **repo root** (relative paths) and writes `city_day_cleaned.csv` to the root.
- `Datasets/` holds byte-identical copies (same md5) of the five source CSVs; the root copies are the
  ones the notebook reads. `city_day 2.csv` is byte-identical to `city_day.csv`.
- Row counts: city_day 18,265; city_hour 438,245; station_day 36,530; station_hour 7,210; stations 10.
- No README, `.gitignore`, requirements file, or licence/provenance note exists.
- Tracked junk: `.DS_Store`, `.ipynb_checkpoints/air_quality_eda-checkpoint.ipynb`, `city_day 2.csv`.
- ~109 MB of CSVs are committed (city_hour.csv alone is 46 MB), twice over.

## Queue

- [ ] **B1 — README.md.** Explain the problem, the five datasets and their columns, how to run the
      notebook (from the repo root, since paths are relative), the 10 sections of the notebook, and what
      it outputs. Describe only what the notebook demonstrably does; quote findings only as recorded in
      its stored outputs.
- [ ] **B2 — requirements.txt.** Pin to the versions recorded in the notebook's stored output
      (pandas 2.0.3, numpy 1.26.4, matplotlib 3.8.4, seaborn 0.13.2) plus plotly (version not recorded
      in the notebook — check `import plotly` output / cell 17 metadata before pinning; otherwise leave
      unpinned and say so) and jupyter. Verify by installing into a clean venv and executing the
      notebook to a **scratch copy** (never overwrite the committed one).
- [ ] **B3 — .gitignore + remove accidental junk.** `git rm --cached` `.DS_Store`,
      `.ipynb_checkpoints/`, and `city_day 2.csv` (confirm still byte-identical to `city_day.csv`
      first); add ignore entries for `.DS_Store`, `.ipynb_checkpoints/`, `__pycache__/`, `.venv/`.
- [ ] **B4 — Dataset provenance note.** `Datasets/README.md` or a README section: per-file columns,
      row counts, date range (derive from the files). Source and licence: the files look like the public
      "Air Quality Data in India" set, but that is **unverified here** — a human (VB) must confirm the
      source URL and licence before it is written down. If unconfirmed, record only what is derivable.
- [ ] **B5 — Document the root vs `Datasets/` duplication** in the README (notebook reads root copies;
      `Datasets/` is a byte-identical copy). Do not delete either without VB's decision.

## Observations / needs VB's decision (do not act)

- **`dev` vs `DEV-AAT` overlap.** The `dev` repo also contains `air_quality_eda.ipynb` and the same
  CSV layout (plus `Datasets/`); its notebook differs from this one (not byte-identical) and `dev` has a
  single "first commit". DEV-AAT has the later, extended notebook history. VB to decide which is
  canonical; no repo should be merged or deleted by the agent.
- `station_hour.csv` has only 7,210 rows against 438,245 in `city_hour.csv` and 36,530 in
  `station_day.csv`, which looks truncated relative to the others. Unconfirmed; the notebook only
  inspects it for shape and missing values.
- Committed `city_day_cleaned.csv` has columns `Month, Year, AQI_Category` but no `Date` column, while
  the latest notebook code (cell 9) also derives `Date`. The committed CSV therefore appears to predate
  the final notebook edit. Not regenerated, because that would alter assessed output.
- Notebook cell 4's error message and the `Datasets/` copies suggest the data was reorganised at some
  point; the notebook was never repointed. Left as submitted.
- Large CSVs are in git history; slimming them would need history rewriting and is out of scope.

## Log

2026-10-26 - audit - docs: add commit backlog from repo audit

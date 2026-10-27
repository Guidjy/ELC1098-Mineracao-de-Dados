# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Coursework (UFSM, ELC1098 – Mineração de Dados, assignment T2; spec in `T2_AOM.pdf`) on Age of Mythology unit data. Goal: preprocess the data and classify units by `Class`. Notebook text is in Portuguese; keep that convention.

## Layout

- `main.ipynb` — the whole pipeline (single notebook, no Python modules, no tests, no build/lint).
- `AgeOfMythology_work.csv` — labeled data (has `Class` plus extra columns such as `Cost`).
- `AgeOfMythology_noClass.csv` — unlabeled data to be classified; its columns are the feature schema.
- `.venv/` — local virtualenv (Windows). `requirements.txt` is a `pip freeze` saved as UTF-16 (pip may need it converted to UTF-8 before `pip install -r`). Stack: pandas, numpy, ipykernel/matplotlib-inline.

Run by opening `main.ipynb` with the `.venv` kernel (`.venv\Scripts\Activate.ps1`).

## Data pipeline (as it stands)

The labeled set is aligned to the unlabeled schema:
1. Drop columns present in labeled but absent from unlabeled (except `Class`).
2. Coerce labeled columns to `Int64` wherever the unlabeled column is integer (`pd.to_numeric(errors="coerce")`, round, cast), since the labeled CSV loads them as strings.

Notes from the professor, recorded in the notebook: `LOS` = line of sight; `Bonus` = what the unit is strong against (negative = weak); `Other` = special attribute; `Favor` = secondary resource (unit creation cost).

Open TODOs in the notebook: `Favor` must be extracted from the labeled `Cost` column (which mixes several resources) before dropping `Cost`; handle `Age == 0`. Note the current drop step removes `Cost` too, despite the markdown saying to keep it — reconcile when implementing.

Notebook variable names use the misspelling `dados_labled` / `dados_unlabled`; keep it for consistency.

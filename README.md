# Leakage_Resistant_Elliptic_pp
We revisit how the 55 Elliptic++ address-level features are computed and propose a leakage-resistant pipeline.

# Leakage-resistant Elliptic++ address features

Code and data for the paper "Revisiting Elliptic++: ".

Elliptic++ releases 55 features for 265,354 labelled Bitcoin addresses, with a positional train/test split and features that summarise each address over the whole collection window. This repository recomputes the 55 features from public ledger data with exact definitions, applies a temporal split at block 457,734 (the last block of Elliptic time step 34), and restricts the feature computation process of each training address to its transactions up to that block. It contains the notebooks that build the dataset from the raw sources and reproduce every table and figure in the paper, and the resulting leakage-resistant features.

## Repository layout

| Path | Content |
|---|---|
| `data/raw/` | raw datasets, downloaded by the user (see `data/raw/README.md`) |
| `data/processed/` | intermediate tables written by the notebooks |
| `notebooks/` | the pipeline, run in numerical order, saved with their outputs |
| `outputs/features/` | the leakage-resistant features |
| `outputs/tables/` | the tables of the paper in LaTeX |
| `outputs/figures/` | the figures of the paper in PDF |
| `outputs/paper_numbers.csv` | every number reported in the paper, with the notebook that computes it |

## Data sources

| Source | Provides | Where |
|---|---|---|
| Elliptic++ | labelled addresses, time steps, released features | https://github.com/git-disl/EllipticPlusPlus |
| Deanonymisation map | Elliptic transaction identifier to transaction hash, for 202,804 of 203,769 transactions | https://www.kaggle.com/datasets/alexbenzik/deanonymized-995-pct-of-elliptic-transactions |
| Kondor 2020 release | full Bitcoin ledger up to February 2020 | Dryad, https://doi.org/10.5061/dryad.qz612jmcf |

`data/raw/README.md` lists the nine files needed and where to place them.

## Pipeline

| Notebook | Step | Main outputs |
|---|---|---|
| `00_convert.ipynb` | converts the Kondor files to Parquet | Kondor tables in `data/processed/` |
| `01_link.ipynb` | joins Elliptic++ addresses to the ledger, maps Elliptic transactions to the ledger, derives the block range of each time step, the cutoff block, and the temporal split | address map, Elliptic transactions, time-step blocks |
| `02_features.ipynb` | computes the 55 features from the per-transaction table, once over each address's full history (lifetime set) and once restricted at the cutoff (leakage-resistant set) | `outputs/features/` |
| `03_validate.ipynb` | compares the lifetime set with the released Elliptic++ features | match rates, fee-share check, divergent addresses |
| `04_evaluate.ipynb` | reproduces the Elliptic++ classifiers and measures the effect of the split and the features | reproduction, sensitivity, and leakage tables |
| `05_figures_tables.ipynb` | writes the figures, tables, and `paper_numbers.csv` | `outputs/tables/`, `outputs/figures/` |

## Requirements

Python 3.11, with the packages in `environment.yml` (DuckDB, PyArrow, pandas, NumPy, scikit-learn, Matplotlib).

```bash
conda env create -f environment.yml
conda activate Leakage-Resistant-Elliptic_pp
```

Notebooks `00` to `02` process about 1.2 billion transaction inputs and 1.3 billion outputs. They were run on a node of the Dutch national supercomputer Snellius with 192 threads and 336 GB of memory. The DuckDB settings (threads, memory limit, temporary directory) are set in the first cell of each notebook and can be lowered, at the cost of longer run times and more disk spill.

Notebooks `03` to `05` only read the files written by `02`, so they run on a standard machine once the features exist.

## Reproducing the paper

1. Download the raw data into `data/raw/` as described in `data/raw/README.md`.
2. Create the environment.
3. Run the notebooks in order, from `00_convert.ipynb` to `05_figures_tables.ipynb`.

Random forest results are averaged over ten fixed seeds, and every query that loads data sorts its rows, so reruns give the same numbers.

## The released features

`outputs/features/[...]` holds one row per labelled address matched to the ledger (265,352 addresses), with

- `address`, the Bitcoin address,
- `split`, `train` or `test`, by the address's first appearance,
- the 55 leakage-resistant features, named as in Elliptic++.

The exact definition of each feature is given in the appendix of the paper.

## Licence

The code is released under the MIT licence (`LICENSE`). The recomputed features are released under CC BY 4.0. The ledger data come from the Kondor release, published under CC0 on Dryad. The licit and illicit labels belong to Elliptic++ and are not redistributed here.

## Citation

[...]

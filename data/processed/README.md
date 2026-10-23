# Processed data

Written by the notebooks and not part of the repository.

`00_convert.ipynb` converts the six Kondor files to Parquet, about 100 GB in total.
`01_link.ipynb` to `02_features.ipynb` write the intermediate tables: the address map, the Elliptic transactions in the ledger, the block range of each time step, and the per-transaction table.
`03_validate.ipynb` writes two lists of divergent addresses for '04_evaluate.ipynb'.

Deleting this folder and rerunning the notebooks from `00_convert.ipynb` rebuilds it.

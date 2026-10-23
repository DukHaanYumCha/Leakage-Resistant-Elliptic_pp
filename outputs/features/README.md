# Leakage-resistant features

`notebooks/05_correlations_release.ipynb` writes the released dataset to this folder as
`elliptic_pp_leakage_resistant.parquet`. To use it without running the pipeline, download it from https://drive.google.com/file/d/1wYoqSVz96OIoSd5bqqbuT3kzYIgL-tSU/view?usp=sharing.

## Content

One row per labelled Elliptic++ address found in the Bitcoin ledger, 265,352 addresses in total.

| Column | Content |
|---|---|
| `address` | the Bitcoin address |
| `split` | `train` (172,903 addresses) or `test` (92,449), by the Elliptic time step in which the address first appears |
| 55 feature columns | the leakage-resistant features, named as in Elliptic++ and defined in the appendix of the paper |

Unlabelled addresses are excluded, as are the two labelled addresses whose strings in the Elliptic++ release are truncated and have no ledger record.

The file contains no labels, which belong to Elliptic++. The last cell of `05_correlations_release.ipynb` shows how to attach them from the Elliptic++ wallet file.

## Licence

CC BY 4.0.

## Loading

```python
import pandas as pd

df = pd.read_parquet('outputs/features/elliptic_pp_leakage_resistant.parquet')
print(f'{len(df):,} addresses, {df.shape[1]} columns')
print(df.split.value_counts())
```

Expected output: 265,352 addresses, 57 columns, and 172,903 training and 92,449 test addresses.

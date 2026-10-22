# Raw data

Place the nine files below in the subfolders shown. The notebooks read them from these exact paths.
None of the files is redistributed in this repository.

## Elliptic++ (`elliptic_pp/`)

Download from the links in https://github.com/git-disl/EllipticPlusPlus.
Actors Dataset/wallets_features_classes_combined.csv
Transactions Dataset/txs_features.csv

| Path | Content |
|---|---|
| `elliptic_pp/wallets_features_classes_combined.csv` | labelled addresses, their Elliptic time steps, and the 55 released address features |
| `elliptic_pp/txs_features.csv` | Elliptic transactions and their time steps |

## Deanonymisation map (`kaggle_map/`)

Download from https://www.kaggle.com/datasets/alexbenzik/deanonymized-995-pct-of-elliptic-transactions.

| Path | Content |
|---|---|
| `kaggle_map/elliptic_deanonymized.csv` | Elliptic transaction identifier (`txId`) and transaction hash (`transaction`) |

## Bitcoin ledger, Kondor 2020 release (`kondor/`)

Download the 2020 release from Dryad, https://doi.org/10.5061/dryad.qz612jmcf.
Feb 19, 2021 version files

| Path | Content |
|---|---|
| `kondor/bitcoin_2020_addresses.dat.gz` | address identifier and address string |
| `kondor/bitcoin_2020_txh.dat.gz` | transaction identifier and transaction hash |
| `kondor/bitcoin_2020_bh.dat.gz` | block height, hash, timestamp, and number of transactions |
| `kondor/bitcoin_2020_tx.dat.xz` | transaction identifier, block, numbers of inputs and outputs |
| `kondor/bitcoin_2020_txin.dat.xz` | transaction inputs with address and amount in satoshis |
| `kondor/bitcoin_2020_txout.dat.xz` | transaction outputs with address and amount in satoshis |

The compressed Kondor files take about 60 GB.

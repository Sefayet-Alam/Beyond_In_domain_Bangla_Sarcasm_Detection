# Beyond In-Domain Accuracy

## Cross-Corpus Bengali Sarcasm Detection Under Normalized Exact-Match Control

This repository contains the code and text-free numerical artifacts for the
manuscript *Beyond In-Domain Accuracy: Cross-Corpus Bengali Sarcasm Detection
Under Normalized Exact-Match Control*.

The primary experiment is Notebook 18. It trains 30 BanglaBERT models using
vanilla and Fast Gradient Method (FGM) fine-tuning on three Bengali sarcasm
corpora and five matched seeds, then evaluates 90 source-target cells.

The primary analysis uses:

- normalized exact-match deduplication before splitting;
- fixed stratified 80/10/10 splits with seed 42;
- five training seeds: 42, 1, 7, 123, and 2024;
- macro-F1 as the primary metric;
- source-trained zero-shot cross-corpus evaluation;
- text-free predictions, hashed split manifests, and machine-readable tables.

## Repository layout

```text
00_admin/                         provenance and model links
01_data/                          local data preparation and split manifests
02_notebooks/                     experiment notebooks
03_checkpoints/                   local checkpoints; not required for Notebook 18
04_outputs/finalized_outputs/    figures and finalized numerical tables
04_outputs/predictions/18_multiseed_cross_corpus/
                                   90 text-free primary prediction files
```

Source corpora are not redistributed by this repository. Obtain them from
their original publishers and follow their licenses. Place local source files
according to `01_data/Readme.md` before running the data-preparation notebook.

## Primary experiment

Run from the repository root:

```text
02_notebooks/01_data_prep_clean_dedup_splits.ipynb
02_notebooks/18_reviewer_ready_multiseed_cross_corpus.ipynb
```

Notebook 18 uses `csebuetnlp/banglabert`, a native sequence-classification
head, maximum sequence length 128, learning rate 2e-5, batch size 32, up to
8 epochs, early stopping patience 2, and FGM epsilon 0.5.

The authoritative result files are:

```text
04_outputs/finalized_outputs/tables/18_transformer_cross_corpus_multiseed_runs.csv
04_outputs/finalized_outputs/tables/18_transformer_cross_corpus_multiseed_summary.csv
04_outputs/finalized_outputs/tables/18_fgm_vs_vanilla_paired_seed_tests.csv
04_outputs/finalized_outputs/tables/18_fixed_target_seedwise_sensitivity.csv
04_outputs/finalized_outputs/tables/18_fixed_target_summary.csv
```

## Data protection

Do not commit raw comments, cleaned corpus files, processed corpus files,
prediction files containing a `text` or `comments` column, API caches, API
responses, `.env` files, or model-service credentials.

The public prediction artifacts contain labels, hashes, logits, probabilities,
system identifiers, source/target identifiers, and seeds, but no comment text.

## Reproducibility

The reported results are conditional on the frozen corpus splits. Student-t
intervals summarize variation over the five training seeds; they do not measure
uncertainty from redrawing the corpus splits or collecting new annotations.

The repository code is released under the license in `LICENSE`. Dataset files
are not relicensed by this repository and remain governed by the terms of their
original publishers.
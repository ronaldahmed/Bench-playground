# Bench-playground

Datasets for spreadsheet and table benchmark work.

## Contents

| Path | Size | What |
|---|---|---|
| `deepnlz-ds-instruct-500k/` | 245 MB (LFS) | Instruction-tuning set, 26,202 examples, zstd parquet |
| `sheetbench/` | 98 MB | 62 `.xlsx` workbooks + case/question JSONs across 4 case types |
| `tablebench/` | 16 MB | 5 `.jsonl` splits (TQA + DP/TCoT/SCoT/PoT instruct) |
| `stateval/` | 11 MB | Statistical reasoning benchmark, 1,900 questions in 2 tracks |
| `docs/` | 40 KB | Benchmark comparison matrix (docx + xlsx) |

Each dataset directory has a `SOURCE.md` (or `README.md`) recording where it
came from and under what terms.

`stateval/foundational_test.jsonl` is normalized rather than a verbatim mirror;
`stateval/SOURCE.md` records the three changes and the before/after hashes.

## Cloning

Large binaries — the parquet shards and the four oversized workbooks in
`sheetbench/large_cases/large_cases_xlsx/` — are stored in Git LFS, about
340 MB in total.

```bash
git clone git@github.com:ronaldahmed/Bench-playground.git
```

To skip the LFS payload and fetch it selectively later:

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone git@github.com:ronaldahmed/Bench-playground.git
cd Bench-playground
git lfs pull --include="deepnlz-ds-instruct-500k/*"
```

This matters because GitHub's free LFS tier allows 1 GB of bandwidth per month,
so a full clone consumes roughly a third of it.

## Note on `sheetbench` paths

The `File` fields inside the sheetbench case JSONs use the upstream directory
naming, including `sheetbench/manipulation cases/` with a space, whereas the
directory on disk is `manipulation_cases`. Normalize when resolving paths.

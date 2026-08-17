# deepnlz-ds-instruct-500k

Instruction-tuning dataset, 26,202 examples, single `train` split.

## Format

Stored as 4 zstd-compressed parquet shards. The dataset originally lived on disk
as 3 uncompressed `.arrow` shards totalling ~1.2 GB, which exceeds GitHub's
100 MB per-file limit; the parquet copies total 245 MB and each shard stays
under the limit.

The conversion was verified lossless: an MD5 over the canonical JSON of every
row, streamed in order, is identical for the arrow source and the reloaded
parquet (`f002346d55a9d57e4e6ab00f218b91e3`, 26,202 rows both sides), with no
schema drift.

The parquet files are stored via Git LFS.

## Loading

```python
from datasets import load_dataset

ds = load_dataset(
    "parquet",
    data_files="deepnlz-ds-instruct-500k/train-*.parquet",
    split="train",
)
```

## Schema

| Field | Type |
|---|---|
| `id` | int64 |
| `messages` | list of `{role: string, content: string}` |
| `input_tokens` | int64 |
| `output_tokens` | int64 |
| `total_tokens` | int64 |
| `evaluation` | `{difficulty: int64, quality: int64, ability: list[string]}` |

`dataset_info.json` is carried over from the original arrow build for
provenance. Its `download_checksums` path and `_data_files` entries refer to the
superseded arrow layout, not to the parquet shards.

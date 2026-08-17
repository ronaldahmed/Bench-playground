# StatEval — provenance

Upstream: <https://huggingface.co/datasets/StatAILab/StatEval>
Snapshot taken from revision `0e2d28b99fa4662f5016f70a2ca7abcecee5cac7`
(upstream last modified 2026-07-11). `README.md` here is the upstream dataset
card, carried over verbatim.

License: **MIT**, as declared on the upstream dataset card.

1,900 questions in two tracks: `foundational_test.jsonl` (1,000 textbook- and
exam-style problems) and `research_test.jsonl` (900 = 300 research problems ×
easy/medium/hard variants, drawn from 134 papers).

## Modifications from upstream

`research_test.jsonl` is **unmodified**; its sha256 matches upstream. It has no
`id` or `test_id` column, so the changes below do not apply to it.

`foundational_test.jsonl` has been normalized. Upstream had a non-uniform schema
that broke type inference on load:

1. **Dropped the `id` column.** It was a source-local problem number, not a key
   — it collided across sources, and its type was inconsistent: 996 rows had
   ints, while 4 rows sourced from *Bayesian Reasoning and Machine Learning*
   carried `chapter.exercise` strings (`"1.5"`, `"13.3"`, `"9.7"`, `"21.3"`).
2. **Renamed `test_id` to `id`.** It is the real primary key: int, unique,
   0–999, equal to the line index.
3. **Line 801 was missing `data_quality` and `source`** — the only such row of
   1,000. Both are now explicit `null`, so all 1,000 rows share one schema.

No other field was altered; the transform verified field-by-field equality
against the upstream file for everything outside those changes.

| File | sha256 |
|---|---|
| `foundational_test.jsonl` upstream | `4c5ab3e585ef6b92c685ac70654eb3bf4c3763977ef1930b9d7e510550021a02` |
| `foundational_test.jsonl` as committed | `aa6dc21a9bb5b1ee388d4a56979af3621353922409e07b0bf307e6cf3a7aaf10` |
| `research_test.jsonl` (unmodified) | `e3e70e94e761965ae22c01a36ac5945f120a4c5993ae2a57d86081a9fb3c6c38` |

## Schema

`foundational_test.jsonl` — `id`, `type`, `question`, `answer`,
`detailed_solution`, `data_quality`, `source`, `final_check`, `check_reason`.

`research_test.jsonl` — `group_id`, `question`, `proof`, `external_lemma`,
`difficulty`, `theorem_name`, `result_category`, `direction_category`,
`used_lemmas`, `document_title`, `final_check`. Note that `group_id` runs 1–300
with three difficulty variants per group, so it is not a per-row key.

## Loading

```python
from datasets import load_dataset

foundational = load_dataset("json", data_files="stateval/foundational_test.jsonl", split="train")
research     = load_dataset("json", data_files="stateval/research_test.jsonl", split="train")
```

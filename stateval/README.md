---
language:
  - en
  - zh
license: mit
tags:
  - statistics
  - reasoning
  - math
  - evaluation
  - benchmark
pretty_name: StatEval
---

# StatEval: A Statistical Reasoning Evaluation Benchmark

StatEval is a comprehensive benchmark designed to evaluate the rigorous statistical reasoning capabilities of large language models, spanning from fundamental academic knowledge to frontier research-level problems.

## Dataset Structure

This repository hosts the complete StatEval test set, containing 1,900 questions across two tracks:

- `foundational_test.jsonl` (1,000 questions): The complete test set for the Foundational Track. It evaluates mastery of statistical concepts through textbook- and exam-style problems across undergraduate and graduate levels, with an emphasis on proofs and complex calculations in Probability, Statistics, and Machine Learning.
- `research_test.jsonl` (900 questions): The complete test set for the Research Track. It assesses multi-step, formal reasoning on frontier research tasks derived from top-tier statistical journals (2000–2025). It consists of **300 unique research problems**, with each problem presented in three difficulty variants (Easy, Medium, and Hard) based on the degree of autonomous lemma discovery required.

**Data last updated:** July 10, 2026.

## Full Training Dataset Access

The updated paper detailing the full methodology and data distribution is currently in progress.

To request access to the complete training dataset, please contact: zhoufan@mail.shufe.edu.cn

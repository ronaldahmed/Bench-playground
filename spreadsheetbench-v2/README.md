---
license: mit
---

# SpreadsheetBench 2

[Home Page](https://spreadsheetbench.github.io/)

SpreadsheetBench 2 is a benchmark for evaluating agents on end-to-end business spreadsheet workflows.
Unlike existing benchmarks that focus on isolated manipulations, SpreadsheetBench 2 requires agents to
(1) complete workflow-level goals through multi-step coordinated operations,
(2) perform cross-sheet reasoningwithin complex multi-sheet workbooks,
(3) produce deliverable-level outcomes including structured models, repaired spreadsheets, and accurate visualizations.

## Key Features
1. End-to-End Workflows: Tasks are designed as self-contained, multi-stage objectives requiring sequences of coordinated spreadsheet operations, rather than atomic formula generation or local edits.
2. Professional Financial Domain: Covers real business scenarios including financial modeling with multi-statement integration, systematic error debugging across 10 error types, and data visualization.
3. Complex Workbook Structures: Tasks involve workbooks with numerous sheets per question andrequire extensive cell modifications. Debugging tasks require hundreds of cell edits on average, and financialmodeling tasks require over a thousand.

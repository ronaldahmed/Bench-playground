---
language:
- en
license: apache-2.0
pretty_name: TableBench
size_categories:
- n<1K
task_categories:
- question-answering
task_ids: []
tags:
- table-question-answering
configs:
- config_name: table_bench
  data_files:
  - split: TQA_test
    path: 'TableBench.jsonl'
  - split: Instruct_test
    path: 
    - 'TableBench_DP.jsonl'
    - 'TableBench_TCoT.jsonl'
    - 'TableBench_SCoT.jsonl'
    - 'TableBench_PoT.jsonl'
---

# Dataset Card for TableBench

<p align="left">
  <a href="https://arxiv.org/abs/2408.09174">📚 Paper</a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://tablebench.github.io/">🏆 Leaderboard</a>   
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/TableBench/TableBench">💻 Code</a>
</p>

## Dataset Summary
<code style="color:#8b44c7"><b>TableBench</b></code> is a <b>comprehensive</b> and <b>complex</b>
                benchmark designed to evaluate Table
                Question Answering (TableQA) capabilities, aligning closely with the "<code style="color:#8b44c7"><b>Reasoning Complexity of
                Questions</b></code>" dimension in real-world Table QA scenarios. It covers <b>18</b> question
                categories
                across <b>4</b> major ategories—including <b>Fact Checking</b>, <b>Numerical Reasoning</b>, <b>Data
                  Analysis</b>, and <b>Visualization</b>—with <b>886</b> carefully curated test cases. TableBench
                substantially pushes the boundaries of large language models in complex TableQA scenarios.

## Latest Version
> **🔥TableBench-2025-04-18🔥** 
>
> 1. **☀️ Enhanced TableBench**:
>  We’ve released an cleaner version of TableBench, after thoroughly reviewing all test set cases and correcting any errors we identified. Please download the latest version of TableBench for the most accurate dataset.
>
> 2. **🚀 Brand New Leaderboard**:
> The brand new [Leaderboard](https://tablebench.github.io/) is now live! We've included the performance of many newly released models in our latest leaderboard and will continue to keep it up to date. Submissions are welcome! For submission guidelines, please refer to the `Submission section` on [Leaderboard](https://tablebench.github.io/) website.
>
> 3. **🔍 Refined Evaluation Metrics**:
> In response to community feedback and in-depth discussions, we've updated the evaluation metrics for Fact Checking, Numerical Reasoning, and Data Analysis. You can find the detailed specifications of these new metrics and evaluation tools on our [github repo](https://github.com/TableBench/TableBench)

## Data Introduction
Our dataset has two parts:

- **[TQA_test] Original Table QA Test Set (`TableBench.jsonl`)**: This serves as the core benchmark data, suitable for evaluating specialized reasoning capabilities in TableQA systems.

- **[Instruct_test] Pre-designed Instruction Test Set with Various Reasoning Methods (`TableBench_DP.jsonl`, `TableBench_TCoT.jsonl` ,`TableBench_SCoT.jsonl` and `TableBench_PoT.jsonl` )**: Derived from the original paper, this version includes diverse reasoning instructions and is more suitable for assessing the reasoning abilities of large language models (LLMs) on table-based QA tasks.

These two formats focus on different evaluation aspects. This design aims to enhance the dataset's flexibility and scalability. Both versions are maintained and provided in the repository.


## Data Fields (TQA_test)

| ID | String | Description |
|----|--------|-------------|
| id | string | Unique Identifier |
| qtype | string | Question Type (FactChecking, NumericalReasoning, DataAnalysis, Visualization) |
| qsubtype | string | Question Subtype |
| table | string | Table |
| question | string | Question |
| answer | string | Answer |
| chart_type | string | Only Valid for Evaluating Chart Generation Task |


## Data Example (TQA_test)

An example of `TableBench.jsonl` looks as follows:
```
{
    "id": "60670a8d9b1e39dd845fb1639d0d8b86",
    "qtype": "DataAnalysis",
    "qsubtype": "StatisticalAnalysis",
    "table": {"columns": ["rank", "circuit", "headquarters", "screens", "sites"], "data": [[1, "regal entertainment group", "knoxville , tn", 7367, 580], [2, "amc entertainment inc", "kansas city , mo", 5894, 483], [3, "cinemark theatres", "plano , tx", 3895, 298], [4, "carmike cinemas , inc", "columbus , ga", 2242, 232], [5, "cineplex entertainment", "toronto , on", 1438, 133], [6, "rave motion pictures", "dallas , tx", 939, 62], [7, "marcus theatres", "milwaukee , wi", 687, 55], [8, "national amusements", "dedham , ma", 450, 34], [9, "empire theatres", "stellarton , ns", 438, 53]]},
    "question": "Can you calculate the standard deviation of the number of screens operated by the top 5 movie theater chains?",
    "answer": "2472.33",
}
```

## Data Fields (Instruct_test)

| ID | String | Description |
|----|--------|-------------|
| id | string | Unique Identifier |
| qtype | string | Question Type (FactChecking, NumericalReasoning, DataAnalysis, Visualization) |
| qsubtype | string | Question Subtype |
| instruction | string | Instruction to prompt LLM |
| instruction_type | string | four different instruction types in TableBench: DP(Direct Prompting), TCoT(Textual Chain of Thought),SCoT(Symbolic Chain of Thought) and PoT(Program of Thought) |
| table | string | Table |
| question | string | Question |
| answer | string | Answer |
| chart_type | string | Only Valid for Evaluating Chart Generation Task |

## Data Example (Instruct_test)
An example of 'TableBench_PoT.jsonl' looks as follows:
```
{
    "id": "60670a8d9b1e39dd845fb1639d0d8b86",
    "qtype": "DataAnalysis",
    "qsubtype": "StatisticalAnalysis",
    "instruction": "You are a data analyst proficient in Python ...",
    "instruction_type": "PoT",
    "table": {"columns": ["rank", "circuit", "headquarters", "screens", "sites"], "data": [[1, "regal entertainment group", "knoxville , tn", 7367, 580], [2, "amc entertainment inc", "kansas city , mo", 5894, 483], [3, "cinemark theatres", "plano , tx", 3895, 298], [4, "carmike cinemas , inc", "columbus , ga", 2242, 232], [5, "cineplex entertainment", "toronto , on", 1438, 133], [6, "rave motion pictures", "dallas , tx", 939, 62], [7, "marcus theatres", "milwaukee , wi", 687, 55], [8, "national amusements", "dedham , ma", 450, 34], [9, "empire theatres", "stellarton , ns", 438, 53]]},
    "question": "Can you calculate the standard deviation of the number of screens operated by the top 5 movie theater chains?",
    "answer": "2472.33"
}
```

## Data Usage
- If you wish to assess the capabilities of LLMs on tabular data, you can utilize `TableBench-DP.jsonl`, `TableBench-TCoT.jsonl`, `TableBench-SCoT.jsonl`and `TableBench-PoT.jsonl` to evaluate the model's abilities directly. Detailed performance comparisons can be found on the [**live-updated leaderboard**](https://tablebench.github.io/).
- If you wish to evaluate your holistic approach on TableBench, please directly use `TableBench.jsonl`. There is no need to adopt any predefined prompt set. You can run the evaluation using the tools provided in our [**GitHub**](https://github.com/TableBench/TableBench) repository. To submit your results to the [**Leaderboard**](https://tablebench.github.io/), please follow the submission instructions provided on the leaderboard website.

## Historical versions
**Note：** It is strongly recommended to use the **latest version** of the dataset, as it provides the most **up-to-date** leaderboard results and improved data quality.

> **2024-08-29：**
> [TableBench-2024-08-29](https://huggingface.co/datasets/Multilingual-Multimodal-NLP/TableBench/tree/90593ad8af90f027f6f478b8c4c1981d9f073a83) can be downloaded here，which corresponds to the version used in our [paper](https://arxiv.org/abs/2408.09174).

## Citation
If you use the data from this project, please cite the original paper:
```
@inproceedings{wu2025tablebench,
  title={Tablebench: A comprehensive and complex benchmark for table question answering},
  author={Wu, Xianjie and Yang, Jian and Chai, Linzheng and Zhang, Ge and Liu, Jiaheng and Du, Xeron and Liang, Di and Shu, Daixin and Cheng, Xianfu and Sun, Tianzhen and others},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence},
  volume={39},
  number={24},
  pages={25497--25506},
  year={2025}
}
```
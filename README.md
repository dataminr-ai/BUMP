# BUMP: A Benchmark of Unfaithful Minimal Pairs for Meta-Evaluation of Faithfulness Metrics

This repo contains the dataset proposed in our paper [BUMP: A Benchmark of Unfaithful Minimal Pairs for Meta-Evaluation of Faithfulness Metrics](https://aclanthology.org/2023.acl-long.716/).

## Dataset
![](figures/hook.png)

Example from BUMP dataset. An annotator constructs an unfaithful summary containing an *Extrinsic Entity Error* by replacing the word `homegrown` in the reference summary with the word `foreign`. The reference and edited summary form a minimal unfaithful summary pair. Faithfulness metrics are evaluated on both the reference and edited summary and compared to measure whether the metric is consistent, e.g., in this example, **QuestEval** and **CoCo** are consistent, while **FactCC** is not.

Two annotation tasks are designed for BUMP, where Task 1 is taxonomy-based (a specific error type is required for the edited summary), and Task 2 allows freestyle edits (i.e., no error type constraints are imposed).
### Task 1
For Task 1, we randomly select 100 article-summary pairs from the test set of the CNN/DailyMail dataset. Each pair is then annotated following the error taxonomy below:
#### Taxonomy

|Error Type|Description|
|---|---|
|Predicate Error|The predicate in the summary is inconsistent with the source article.|
|Entity Error|The subject/object of a predicate is inconsistent with the source article.|
|Circumstance Error|Time, duration, or location of an event of the predicate is wrong.|
|Coreference Error|A pronoun/reference with wrong or nonexistent antecedent.|
|Intrinsic Error|Error derived from information within the source article.|
|Extrinsic Error|Error contains information not present in the source article.|

### Task 2
For Task 2, we select an additional 100 random article-summary pairs from the CNN/DailyMail dataset and each pair is annotated in freestyle edits.

## Statistics
BUMP dataset statistics

|              |           | Task 1 | Task 2 |
|--------------|-----------|:------:|:------:|
| Predicate    | Intrinsic |  116   |   17   |
|              | Extrinsic |   76   |   28   |
| Entity       | Intrinsic |  128   |   28   |
|              | Extrinsic |  115   |   62   |
| Circumstance | Intrinsic |   82   |   22   |
|              | Extrinsic |   78   |   33   |
| Coreference  | -         |   98   |   1    |
| Other        | -         |   0    |   5    |
| Total        |           |  693   |  196   |

## Meta-Evaluation
### Consistency Evaluation
![](figures/consistency.png)
**Consistency (%) of faithfulness evaluation metrics**. `BART`: `BARTScore`, `QAFaEv`: `QAFactEval`, `BERT`: `BERTScore`, `QuEv`: `QuestEval`, `R-2`: `ROUGE-2`. All values are color-coded. For each row, `* (p < 0.05)` and `** (p < 0.01)` indicate the results are statistically significant when comparing the best to the second-best metric. 

### ROC AUC Evaluation
![](figures/AUC_ROC.png)
**ROC AUC (%) of faithfulness evaluation metrics**. `BART`: `BARTScore`, `QAFaEv`: `QAFactEval`, `BERT`: `BERTScore`, `QuEv`: `QuestEval`, `R-2`: `ROUGE-2`. All values are color-coded. For each row, `* (p < 0.05)` and `** (p < 0.01)` indicate the results are statistically significant when comparing the best to the second-best metric. 


## Citation:
If you find the data in this repo helpful, please cite [our paper](https://aclanthology.org/2023.acl-long.716/):
```
@inproceedings{ma-etal-2023-bump,
    title = "{BUMP}: A Benchmark of Unfaithful Minimal Pairs for Meta-Evaluation of Faithfulness Metrics",
    author = "Ma, Liang  and
      Cao, Shuyang  and
      Logan IV, Robert L  and
      Lu, Di  and
      Ran, Shihao  and
      Zhang, Ke  and
      Tetreault, Joel  and
      Jaimes, Alejandro",
    booktitle = "Proceedings of the 61st Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)",
    month = jul,
    year = "2023",
    address = "Toronto, Canada",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.acl-long.716",
    pages = "12788--12812",
    abstract = "The proliferation of automatic faithfulness metrics for summarization has produced a need for benchmarks to evaluate them. While existing benchmarks measure the correlation with human judgements of faithfulness on model-generated summaries, they are insufficient for diagnosing whether metrics are: 1) consistent, i.e., indicate lower faithfulness as errors are introduced into a summary, 2) effective on human-written texts, and 3) sensitive to different error types (as summaries can contain multiple errors). To address these needs, we present a benchmark of unfaithful minimal pairs (BUMP), a dataset of 889 human-written, minimally different summary pairs, where a single error is introduced to a summary from the CNN/DailyMail dataset to produce an unfaithful summary. We find BUMP complements existing benchmarks in a number of ways: 1) the summaries in BUMP are harder to discriminate and less probable under SOTA summarization models, 2) unlike non-pair-based datasets, BUMP can be used to measure the consistency of metrics, and reveals that the most discriminative metrics tend not to be the most consistent, and 3) unlike datasets containing generated summaries with multiple errors, BUMP enables the measurement of metrics{'} performance on individual error types.",
}
```

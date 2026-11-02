# Real-data evaluation — 2026-11-02

Input: `House/1632300362534233.csv`. Dataset SHA-256: `fbf022a1cad47163cef93b0b60bc7beddc8258b90f227aea2eab6d76544f70fd`.

Model selection used only training-fold CV. One final holdout was reserved before preprocessing. The full CV leaderboard, dependency versions, seed, feature schema and split sizes are in [experiments/report.json](experiments/report.json).

- Model: **ExtraTreesRegressor**
- Training rows: **2789**; holdout rows: **690**
- Selection metric: `neg_mean_absolute_error`; selected CV score: **-1503431922.103744**
- Dummy baseline CV score on the same folds: **-4546520434.055565**
- Five CV folds; seed 42; tuning: **True**
- Identical raw predictor rows grouped: **True**

| Metric | Holdout value |
|---|---:|
| mae | 1776991450.677283 |
| rmse | 5161079437.763136 |
| r2 | 0.626660 |


## Dataset-specific interpretation

Price(USD) and price-per-meter leakage are excluded. Comma-separated Area is parsed and nonpositive area is treated as missing. Identical raw predictor rows are grouped even when prices differ. MAE/RMSE retain the original Price-column units; the currency unit was not independently verified. No target-based outlier pruning is applied. This random historical holdout does not establish current market prices.

## Reproduce

Activate an environment with the project's requirements, change to the repository root, and run:

```cmd
python -m mlproject train --data "D:\data\House\1632300362534233.csv" --output artifacts --folds 5 --seed 42 --tune
```

Results were obtained with the dependency versions recorded in the JSON report. Different versions can change results slightly. Negative MAE selection scores are higher-is-better. CV scores are selection estimates and optimistic; the holdout is the final internal result. Hyperparameter tuning is enabled on the smaller datasets and diabetes; for credit, soccer, student and churn the default bounded candidate comparison is used. Scores are not directly comparable across datasets or tasks.

Do not tune against the now-observed holdout or claim improvement over the legacy notebooks: leakage, split policies and preprocessing differ. Raw data, row-level predictions and trained pickle artifacts are not included in this evidence commit.

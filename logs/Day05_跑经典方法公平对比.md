# Day 05 跑经典方法，公平对比

> 定位：Isolation Forest 是 ADERH 的经典隔离对照；LOF、kNN、OCSVM 提供其他机制参照。

## 做了什么

- 运行 `src/run_day05_baselines.py` 和 `src/check_day05_score_direction.py`，在固定 `split_v1` 和训练集拟合的标准化下计算四种方法的连续分数、AP、ROC-AUC 和本机耗时；所有输出统一为“越大越异常”。

## 结果

| 方法 | 运行数 | ROC-AUC | AP | 拟合(s) | 评分(s) |
|---|---:|---:|---:|---:|---:|
| Isolation Forest | 5 | 0.997083 ± 0.000178 | 0.976866 ± 0.001822 | 1.2710 | 0.3915 |
| One-Class SVM | 1 | 0.883284 | 0.375004 | 10.8117 | 4.3575 |
| kNN mean distance | 1 | 0.713937 | 0.192808 | 0.1049 | 2.4885 |
| Local Outlier Factor | 1 | 0.556667 | 0.134447 | 5.9781 | 2.4616 |

## 判断

我原本倾向于认为 kNN/LOF 会比较有竞争力——Day 4 的 9 维距离没有看到严重集中。但它们的 AP 只有 0.1928、0.1344，虽高于异常基率 0.0702，却远低于 Isolation Forest。所以我把 Day 4 的判断修正为“距离仍有对比度，不代表邻域密度与派生异常标签一致”，这给 Day 6 和 Day 12 留下真正要解释的问题。

## 追踪

- run_id：8 个 Day 05 run，见 `registry/experiments.csv`。
- 证据：`results/aggregated/day05_classic_baselines.csv`、`score_direction_check.json`。
- 下一步：Day 6 运行 PCA 重构分数，比较 kNN/LOF 在 9 维与 PCA(6) 下的表现与效率。

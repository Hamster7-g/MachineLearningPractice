# Day 04 探索数据，提出异常假设

> 定位：在训练集上不带标签做探索；提出的假设之后可能被实验推翻，不是 ADERH 已经赢了的证据。

## 做了什么

- 运行 `figures/gen_fig_day04_eda.py`，对 29,402 条训练记录计算描述统计、Spearman 相关、2/4/6/9 维距离诊断和 PCA 解释方差；异常标签全程未参与。

## 结果

- `feature_04`、`feature_06` 长尾明显，偏度绝对值分别 66.85、41.67。
- 最大绝对 Spearman 相关 0.799（`feature_05` 与 `feature_08`，负相关）。
- 前 6 个主成分累计解释 99.9806% 方差；前 2 个仅 52.88%，二维图不能替代正式空间。
- 9 维随机点对距离 CV 0.7905、相对对比度 3.4546，暂未看到严重距离集中。

## 判断

PCA 二维图有清楚的分支和远点，很容易凭视觉直接说“这些就是异常”，但图中没有用标签，且二维只覆盖约一半方差。所以我把这种直觉整理成一个待 Day 7 检验的 DBSCAN 参数敏感性假设，并写成可证伪的形式。先隐藏标签能减少“看见答案后解释数据”的风险。

## 追踪

- run_id：`day04_eda_train_split_v1`。
- 证据：`evidence/Day04/descriptive_stats.csv`、`distance_diagnostics.csv`、`pca_explained_variance.csv` 和三组图。
- 下一步：Day 5 运行 Isolation Forest、kNN、LOF、One-Class SVM，检验结构判断能否转化为排序效果。

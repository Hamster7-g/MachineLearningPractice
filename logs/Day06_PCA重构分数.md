# Day 06 PCA 重构分数

> 定位：PCA 的重构与降维结果用来解释数据的几何结构，是讨论 ADERH 结果的背景，不算对 ADERH 机制的消融。

## 做了什么

- 运行 `src/run_day06_pca.py` 和 `figures/gen_fig_day06_pca.py`；只在训练数据上拟合 PCA，用测试样本的重构均方误差作连续分数，并比较 kNN/LOF 在 9 维与 PCA(6) 下的表现。

## 结果

- PCA(5) 重构：ROC-AUC 0.791248，AP 0.356048；PCA(6) 重构：ROC-AUC 0.524147，AP 0.090334。
- kNN 9D→PCA(6)：AP 0.192808→0.191450，评分 3.698s→0.486s。
- LOF 9D→PCA(6)：AP 0.134447→0.136431，拟合 7.886s→1.277s，评分 3.269s→0.504s。

## 判断

我原本以为 PCA(6) 保留 99.98% 方差，重构误差至少不会比 PCA(5) 差太多；实际 AP 从 0.356 降到 0.090，分数方向和分布都已核验不是代码错误。原因在于 PCA 重构检测看的是被丢弃的方向：PCA(5) 把约 10.53% 方差的第 6 主成分留在残差里，PCA(6) 只剩三个合计约 0.019% 的方向，保留更多信息反而消掉了可用于排序的残差信号。“解释方差保留越多、异常检测越好”在本数据上被明确反驳。

## 追踪

- run_id：6 个 Day 06 run，见 `results/aggregated/day06_pca_comparison.csv`。
- 证据：`configs/day06_pca.yaml`、`evidence/Day06/pca_config.csv`、`pca_test_scores.csv`。
- 下一步：Day 7 用 k-distance 设置 DBSCAN 参数网格，检验多密度条带是否导致噪声集合不稳定。

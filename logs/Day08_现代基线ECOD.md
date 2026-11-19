# Day 08 现代基线 ECOD

> 定位：ECOD 用逐维尾概率做对照，检验 ADERH 的联合几何评分会不会给出不同排序；它不是另一个重点新方法。

## 做了什么

- 运行 `src/run_day08_modern.py`，在 `split_v1` 和相同标准化下调用 `pyod==3.6.6` 的 ECOD，`contamination=0.1`、`n_jobs=-1`，确定性运行。

## 结果

- ECOD：ROC-AUC 0.993067，AP 0.910299；单次拟合约 9.35s、评分约 0.108s。
- 这是强基线，但仍低于 Isolation Forest 五种子均值（ROC-AUC 0.997083、AP 0.976866）。

## 判断

我最初担心现代方法会完全压住经典基线，实际没有：随机隔离最好、边缘尾概率紧随其后、局部邻域明显较弱。ECOD 的 `decision_function` 会把训练集和当前测试批次拼接后计算经验秩，未用测试标签，但测试样本之间会互相影响分数，所以“可逐条部署”不成立，这不妨碍批量离线比较。PyOD 文档说明 ECOD 是 COPOD 的完善版本并建议优先使用，再跑 COPOD 对问题帮助有限，故不加入。

## 追踪

- run_id：`day08_ecod_seeddeterministic_split_v1`。
- 证据：`results/aggregated/day08_modern_baselines.csv`、`environment.txt`。
- 下一步：Day 9 用 ADERH 官方实现做一次不进入主表的小规模完整数据流试跑。

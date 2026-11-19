# Day 09 ADERH 小规模试跑

> 定位：这天只确认 ADERH 的正式实现能在项目数据流里跑起来，试跑结果不进入正式的效果与效率结论。

## 做了什么

- 运行 `src/run_day09_frontier_smoke.py`，从训练/测试索引无标签抽取 5,000/2,000 条，以 32 个集成成员、`n=18`、`contamination=0.1`、种子 0 完成一次小规模拟合和评分。

## 结果

- 返回 2,000 个有限 `float64` 分数，范围约 0.0149–1.0；拟合约 1.33s、评分约 0.48s，`tracemalloc` 峰值约 7.17MB（不覆盖全部底层内存，不作严格内存结论）。
- 输出形状、类型、有限性和方向通过，试跑结果未进入 `results/final/`。

## 判断

决定 **GO**：Day 10 用完整 29,402/12,345 拆分、256 个估计器和种子 0–4。若单种子超过 10 分钟、出现非有限分数或维度错误就原样停止记录，不用缩小版冒充正式结果。这里最容易犯的错误是看到试跑指标不错就提前写成方法表现，所以 `performance_evidence` 明确设为 `false`。

## 追踪

- run_id：`day09_aderh_smoke_seed0_split_v1`。
- 证据：`evidence/Day09/smoke_config.yaml`、`output_schema.json`、`smoke_log.txt`、`go_no_go.md`。
- 下一步：Day 10 运行正式总实验并冻结结果。

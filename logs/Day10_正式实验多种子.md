# Day 10 正式实验（多种子）

> 定位：正式结果先回答 ADERH 的 AP、ROC-AUC、五种子波动与耗时，再用 IF、ECOD 解释相对位置。ADERH 没超过 IF 的负结果保留。

## 做了什么

- 运行 `src/run_day10_formal.py` 和 `src/validate_day10.py`，在完整 29,402/12,345 拆分上完成 15 个正式 run：Isolation Forest 与 ADERH 各跑种子 0–4，ECOD、OCSVM、PCA(5)、kNN、LOF 为确定性运行；每个 run 保存 JSON 和不带标签的逐样本分数。

## 结果

按 AP 排序：Isolation Forest 0.976866±0.001822；ECOD 0.910299；ADERH 0.890062±0.011963；OCSVM 0.375004；PCA(5) 0.356048；kNN 0.192808；LOF 0.134447。

ADERH 的 ROC-AUC 0.993468 很高，但 AP 低于 ECOD、更低于 Isolation Forest，且五种子 AP 标准差 0.011963 明显高于 IF 的 0.001822。测试集异常率约 7.02%，AP 对前列排序更敏感，因此主结论以 AP 为核心、AUC 为辅助，不挑最好种子代替均值。

## 判断

最值得保留的不是“前沿方法赢了”——它没有赢。第一次启动时参数顺序错误，seed 0 在拟合前立刻失败、未生成分数，失败堆栈保存在 `formal_run_log_attempt1_failed.txt`；我只修正参数传递顺序，数据、配置、种子和评价协议不变，再沿用同一 run_id 重新跑一遍，另存正式日志。

## 追踪

- run_id：`day10_*_split_v1`，共 15 个；`validate_day10.py` 从 raw 文件核对逐 run 指标与最终表一致。
- 证据：`results/aggregated/main_results_by_run.csv`、`main_results_summary.csv`。
- 下一步：Day 11 预先定义一个不调参的删特征扰动，检验主排序是否依赖 `feature_08`。

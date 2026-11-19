# Day 03 准备数据，固定无泄漏拆分

> 定位：为 ADERH 和所有对照准备同一份可追溯的数据；Shuttle 的异常标签是基准转换规则，不是真实故障标签。

## 做了什么

- 运行 `src/prepare_shuttle.py`，下载并校验 UCI Shuttle 原始文件，排除原始类 4，生成 0/1 基准标签、`split_v1.npz` 和只在训练部分拟合的预处理 Pipeline（中位数插补 + 标准化）。

## 结果

- 原始 58,000 条，排除类 4 后保留 49,097 条、9 个数值特征；无缺失、无重复特征行。
- 类 1 为正常，类 2/3/5/6/7 为基准异常，共 3,511 条，占 7.151150%；测试集异常 867 条，约占 7.02%。
- 固定拆分：训练 29,402 / 验证 7,350 / 测试 12,345，测试保持 UCI 官方分区。

## 判断

UCI 新页面元数据对特征数显示不一致（有 7 或 8），但官方 `shuttle.doc` 写 9 个属性，两份原始文件也都是 10 列（9 特征 + 1 类别），故以原始说明和文件形状为准并保留哈希。Shuttle 常见异常基准会删类 4，但这不是 UCI 官方故障标签，把转换规则和局限写出来比直接下载现成 `.mat` 更能说明数据来历。

## 追踪

- run_id：`prepare_shuttle_20261102_split_v1`。
- 证据：`registry/datasets.csv`、`data/splits/split_v1.npz`、`evidence/Day03/data_profile.csv`、`label_summary.csv`、`split_summary.csv`、`source_note.md`。
- 下一步：Day 4 在隐藏标签的条件下做描述性统计与结构诊断，先提可证伪假设。

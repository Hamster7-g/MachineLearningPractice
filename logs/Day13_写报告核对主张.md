# Day 13 写报告，核对主张

> 定位：2026-11-07 起按课程任务 4，把原来的多算法比较改成 ADERH 单一新方法的主线；原有数字和结果不因叙述调整而改变。

## 做了什么

- 运行 `src/build_report_stats.py`、`src/build_day13_notebook.py` 和 `src/audit_day13_report.py`，把 Day 10–12 的正式结果组织成可逐项回查的报告。
- 正文不再写内部 Day 编号、准入门槛和工程状态，只写科学上相关的方法身份、配置和证据。

## 结果

- 当前 Notebook 20 个单元、错误输出 0；正文引用的 26 个统计键全部存在；8 条主张都有 run、表、图和反证边界；7 条实际使用的核心文献。
- 所有经验数字由 `build_report_stats.py` 从正式 CSV、拆分和证据文件生成，不依赖手工复制。

## 判断

正文只保留四个真正影响路线的判断：新方法没有赢；PCA 解释方差不等于异常可分性；DBSCAN 不适合强行连续评分；类别正常与统计常见不等价。日志里的安装、接口门槛和重复警告没有搬进报告。最初数字审计正则把 `methods[...]` 误识别为统计字典 `s[...]`，已修正为只匹配独立变量 `s`，报告数字未改。

## 追踪

- run_id：Day 10 与 Day 11 正式运行、Day 12 案例分数。
- 证据：`report/report_stats.json`、`report/claims_evidence_matrix.csv`、`report/references.bib`。
- 下一步：Day 14 全新环境从头执行，检查环境、提交物与公开边界。

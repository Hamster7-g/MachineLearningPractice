# Day 14 换新环境复现，检查提交

> 定位：2026-11-19 定稿：本人决定这次交付不用 PDF，现阶段验收的是 Notebook、HTML 预览和可恢复的项目备份；旧的 PDF 排版验收不会自动套到新版。

## 做了什么

- 运行 `src/run_day14_repro.py` 和最终 Notebook 全量执行，记录 Python 与依赖版本，检查 HTML、Notebook、日志和项目备份。

## 结果

- 全量执行退出码 0；最终 Notebook 20 个单元、错误输出 0；HTML 预览和可恢复 ZIP 已生成。
- `evidence/Day14/environment.txt`、`run_all_log.txt`、`final_checklist.md` 已保存；本地最终 Notebook 已按本人信息填写姓名、学号、班级。

## 判断

首版 PDF 打印了完整流水线日志且宽表被横向截断，一次无代码 HTML 导出还因相对输出路径解析失败。实验协议和结果不变，只把完整日志转存为证据文件、精简报告展示列、改用绝对输出路径重导出，失败记录保留在日志里。技术验收已完成，正式平台上传与 GitHub 公开仍需本人完成，公开仓库应去除学号等个人信息。

## 追踪

- run_id：Day 10 正式 15 runs、Day 11 扰动 11 runs。
- 证据：`evidence/Day14/final_checklist.md`、`environment.txt`、`run_all_log.txt`。
- 下一步：本人决定仓库公开范围并检查个人信息后建仓上传。

# Day 02 选定前沿算法，检查能否复现

> 定位：从近年的候选里选出唯一的前沿方法 ADERH；接口烟雾测试不等于算法性能。

## 做了什么

- 建立 4 个候选，逐个核验论文年份、机制、是否非深度、官方实现与许可证；填写 `configs/frontier_gate.yaml` 和 `evidence/Day02/candidate_matrix.md`。
- 用 48×4 合成训练数组、8×4 测试数组检查 ADERH 的 `fit` 与评分接口。

## 结果

- `aderh==1.0.0` 安装成功、依赖检查通过；程序返回 8 个有限连续分数，退出码 0。
- BRDAD 思路贴合本课题，但 JMLR 页面无代码链接，也找不到作者维护且许可明确的实现；RGLD 论文说明代码要等接收后公开。两者不进入正式实验。

## 判断

如果为了追“最新”而自己临时重写 BRDAD，后面很难区分实现误差和算法差异，也不能诚实地称为论文复现。ADERH 有论文、官方仓库、MIT 许可、PyPI 包和评分接口的完整证据链，选它更稳妥。今天只证明 ADERH 可调用，尚未证明它效果好。

## 追踪

- run_id：`smoke_day02_aderh_interface_20261102`（仅接口测试，非正式实验）。
- 证据：`evidence/Day02/install_log.txt`、`smoke_test.py`、`smoke_output.txt`。
- 下一步：Day 3 选择数据集并建立固定无泄漏拆分，之前不跑 ADERH 正式性能。

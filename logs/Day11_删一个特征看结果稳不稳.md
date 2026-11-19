# Day 11 删一个特征，看结果稳不稳

> 定位：单次删特征检验 ADERH 与 IF/ECOD 的相对排序；结论只覆盖这一种扰动，不是普遍鲁棒性证明。

## 做了什么

- 运行 `src/run_day11_robustness.py`，根据 Day 4 的无标签相关性，固定删除强相关对中编号更大的 `feature_08`，重新标准化后运行 Isolation Forest、ADERH 各 5 个种子及确定性的 ECOD，共 11 个 run。翻转标准先于运行写入：删除后 IF 不再平均 AP 最高，或 IF−ADERH 差值不再为正。

## 结果

- Isolation Forest：AP 0.976866 → 0.973432（-0.003434）。
- ADERH：AP 0.890062 → 0.896028（+0.005966）。
- ECOD：AP 0.910299 → 0.872358（-0.037942）。

主结论没有翻转，IF 仍领先 ADERH 约 0.077404；但次级排序变化，ADERH 从第三升到第二、ECOD 从第二降到第三。

## 判断

ECOD 直接聚合逐维边缘尾概率，删除一个信息较强的维度后变化更大，机制上说得通，但单次删特征不能证明因果。我把它写成“与机制一致的解释假设”，而不是断言 `feature_08` 就是 ECOD 成败原因。

## 追踪

- run_id：`day11_remove_feature08_*_split_v1`，共 11 个。
- 证据：`evidence/Day11/robustness_plan.md`、`claim_update.md`。
- 下一步：Day 12 按模型排序分歧选择案例，回到原始特征解释差异。

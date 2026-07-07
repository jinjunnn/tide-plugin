---
description: 盘后复盘(涨停簇 + 龙虎榜 + 竞价兑现)
argument-hint: [可选:YYYY-MM-DD,缺省最新交易日]
---

执行盘后复盘($ARGUMENTS 可指定日期,缺省最新)。

1. 先调 `get_methodology(name="postmarket-review")` 获取分析流程,严格照做。
2. 盘后报告 16:30-17:00 后才有当日数据;更早调用时明示拿到的是哪一天的。
3. 输出风格与免责边界遵循 `tide-intro` skill。

---
description: 题材相位分析(还能不能追)
argument-hint: <题材/概念名>
---

对 $ARGUMENTS 指定的题材/概念执行相位分析。

1. 先调 `get_methodology(name="theme-analysis")` 获取分析流程,严格照做。
2. 第一步永远是 `search_topic(q="$ARGUMENTS")` 解析 cid;多个候选时向用户确认层与对象。
3. 输出风格与免责边界遵循 `tide-intro` skill。

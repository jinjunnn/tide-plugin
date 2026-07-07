---
description: 个股深挖(结构档案 + 归因)
argument-hint: <股票代码或名称>
---

对 $ARGUMENTS 指定的个股执行深挖分析。

1. 先调 `get_methodology(name="stock-deep-dive")` 获取分析流程,严格照做。
2. 用户给的是名称时,先用 `search_topic` / `get_stock` 的返回确认代码,向用户复述确认的标的再继续。
3. 输出风格与免责边界遵循 `tide-intro` skill。

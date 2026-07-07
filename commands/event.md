---
description: 事件冲击分析(历史先例 + 暴露面 + 持仓交叉)
argument-hint: <新闻/事件描述>
---

分析 $ARGUMENTS 描述的事件对市场与用户持仓的影响。

1. 先调 `get_methodology(name="event-impact")` 获取分析流程,严格照做。
2. 若用户有持仓档,必须做持仓交叉段(谁受益、谁暴露在受损面)。
3. 输出风格与免责边界遵循 `tide-intro` skill。

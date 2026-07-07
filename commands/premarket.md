---
description: 盘前简报(环境 → 今日重点 → 观察/回避 → 板块池)
---

生成今日盘前简报。

1. 先调 `get_methodology(name="premarket-briefing")` 获取分析流程,严格照做。
2. 先核报告最新可用日期(非交易时段可能是上一交易日),向用户明示数据时点。
3. 若用户有持仓档(~/.tide/portfolio.md 或 get_watchlist),简报末尾做持仓交叉提示。
4. 输出风格与免责边界遵循 `tide-intro` skill。

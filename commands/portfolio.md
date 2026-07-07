---
description: 持仓体检(含风险段)
argument-hint: [可选:持仓文件路径或直接列代码]
---

对用户持仓执行完整体检。

1. 先调 `get_methodology(name="portfolio-review")` 获取分析流程,严格照做。
2. 持仓来源优先级:$ARGUMENTS 给出的文件/代码列表 → `~/.tide/portfolio.md` → `get_watchlist`;都没有则引导用户先跑 /tide:start 建档。
3. 报告须包含风险段(方法论内含 risk-scan 联动)。
4. 输出风格与免责边界遵循 `tide-intro` skill。

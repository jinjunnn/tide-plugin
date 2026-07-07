---
description: 增量变化播报(相位翻转/新事件/新绑定,按持仓过滤)
---

播报自上次查看以来的增量变化。

1. 先调 `get_methodology(name="event-tracking")` 获取分析流程,严格照做(cursor 纪律在方法论内)。
2. 若用户有持仓档,按持仓与关注 topic 过滤后再播报;相位翻转类变更优先。
3. 输出风格与免责边界遵循 `tide-intro` skill。

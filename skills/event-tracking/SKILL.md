---
name: event-tracking
description: 增量事件追踪:变更流 cursor 纪律、按持仓过滤、相位翻转告警。触发词:最近有什么新变化、有什么新消息、增量更新、whatsnew、盯一下我的持仓。
---

场景:「最近有什么新变化?」——增量消费变更流,只播报真正的新东西。

执行:先调 `get_methodology(name="event-tracking")` 获取完整分析流程,严格按流程执行。
输出风格、术语翻译、免责边界与失败路径处理,一律遵循本插件 `tide-intro` skill。

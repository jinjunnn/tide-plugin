---
name: portfolio-review
description: 持仓体检:逐股结构档案 + 事件 + 所属题材/产业链相位 + 集中度与风险段。触发词:我的持仓怎么样、帮我看持仓、持仓体检、组合体检、portfolio。
---

场景:「我的持仓怎么样了?」——对用户持仓做逐股体检与组合层风险扫描。

执行:先调 `get_methodology(name="portfolio-review")` 获取完整分析流程,严格按流程执行。
输出风格、术语翻译、免责边界与失败路径处理,一律遵循本插件 `tide-intro` skill。

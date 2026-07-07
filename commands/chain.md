---
description: 产业链分析(门控环节 + 受益股)
argument-hint: <产业链名>
---

对 $ARGUMENTS 指定的产业链执行链级分析。

1. 先调 `get_methodology(name="chain-analysis")` 获取分析流程,严格照做(注意:该方法论需 pro 档,tier 不足时按错误提示转述升级路径,并降级用 get_topic 做结构概览)。
2. 第一步 `search_topic(q="$ARGUMENTS", layer="chain")` 解析链 cid。
3. 输出风格与免责边界遵循 `tide-intro` skill。

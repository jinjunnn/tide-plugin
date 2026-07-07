---
name: tide-intro
description: tide A 股结构化分析的公共底座。任何用 tide 工具做分析之前先读本 skill:23 个工具的地图(何时用哪个)、本体字典(三层 topic/相位/门控/绑定轴/事件轴)、术语人话翻译表、溯源阅读法、免责边界、数据时效节奏。触发词:tide、A股分析、工具怎么用、术语解释、tide 入门。
---

# tide 使用底座:工具地图 · 本体字典 · 输出风格

tide 是一个 A 股结构化分析服务:**产业链 / 概念板块 / 催化题材三层知识图谱 + 事件主干与历史先例 + 日更盘前盘后分析产物**。分工:你(用户自带的 LLM)负责推理与表达,tide 负责事实与结构。本文件是所有 tide 分析 skill 的公共底座——输出风格、术语字典、免责与时效边界都以本文件为准。

## 1. 输出风格(所有分析输出必须遵守)

1. **结论先行**:第一段直接给判断,不铺垫。
2. **证据随后**:每条关键判断挂出处——用了哪个工具、哪份报告、数据时点(`as_of`)。
3. **反面与风险**:至少给一条「什么情况下这个判断不成立」。
4. **下一步可问**:结尾给 2-3 个用户可以继续追问的问题。
5. **术语首现带白话**:内部词表(相位/门控/conviction 等)第一次出现时,按 §4 翻译表给白话解释。
6. **免责框架必带**(§6)。
7. **数据时点明示**:如「基于 07-06 盘后数据」;绝不把日更数据说成实时。

## 2. 工具地图(23 个,何时用哪个)

**典型链路**:中文名 → `search_topic` 拿 cid → `get_topic` 看全貌 → `get_topic_members` / `get_topic_events` 下钻 → 个股 `get_stock`。

### 入口与目录
| 工具 | 何时用 |
|---|---|
| `search_topic` | 一切分析第一步:把中文板块/题材/产业链名(含俗称)解析成图谱 cid |
| `list_topics` | 不知道看什么时的目录页;`scope=themes_active` 扫当前活跃题材相位 |
| `aggregate` | 要一张市场结构概览(题材相位分布 / 受益确信分布 / 事件类型日频) |

### topic(题材 / 概念 / 产业链)
| 工具 | 何时用 |
|---|---|
| `get_topic` | 单个 topic 全貌(相位、关联结构、成分广度、近窗催化);`section=timeline` 相位史,`section=metrics` 板块时序 |
| `get_topic_members` | 成分股与广度(服务端已内建纪律:只给有效绑定 + 强度白名单 + 已上市) |
| `get_topic_events` | 「这个题材最近有什么催化」;传 `event_id` 取单条事件详情 |
| `get_concept_state` | 单板块状态机相位 / 四象限现值(「这个板块还能不能追」的状态视图) |

### 个股
| 工具 | 何时用 |
|---|---|
| `get_stock` | 个股结构档案:缺省多维装配卡;`section=memberships` 反查三层归属;`section=relations` 客供/竞争邻域 |
| `get_stock_events` | 「这只股票最近发生了什么」 |
| `get_quote_kline` | 价格佐证(现价快照 / 日 K);注意低频限额 |

### 产业链 alpha
| 工具 | 何时用 |
|---|---|
| `get_chain_alpha` | 「这条链现在卡在哪、谁最受益」:gating 门控下钻 + picks 三重交叉选股 |
| `find_disrupts_pairs` | 链级替代/颠覆关系扫描(谁在侵蚀谁的需求;pair-trade / 受损回避) |

### 事件与影响
| 工具 | 何时用 |
|---|---|
| `find_similar_events` | 历史先例:「上次出这种事,后来怎么走」 |
| `impact_map` | 假设事件暴露面:「若 X 发酵,谁受益、谁遭殃」 |
| `changes_feed` | 增量变更流(相位翻转 / 新绑定 / 新高强度事件;cursor 断点续传) |

### 新闻
| 工具 | 何时用 |
|---|---|
| `news_context` | 已入库新闻簇(标题 + 摘要 + 热度):「这个题材/个股最近有什么报道」 |
| `search_news` | 即时定向检索(突发核实 / 海外一手源;按次计费;一次查一个实体的一条可证伪声明) |

### 报告与截面
| 工具 | 何时用 |
|---|---|
| `get_daily_report` | 日更分析产物:盘前三件套 / 宏观 / 涨停簇复盘 / 龙虎榜 / 竞价验证 / 题材报告 |
| `get_sector_pool` | 板块强弱两池(focus 强势 / avoid 走弱),盘中可用 |
| `get_sector_verdicts` | 盘中板块裁决流(值得上/再等等/跳过 + 四问叙事) |

### 个人化与方法论
| 工具 | 何时用 |
|---|---|
| `get_watchlist` / `set_watchlist` | 云端自选(与 iOS 同账户);未上线时按提示改用本地档 `~/.tide/portfolio.md` |
| `get_methodology` | 执行任何 `/tide:*` 分析前,先取对应方法论全文再照流程做 |

## 3. 本体字典

### 3.1 三层 topic(平行三层,各自独立的股票集)
- **chain(产业链)**:真实供应链结构树(环节、咽喉、门控、成本占比)。cid 常见 `CHAIN:` 前缀。
- **concept(概念板块)**:A 股市场约定俗成的板块镜像,带板块状态机(四象限)。
- **catalyst_theme(催化题材)**:被具体事件「点燃」的短期热点,有生命周期相位。判据:指不出一个点燃它的催化事件,就不是题材。

### 3.2 题材两轴:成熟度与相位(正交,别混)
- **status(成熟度)**:`candidate`(候选)→ `confirmed_candidate`(确认候选)→ `resolved`(正式题材)→ `archived`(归档)。
- **current_state(相位,7 档)**——生命周期走到哪:

| 相位 | 白话 | 操作含义(仅结构描述,非建议) |
|---|---|---|
| `dormant` | 蛰伏 | 暂无催化;可复燃,非死亡 |
| `emerging` | 萌芽期 | 催化刚出现、少数个股响应;信息不对称最大、不确定也最大 |
| `accelerating` | 加速期 | 催化密集、广度扩散中;题材动能最强阶段 |
| `main_up_wave` | 主升期 | 市场主线,龙头带高度;拥挤度同步上升 |
| `divergence` | 分歧期 | 高位震荡,龙头与跟风分化;方向待定 |
| `fading` | 退潮期 | 催化衰减、广度收缩 |
| `dead` | 出清 | 本轮结束 |

相位有 `state_confidence`(置信 0-1)与 `state_at`(裁决时点);`state_reason` 带 `[degraded:...]` 前缀表示降级判断,转述时要说明。

### 3.3 板块状态(concept 的「状态视图」)
- **四象限 quadrant**:`LEADING`(强势领涨)/ `IMPROVING`(改善修复)/ `WEAKENING`(走弱)/ `LAGGING`(落后)。
- `rotation_score` 轮动强度分;`z_rs` / `z_rm` 相对强弱与动量的连续评分;`is_mainline` 主线标记。
- `fsm` / `confirm_state`:板块状态机相位与确认态(get_concept_state 返回)。

### 3.4 产业链结构轴(都在链的「环节」和「个股绑定」上)
- **structural_role(结构角色)**:`chokepoint`(咽喉:独家/换不掉,慢变)> `bottleneck`(瓶颈:产能爆满,快变)> `normal` > `candidate`(潜在候选,前瞻推测)。
- **gating_role(门控紧迫度,与结构角色正交)**:`gating_now`(当下最紧=「现在」)/ `structural_hardest`(结构最难缓=扩产最慢,「埋伏」)/ `both`(又急又难,最高优先)/ 空值(非门控或未判)。
- **cost_share_pct(成本占比)**:该环节占其**直接父层** BOM 成本的百分比(价值池);整机占比需沿层级连乘,不能跨层相加。

### 3.5 个股 ↔ topic 绑定轴(一条边上的几个正交字段)
- **strength(业务贴合)**:`core`(核心真受益)/ `related`(相关)/ `speculation`(蹭概念,弱关联)/ `sentiment`(纯情绪炒作,非基本面)。广度/状态类聚合只认 core+related。
- **binding_status(绑定有效性)**:`active`(有效)/ `quarantined`(已隔离=错误绑定,一切分析忽略)。服务端已过滤,若见到 quarantined 不要采纳。
- **conviction(受益确信)**:`high` / `medium` / `low`。受「纯度」修正:`pure_play`(纯玩家,业务专注弹性大)/ `focused`(聚焦)可以 high;`diversified`(多元化)上限 medium;`conglomerate`(巨型集团,该业务占比小)上限 low-medium。**大市值 ≠ 高受益弹性**。
- **opportunity_stage(机会成熟度)**:`anticipated`(前瞻推测,无订单)→ `qualifying`(送样认证中)→ `confirmed`(订单确认)→ `ramping`(放量)。前两档 = 高潜在收益 + 低确定性,**必须与 `speculation_risk`(投机风险 low/medium/high)一起报**。

### 3.6 事件轴(三个正交维度 + 一个方向)
- **event_class(事件成色,5 类)**:
  - `state_change` 事实状态改变(签约/管制/量产/停产)——最硬,可入判断;
  - `data_point` 数据点(销量/份额/价格)——趋势佐证;
  - `roadmap` 路线图(两三年后的规划)——远期,不折现为当下;
  - `narrative` 叙事(观点/展望/散文)——只作情绪背景,**绝不当 state_change 报**;
  - `market_vehicle` 行情载体(指数/基金/资金面事件)——不映射公司基本面。
- **significance(影响强度)**:0-10,**无方向**(强度不表利好利空)。
- **impact(方向)**:`positive` / `negative` / 空值(未判)。方向挂在「事件 → 某个 topic」的绑定上,不在事件本身——同一事件可以对 A 题材利好、对 B 链利空。空值不要脑补方向。
- **event_subtype**:公告/财报/合同等细类(有则参考)。

### 3.7 其它常见字段
- **listing_status**:`listed` 已上市 / `pre_ipo` 上市前 / `private` 未上市 / `delisted` 已退市。非 listed 的节点只是结构锚点(如某私有巨头),**不是可投资标的**。
- **资质曲线(qualification,个股在链上的兑现进度)**:`dev_contract`(研发合作)→ `qualifying`(认证送样)→ `volume_ramp`(放量爬坡)→ `sold_out`(产能售罄)。
- **theme_diffusion.stage(涨停题材扩散,4 档)**:`零星` → `扩散` → `分歧` → `塌方`。扩散且健康 = 次日核心观察;塌方 = 回避。
- **displacement_stage(替代进度,DISRUPTS 边)**:`emerging`(替代萌芽)/ `accelerating`(替代加速)/ `majority`(过半)/ `terminal`(尾声,基本已定价)。
- **SELLS_TO / COMPETES_WITH(公司级关系)**:客供关系里 `sole_source` = 独家供应(公司级咽喉);竞争关系里 `incumbent` 在位者 / `challenger` 挑战者(常见:国产替代挑战全球在位)。

## 4. 人话翻译层(输出用右列白话;首次出现附原词)

| 原词 | 白话 |
|---|---|
| chain / concept / catalyst_theme | 产业链 / 概念板块 / 催化题材 |
| dormant / emerging / accelerating | 蛰伏 / 萌芽期 / 加速期 |
| main_up_wave / divergence / fading / dead | 主升期 / 分歧期 / 退潮期 / 出清 |
| candidate / resolved(题材 status) | 候选题材 / 正式题材 |
| chokepoint / bottleneck | 咽喉环节(独家换不掉)/ 瓶颈环节(产能爆满) |
| gating_now | 当前卡脖子环节(现在最紧) |
| structural_hardest | 结构上最难缓解的环节(扩产最慢,埋伏窗口) |
| both(gating_role) | 双重门控(又急又难) |
| cost_share_pct | 成本占比(价值池大小) |
| core / related | 核心受益 / 相关受益 |
| speculation | 蹭概念(沾边但主业不真受益) |
| sentiment | 情绪炒作标的(资金驱动,非基本面) |
| quarantined | 已隔离的错误标签(忽略) |
| conviction high/medium/low | 受益确信度 高/中/低 |
| pure_play / conglomerate | 纯玩家(弹性大)/ 巨型集团(弹性被稀释) |
| anticipated / qualifying / confirmed / ramping | 前瞻推测 / 送样认证中 / 订单确认 / 放量中 |
| speculation_risk | 投机风险(前瞻 ≠ 确定) |
| state_change / narrative | 事实变化(硬事件)/ 叙事(软信息) |
| data_point / roadmap / market_vehicle | 数据点 / 远期路线图 / 行情载体类事件 |
| significance | 影响强度(0-10,不分好坏) |
| impact positive/negative | 对该题材利好 / 利空 |
| LEADING / IMPROVING / WEAKENING / LAGGING | 强势领涨 / 改善修复 / 走弱 / 落后 |
| rotation_score | 板块轮动强度分 |
| limit_up_days | 连板数(涨停高度) |
| sole_source | 独家供应商 |
| dev_contract / qualifying / volume_ramp / sold_out | 研发合作 / 认证送样 / 放量爬坡 / 产能售罄 |
| BUY / WAIT / SKIP | 值得上 / 再等等 / 跳过 |
| as_of | 数据时点 |
| degraded | 服务降级(用的是容灾缓存旧数据) |
| precedent | 历史先例(上次类似事件的后续走法) |

## 5. 溯源阅读法(拿到返回后先看这些)

1. **`as_of`**:每个响应的数据时点;转述任何数字/判断都带上它。
2. **`degraded: true` + `cache: "stale"`**:上游暂不可达,返回的是容灾缓存;`stale_age_sec` / `stored_at` 告诉你数据多旧——**必须向用户明示**「这是 X 小时前的缓存数据」,不能当新鲜数据讲。
3. **逐维 status**:个股卡等多维装配结果里,每一维带自己的来源与状态;某维缺失/降级时如实说「该维度暂无数据」,**不脑补**。
4. **`vec_used: false`**:语义召回降级,命中只来自名字匹配——搜不到不代表不存在,提示用户换个叫法再试。
5. **`evidence` / `basis` / `reason` 字段**:判断依据的具名出处;引用判断时把依据一起给用户。
6. **相似度/召回分数只用于排序**:不要把分数当置信度、不要设阈值卡结果;取前几名逐个人工核对是否真相关。
7. **空结果是有效结果**:如实报「没查到」,并说明查询范围;不要编造。

## 6. 免责边界(所有分析输出必带)

固定框架(可改措辞不可改实质):

> 以上为基于公开数据与知识图谱的**结构与事实分析,不构成投资建议**。数据有明确时点(见 as_of),市场随时变化;涉及前瞻推测处均标注了确定性档位。买卖决策请自行判断,风险自担。

并且:不喊单、不给具体仓位/买卖点指令、不承诺收益;对 `anticipated` / `speculation` / `narrative` 档信息必须明示其低确定性。

## 7. 时效期望管理(日更节奏,不冒充实时)

| 数据 | 可用时点(交易日) |
|---|---|
| 盘前三件套:`premarket_environment` / `premarket_rankings` / `premarket_watch_avoid` | 08:30 后 |
| `auction_analysis`(竞价验证) | 09:25 后 |
| `macro_context`(宏观) | 前一交易日 16:00 后 |
| `cls_limitup_report`(涨停簇)/ `lhb_analysis`(龙虎榜)等盘后件 | 16:30-17:00 后 |
| 盘中可用 | `get_quote_kline`(实时快照)/ `get_sector_pool` / `get_sector_verdicts` / `changes_feed` / `news_context` |
| 盘中突发新闻 | `search_news`(按次计费)或你的 harness 自带 web search 补充 |

纪律:`get_daily_report` 不带 `date` 取最新一份;**先核返回里的日期**,若早于今天(周末/清晨常见),向用户明示「最新一份是 X 日的」。图谱结构(链/绑定/相位)是持续维护的,但也各有自己的时点字段。

## 8. 失败路径明示(绝不静默)

工具报错时返回结构化 JSON:`{error, reason, hint, portal_url?}`。处理纪律:

- **一律把 `reason` 和 `hint` 转述给用户**,不要吞掉换成泛泛的「出错了」。
- `tier_insufficient`:明说该工具/方法论需要哪个订阅档,附 `portal_url` 让用户升级。
- `quota` / 额度类:明示限额与恢复时点。
- `not_implemented` / `not_ready` / `not_configured`:按 `hint` 给的替代路径降级(如云端自选未上线 → 本地档)。
- `unauthorized` / `invalid_key`:引导检查 `TIDE_API_KEY` 配置,portal 可重新签发。
- 上游 `degraded`:照 §5 第 2 条,用旧数据但明示时点。
- 任何失败都不影响诚实:宁可输出「这一步失败了,原因是…,你可以…」,不要假装有数据。

# tide — A 股结构化分析(MCP + plugin)

把 **产业链 / 概念 / 题材三层知识图谱 + 事件主干与历史先例 + 日更盘前盘后分析产物** 接进你自己的 AI 编程/对话工具(Claude Code、Codex、Cursor、Zed…)。你的 LLM 负责推理,tide 负责事实与结构。

> **免责**:tide 提供的是结构与事实分析,**不构成投资建议**;数据有明确时点(as_of),决策请自行判断、风险自担。

## 安装(Claude Code,三行)

```bash
# 1. 到 portal(https://graph.tidelabs.click → 侧栏「API 接入」)注册并签发 API key(tk_ 开头)
export TIDE_API_KEY=tk_xxxxxxxx   # 写进你的 shell profile
# 2. 安装 plugin
claude plugin marketplace add tide && claude plugin install tide
# 3. 上手自检(验 key → 示例问题 → 建持仓档)
/tide:start
```

> 服务地址:`https://mcp.tidelabs.click/mcp`(备用:`https://tide-mcp.jinjunnm.workers.dev/mcp`,
> 两者同一服务;正常情况用正式域名即可)。

## 其它工具接入(remote MCP,无需本地安装任何东西)

tide 是纯远程 MCP 服务(Streamable HTTP)。**不提供 stdio/本地形态**——不支持 remote MCP 的客户端暂不在支持范围。

### Codex

`~/.codex/config.toml`:

```toml
[mcp_servers.tide]
url = "https://mcp.tidelabs.click/mcp"
http_headers = { "Authorization" = "Bearer tk_xxxxxxxx" }
```

### Cursor

`.cursor/mcp.json`(项目级)或 `~/.cursor/mcp.json`(全局):

```json
{
  "mcpServers": {
    "tide": {
      "url": "https://mcp.tidelabs.click/mcp",
      "headers": { "Authorization": "Bearer tk_xxxxxxxx" }
    }
  }
}
```

### Zed

`settings.json` → `context_servers`:

```json
{
  "context_servers": {
    "tide": {
      "source": "custom",
      "url": "https://mcp.tidelabs.click/mcp",
      "headers": { "Authorization": "Bearer tk_xxxxxxxx" }
    }
  }
}
```

## 能问什么(示例问题集,对应八大场景)

| 你可以直接问 | 对应入口 |
|---|---|
| 「我持有宁德时代和中际旭创,最近有什么我该知道的?」 | `/tide:portfolio` |
| 「今天开盘前我该知道什么?」 | `/tide:premarket` |
| 「300308 这只股票能不能买?什么来头?」 | `/tide:stock 300308` |
| 「固态电池现在还能追吗?」 | `/tide:theme 固态电池` |
| 「人形机器人这条链现在卡在哪、谁最受益?」 | `/tide:chain 人形机器人` |
| 「英伟达这个新闻对 A 股什么影响?历史上类似事件后来怎么走?」 | `/tide:event <描述>` |
| 「今天涨停都是什么线索?复盘一下」 | `/tide:review` |
| 「帮我把持仓过一遍雷」/「最近有什么新变化?」 | `/tide:portfolio`(风险段)/ `/tide:whatsnew` |

## 里面有什么

- **23 个 MCP tools**:图谱查询(三层 topic / 成分 / 事件 / 个股档案 / 产业链门控与选股 / 替代关系 / 影响面 / 历史先例)+ 日更报告(盘前三件套 / 宏观 / 涨停簇 / 龙虎榜 / 竞价验证)+ 板块强弱池 / 盘中裁决 + 新闻簇与定向检索 + 自选/持仓 + 方法论下发。
- **10 个 skills**:`tide-intro` 公共底座(工具地图 / 术语字典 / 人话翻译 / 免责与时效)+ 9 个场景分析 skill(持仓体检 / 盘前 / 个股 / 题材 / 产业链 / 事件 / 复盘 / 避雷 / 增量追踪)。深度方法论按订阅档位从服务端下发(`get_methodology`),迭代无需更新 plugin。
- **9 个 commands**:`/tide:start` 上手自检 + 八大场景薄入口。
- **1 个 agent**:`a-share-analyst` 只读分析子代理,适合「把持仓 12 只全部体检一遍」式长任务 fan-out。

## 数据节奏(日更,不冒充实时)

盘前报告交易日 08:30 后、竞价验证 09:25 后、盘后复盘件 16:30-17:00 后可用;盘中可用的是行情快照、板块强弱池、盘中板块裁决、增量变更流与新闻检索。盘中突发建议配合你所用工具自带的 web search。

## 持仓怎么给

- **本地档(默认,隐私最优)**:`~/.tide/portfolio.md`,人话表格(代码/成本/仓位/备注),`/tide:start` 会帮你建模板;持仓不上云。
- **云端档**:与 iOS App 同一账户的自选同步(`get_watchlist` / `set_watchlist`,已上线;iPhone 加自选这里立即可见)。

## 常见问题

- **401 / invalid_key**:检查 `TIDE_API_KEY` 是否配置、key 是否复制完整;portal 可重新签发。
- **tier_insufficient**:该工具/方法论需要更高订阅档,错误里带 portal 链接。
- **degraded: true**:上游暂不可达时返回容灾缓存,响应里有数据时点——旧数据,但可用。

## 贡献

本仓是发行镜像(由源仓单向同步),**不接受直接 PR**——issue 欢迎,改动请在 issue 里描述,我们会在源仓落地后同步过来。

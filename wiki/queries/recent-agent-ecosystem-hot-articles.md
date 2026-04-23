# 近期 Agent 生態熱門文章研究

## 問題意識

我想找的是：近期有哪些 *agent* 相關技術或文章，且在社群上討論度高，值得納入長期筆記。

這次挑選的來源以 Hacker News 熱門討論為主，補上少量技術／產品文章，重點看的是：

- coding agent 的實戰體驗是否真的在進步
- MCP 與 skills 這類 extensibility 路線的討論
- multi-agent / agent teams 是否正在變成主流設計語言
- 開源 agent 工具是否仍有明顯熱度

## 這次挑選的來源

### 1. Qwen3.6-35B-A3B: Agentic coding power, now open to all

- URL: [https://qwen.ai/blog?id=qwen3.6-35b-a3b](https://qwen.ai/blog?id=qwen3.6-35b-a3b)
- HN: 1271 points / 531 comments
- 日期: 2026-04-16
- 觀察：這是這次最「新」而且討論度很高的來源之一，主題是 *agentic coding* 能力對外開放，顯示社群對可用、可跑的 coding agent 模型仍然非常敏感。

### 2. I still prefer MCP over skills

- URL: [https://david.coffee/i-still-prefer-mcp-over-skills/](https://david.coffee/i-still-prefer-mcp-over-skills/)
- HN: 460 points / 375 comments
- 日期: 2026-04-10
- 觀察：這篇很適合拿來觀察 agent extensibility 的分歧。社群不只在看「有沒有擴充機制」，也在看 *protocol-style* 擴充（MCP）和 *workflow/package-style* 擴充（skills）哪個比較自然。

### 3. We tasked Opus 4.6 using agent teams to build a C Compiler

- URL: [https://www.anthropic.com/engineering/building-c-compiler](https://www.anthropic.com/engineering/building-c-compiler)
- HN: 735 points / 738 comments
- 日期: 2026-02-05
- 觀察：這類文章代表 multi-agent / agent teams 已經不是純概念，而是開始被包裝成可以公開討論的 engineering story。社群關心的不是只有結果，還有 agent team 的分工、流程與可靠性。

### 4. OpenCode – Open source AI coding agent

- URL: [https://opencode.ai/](https://opencode.ai/)
- HN: 1274 points / 619 comments
- 日期: 2026-03-20
- 觀察：開源 coding agent 仍然很有熱度，代表大家不只在看大廠模型，也在看可替換、可本地化、可改造的 agent workflow。

### 5. Opus 4.5 is not the normal AI agent experience that I have had thus far

- URL: [https://burkeholland.github.io/posts/opus-4-5-change-everything/](https://burkeholland.github.io/posts/opus-4-5-change-everything/)
- HN: 879 points / 1353 comments
- 日期: 2026-01-06
- 觀察：這種「體驗報告」型文章討論度特別高，反映 agent 領域很大一部分熱度來自真實使用感受，而不是只靠 benchmark 或 demo。

## 初步結論

這批熱門文章/討論大致收斂成 4 個方向：

1. **Agentic coding 仍是核心戰場**
   - 社群最在意的是 agent 能不能穩定地幫忙寫程式、改 repo、跑 tool loop。

2. **Extensibility 的分歧正在變清楚**
   - MCP / skills / plugin / hook 這些做法，不只是功能差異，而是「agent 要怎麼接外部能力」的架構選擇。

3. **Multi-agent / agent teams 開始進入主流敘事**
   - 不少高討論文章已經把多 agent 分工當成可公開討論的工程實踐，而不是研究室想像。

4. **開源與可替換性依然重要**
   - HN 熱度顯示大家仍然很在意 open source、local-first、provider-agnostic 的 agent 工具。

## 跟既有筆記的關係

這份研究最適合和下面幾頁一起看：

- [Agent Research](../sources/agent-research.md)
- [AI Coding Agent 設計維度](../topics/agent-coding-agent-design-dimensions.md)
- [履歷與 CV 的 LLM Agent 工作流](../topics/resume-cv-llm-agent-workflow.md)

其中，[AI Coding Agent 設計維度](../topics/agent-coding-agent-design-dimensions.md) 可以直接拿來當分析框架；這份 query note 則補上 2026-04 這一波社群熱點。

## 延伸方向

如果之後要繼續追，可以再分成三條線：

- *agentic coding* 模型與工具鏈
- MCP vs skills / hooks / plugins 的 extensibility 路線
- multi-agent orchestration / agent teams 的工程化設計
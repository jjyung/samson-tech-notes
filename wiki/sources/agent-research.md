# Agent Research

## Source

- Title: `Agent Research`
- Author: `jjyung`
- Type: research workspace / meta notes repo
- URL: https://github.com/jjyung/agent-research

## Summary

`agent-research` 不是單一產品，而是一個用來研究熱門 GitHub agent 專案的知識工作區。它把上游專案作為研究對象，使用 `git submodule` 管理 `sources/`，再在 `notes/` 中寫出繁體中文的架構分析、設計哲學與觀察心得。

這種做法的重點不是「收藏連結」，而是把外部專案轉成可持續累積的研究筆記。每個 upstream project 都會變成一個可比較、可回看、可延伸的 case study。

## Key Ideas

### 1. 研究對象是具體專案，不是抽象想像

這個 repo 選擇直接研究真實存在的 agent 專案，例如 Codex、OpenCode、Gemini CLI、OpenClaw、open-claude-code。這讓比較不是停留在口號，而是能對照實際架構、tool loop、sandbox、subagent、skills 與 context 管理。

### 2. `sources/` 與 `notes/` 分層很清楚

- `sources/`：以 `git submodule` 管理的原始上游 repo
- `notes/`：每個專案對應的研究筆記

這讓原始碼、觀察與整理分離，避免研究筆記和來源資料混在一起。

### 3. 共同比較維度很明確

從已整理的筆記來看，這個 repo 特別關注以下幾個維度：

- tool orchestration
- approval / permission model
- sandbox 與安全邊界
- subagent / multi-agent 協作
- memory / context compression
- MCP / protocol extensibility
- skills / workflow 可擴充性
- TUI / client-server / control plane 設計

### 4. 研究目標偏向「設計哲學」而不只是功能列表

筆記不只列功能，還在整理：

- 為什麼這樣設計
- 哪些抽象值得學習
- 哪些架構選擇有 trade-off
- 哪些模式適合做自己的 agent 工作流

### 5. 它本身就是一個可持續維護的知識系統

`agent-research` 也在實踐它所研究的概念：把內容持續沉澱成 markdown、讓筆記彼此連結、讓研究結果可反覆增補，而不是一次性摘要。

## Notable Projects

### Codex

重點在 local CLI coding agent、sandbox、安全授權、subagent、MCP 與工具呼叫控制。

### OpenCode

重點在開源、provider-agnostic、TUI-first、LSP、client/server 架構，以及可切換 build / plan 模式。

### Gemini CLI

重點在 Google 生態、terminal-first workflow、interactive / headless 兩種模式、subagent、hooks、memory 與 context compression。

### OpenClaw

重點在 local-first personal assistant、單一 gateway control plane、多通訊平台整合、skills platform 與 agent workspace separation。

### open-claude-code

重點在超大型 CLI agent codebase 的工具系統、permission model、hook 系統、memory、feature flags 與多 agent 協調。

## Relevance To This Wiki

這個 repo 對 `samson-tech-notes` 很有參考價值，因為它展示了：

- 如何把外部來源轉成可維護的知識頁
- 如何用固定結構整理 research notes
- 如何比較不同 agent 工具的 design space
- 如何把研究結果回寫成長期可用的 wiki 資產

它和這個 wiki 的關係很自然：兩者都不是單純存檔，而是在建構會持續增長的知識系統。

## Suggested Follow-up Pages

- `wiki/topics/agent-coding-agent-design-dimensions.md`
- `wiki/concepts/persistent-wiki-vs-rag.md`
- `wiki/topics/ingest-workflow.md`
- `wiki/topics/query-as-knowledge-production.md`

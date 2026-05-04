# Agent 權限管理與 MCP 分隔

## 核心觀點

當 agent 透過 MCP 接外部能力時，最重要的不只是「能不能用」，而是 **怎麼把權限與邊界切清楚**。

一個實用的理解方式是把系統拆成三層：

- **授權層**：誰能授權、授權給誰、scope 是什麼
- **工具層**：哪些 tools 可見、哪些只讀、哪些會改資料
- **邊界層**：哪些能力被隔離在獨立 MCP server、roots 或 sandbox 裡

## 為什麼這個主題重要

agent 的風險通常不是模型本身，而是它能接觸的外部能力太大：

- 可以看到不該看的資料
- 可以執行不該執行的操作
- 可以在沒有審核的情況下把動作放大成實際副作用

所以，MCP 很適合拿來做 **capability separation**：

- 把資料庫、檔案、內部 API 分開
- 把 read-only 和 write / destructive tools 分開
- 把高風險操作放進更嚴格的 server 或 approval flow

## 2026-04-28 / 2026-04-29 的新訊號

這兩波 HN / 文章把「邊界」講得更具體：

- `Integrations gateway for agents with 2FA for destructive ops (OSS)`：高風險操作需要額外確認，2FA / approval 正在變成 product surface。
- `AgentPort – Open-source Security Gateway For Agents`：把 gateway / policy / approval 這些能力獨立出來，顯示 capability governance 正在產品化。
- `Local Figma Port`：把 scoped context 安全轉成 agent 能力，顯示來源資料與工具能力之間需要明確切邊。
- `Run coding agents in a sandbox locally`：sandbox、隔離與可審計性仍是必要條件。
- `Claude AI agent deletes company's database`：雖然是新聞敘事，但它提醒大家副作用控制不能靠「相信模型」解決。

## 2026-04-30：workspace scope、allowlisting 與 trust boundary 進一步產品化

這批訊號把邊界從「能不能接 tool」往「在哪個 workspace / directory / config scope 能接」推進：

- `Show HN: Shell-MCP, per-directory shell allowlisting for Claude Desktop`
  - 以 per-directory allowlisting 方式控制 shell capability，顯示權限治理開始精細到路徑層級。
- `Whose Trust Is It Anyway? Configuration Boundaries in AI Development Tools`
  - 這個標題本身就把焦點放在 config boundary：誰信任誰、哪一層負責授權、哪一層負責隔離。
- `Show HN: Nimbalyst open-source visual workspace for ClaudeCode, Codex, OpenCode`
  - 雖然比較偏 workspace / review，但它也強化了「能力邊界存在於共享控制平面」這個觀點。

這些訊號和原本的 capability separation 主題一致，只是更明確地把 boundary 從 API / tool 級，推進到 workspace / directory / config 級。

## 2026-05-04：SQL proxy 類型工具把 boundary 實作得更明確

- `QueryShield – secure SQL proxy for AI agents (NL→SQL, AST safety, RLS)`
  - 把 agent 與資料庫之間加上一層 proxy，讓 AST safety、RLS 與 SQL 風險控制變成可治理的邊界。
- `Unfortunately, Sprites Now Speak MCP`
  - 提醒我們：當 MCP 變成更通用的接線層時，真正重要的是 capability 要怎麼分隔、限縮與審批。

這讓原本的主題更具體：capability separation 不只是抽象原則，而是可以落在 SQL proxy、policy gateway 與 workspace scope 上。

## 對分享最有用的說法

你可以把它講成：

> MCP 的價值不只是把工具標準化，而是讓 agent 的能力邊界可以被清楚定義、分隔與治理。

再補一句：

> 真正的設計重點不是工具多不多，而是工具該暴露多少、誰能用、用到哪裡停。

## 建議閱讀順序

1. [近期 Agent 權限管理與 MCP 分隔資源整理](../queries/recent-agent-permissions-and-mcp-separation-resources.md)
2. [MCP Toolbox for Databases](mcp-toolbox-for-databases.md)
3. [Agent 生態近期熱點](agent-ecosystem-hot-topics.md)

## 相關來源

- [近期 Agent 權限管理與 MCP 分隔資源整理](../queries/recent-agent-permissions-and-mcp-separation-resources.md)
- [近期 Tech Signals 2026-04-30](../queries/recent-tech-signals-2026-04-30.md)

# AI Coding Agent 設計維度

## 目的

整理不同 AI coding agent 專案時，最值得比較的設計維度。這些維度不是功能清單，而是用來判斷一個 agent 系統為什麼會長成那樣、它適合什麼工作、又有什麼 trade-off。

## 核心維度

### 1. Model / Provider 策略

有些專案綁定特定模型或特定雲端生態，有些則刻意保持 provider-agnostic。

要看的問題：

- 是否能自由切換 model provider
- 是否把模型版本寫死在程式裡
- 是否支援本地模型、雲端模型、或多供應商路由

### 2. Tool Orchestration

agent 的核心不是聊天，而是怎麼安排 tool call。

要看的問題：

- tool 是一次一個，還是可並行執行
- tool output 如何回饋到下一輪 model call
- 是否有 planner / executor 分工
- 是否有專門的 scheduler、registry、hook 系統

### 3. Approval / Permission Model

一個 agent 能做多少事，往往取決於它的授權模型。

要看的問題：

- shell 指令是否要逐一確認
- file write / edit 是否需要 confirmation
- 是否有 policy engine 或 allowlist
- 是否支援 plan mode / read-only mode

### 4. Sandbox 與安全邊界

coding agent 一定會碰到本機檔案與命令執行，所以 sandbox 是核心設計。

要看的問題：

- 是否有 OS-level sandbox
- 是否限制 network access
- 是否區分 read-only 與 full access
- 是否有平台差異處理（macOS / Linux / Windows）

### 5. Subagent / Multi-agent 協作

很多進階 agent 不只是一個 loop，而是一組 agent 協作。

要看的問題：

- 是否支援 subagent
- 子 agent 是同權限還是只讀
- 是否有 task queue、team、mailbox、handoff 機制
- 是否能把大任務拆成平行工作

### 6. Memory 與 Context 管理

長對話或長任務都會面對 context 壓力。

要看的問題：

- 是否有 memory layer
- 是否有 auto-compact / summary
- 是否有 token budget 管理
- 是否把 project memory 和 global memory 分開

### 7. Extensibility

成熟的 agent 通常都有一層擴充機制。

要看的問題：

- 是否支援 MCP
- 是否支援 skills / plugins / hooks
- 是否支援自訂命令或自訂工作流程
- 是否容易接到外部系統

### 8. UI / Control Plane

同樣是 agent，操作界面差很多。

要看的問題：

- 是 terminal-first 還是 web / desktop-first
- 是單一 CLI，還是 client/server 架構
- 是否有遠端控制、手機端、或多通訊平台整合
- 是否把控制平面和 agent runtime 分離

## 常見設計型態

### Terminal-first coding agent

特徵通常是：

- 深度整合 shell、file、git
- 很重視 approval 與 sandbox
- 適合直接在 repo 裡做修改

### Local-first assistant platform

特徵通常是：

- 以個人裝置或私有 gateway 為核心
- 支援多 channel
- agent 本身比較像一個可路由的服務層

### Research / meta-workspace

特徵通常是：

- 不是直接做產品，而是研究產品
- 用 source/notes 的分層方式沉澱比較結果
- 適合長期觀察 agent 生態

## 為什麼這些維度重要

如果只看 demo，很容易被表面功能吸引；但真正決定 agent 可不可以長期使用的，通常是這些底層設計：

- 安全怎麼做
- 工具怎麼排
- 記憶怎麼壓縮
- 子任務怎麼切
- 可否在不同模型間切換
- 能不能自然接入既有工作流

## 和本 wiki 的關係

這份 wiki 之後如果要評估某個 agent 工具，建議先用這些維度做框架，再補充具體觀察：

- 它適合 coding 還是 assistant
- 它強在自由度還是安全性
- 它強在單人使用還是團隊協作
- 它適合直接進 repo 還是只適合做研究

## 關聯頁面

- `wiki/sources/agent-research.md`
- `wiki/topics/ingest-workflow.md`
- `wiki/topics/query-as-knowledge-production.md`

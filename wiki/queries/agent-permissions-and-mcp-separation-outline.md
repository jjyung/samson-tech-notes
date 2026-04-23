# Agent 權限管理與 MCP 分隔分享提綱

## 這次分享想講什麼

主題：**當 agent 透過 MCP 接外部能力時，怎麼把權限管理與能力邊界切清楚。**

一句話版本：

> MCP 的價值不只是標準化工具接入，而是讓 agent 的能力邊界可以被清楚定義、分隔與治理。

## 目標受眾

- 對 MCP 有聽過、但還沒完整用過的人
- 想把 agent 接資料庫、檔案、內部 API 的工程師
- 想理解 agent 安全與權限分層的人

## 建議開場

你可以先用這個問題開場：

> 如果 agent 能用很多工具，為什麼我們還要特別談權限管理？

接著馬上回答：

- 因為真正的風險不是「能不能做」，而是「能做到哪裡」
- agent 一旦拿到太大能力，就會有資料外洩、誤操作、越權、副作用放大等問題
- MCP 很適合拿來做 capability separation

## 內容結構

### 1. 為什麼要談權限管理

- agent 的風險通常來自外部能力過大
- 權限不是附屬議題，而是設計核心
- 沒有邊界就沒有可控性

可用的論述：

- 不是工具越多越好，而是工具暴露要剛好
- 不是模型越強越好，而是模型能力要被限制在對的邊界內

### 2. MCP 在這裡扮演什麼角色

- MCP 是 protocol / tool layer，不是 agent framework
- 它可以把外部能力整理成可控的 tools
- 它讓 capability 更容易被拆分、觀察與治理

你可以把 MCP 分成三層來講：

- **授權層**：OAuth / consent / scope
- **工具層**：tool definitions、read-only vs destructive
- **邊界層**：server、roots、sandbox、approval flow

### 3. 怎麼分隔能力

重點案例：

- **資料庫**：查詢工具和寫入工具拆開
- **檔案系統**：只給 roots，不給整台機器
- **內部 API**：敏感 API 放在更嚴格的 MCP server 後面

可強調的設計原則：

- least privilege
- default deny
- read/write separation
- high-risk action isolation
- human-in-the-loop approval

### 4. 你可以引用哪些標準 / 文件

- MCP Authorization
- MCP Security Best Practices
- MCP Tools / Roots
- OAuth 2.0 Security BCP
- OWASP Top 10 for LLM Applications
- NIST AI RMF GenAI Profile

### 5. 最後的 takeaway

可收斂成三句：

1. **MCP 不是只為了接工具，而是為了接得可控。**
2. **權限設計不是事後補強，而是 agent 架構的一部分。**
3. **真正重要的是 capability separation，而不是工具數量。**

## 5 分鐘版本

1. 問題：agent 為什麼需要權限管理
2. MCP 的角色：標準化工具接入
3. 三層架構：授權 / 工具 / 邊界
4. 分隔策略：read-only、sandbox、roots、approval
5. 結論：可控比強大更重要

## 10 分鐘版本

1. 動機與風險
2. MCP + authorization 的基本概念
3. tool gating 與 capability separation
4. 實務案例：database / filesystem / internal API
5. 相關標準與延伸閱讀
6. 結論與 Q&A

## 可搭配的 references

- [近期 Agent 權限管理與 MCP 分隔資源整理](recent-agent-permissions-and-mcp-separation-resources.md)
- [Agent 權限管理與 MCP 分隔](../topics/agent-permissions-and-mcp-separation.md)
- [MCP Toolbox for Databases](../topics/mcp-toolbox-for-databases.md)
- [Agent 生態近期熱點](../topics/agent-ecosystem-hot-topics.md)
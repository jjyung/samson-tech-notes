# 近期 Agent 權限管理與 MCP 分隔資源整理

## 問題意識

我最近想整理的是：**agent 的權限管理怎麼做**，尤其是當 agent 透過 **MCP** 接外部工具或資料來源時，怎麼把能力切開、把風險降下來。

這份整理的重點不是只看「能不能接」，而是看：

- 誰可以授權
- 哪些工具可見
- 哪些工具只讀、哪些會改資料
- 怎麼做 least privilege
- 怎麼把高風險能力隔離成獨立 MCP server / tool boundary

## 這次挑選的來源

### 1. Authorization — Model Context Protocol

- URL: [https://modelcontextprotocol.io/docs/concepts/authorization](https://modelcontextprotocol.io/docs/concepts/authorization)
- 類型: MCP 官方文件
- 日期: living doc
- 觀察：這是 MCP 權限與授權的核心參考。適合拿來說明 client / server / user 之間的授權關係，以及 MCP 本身如何看待 delegated access。

### 2. Security Best Practices — Model Context Protocol

- URL: [https://modelcontextprotocol.io/docs/concepts/security](https://modelcontextprotocol.io/docs/concepts/security)
- 類型: MCP 官方文件
- 日期: living doc
- 觀察：這是最直接的 MCP security 入口，適合討論 trust boundary、least privilege、server exposure 與整體風險控制。

### 3. Tools — Model Context Protocol

- URL: [https://modelcontextprotocol.io/docs/concepts/tools](https://modelcontextprotocol.io/docs/concepts/tools)
- 類型: MCP 官方文件
- 日期: living doc
- 觀察：工具定義是實際做權限隔離的地方。這頁很適合用來看工具 metadata、read-only vs destructive action 的區分方式。

### 4. Roots — Model Context Protocol

- URL: [https://modelcontextprotocol.io/docs/concepts/roots](https://modelcontextprotocol.io/docs/concepts/roots)
- 類型: MCP 官方文件
- 日期: living doc
- 觀察：如果你的 agent 要碰本機檔案或有限資源，Roots 是很好的 boundary 概念。它能把「可見範圍」縮到明確的工作目錄或資料夾。

### 5. OAuth 2.0 Security Best Current Practice (RFC 9700)

- URL: [https://www.rfc-editor.org/rfc/rfc9700](https://www.rfc-editor.org/rfc/rfc9700)
- 類型: IETF RFC
- 日期: 2024-03
- 觀察：雖然不是 MCP 專屬文件，但對於 MCP 類型的 delegated authorization 非常關鍵。很適合拿來補充 token 安全、授權流程與最佳實務。

### 6. The OAuth 2.0 Authorization Framework (RFC 6749)

- URL: [https://www.rfc-editor.org/rfc/rfc6749](https://www.rfc-editor.org/rfc/rfc6749)
- 類型: IETF RFC
- 日期: 2012-10
- 觀察：OAuth 的基礎規格。若要解釋 MCP 怎麼把 authentication / authorization 分開，這是最基本的參考。

### 7. OWASP Top 10 for Large Language Model Applications

- URL: [https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- 類型: OWASP 指南
- 日期: living project
- 觀察：特別適合補 agent / tool use 的風險語言，例如 excessive agency、prompt injection、tool abuse、缺少 human-in-the-loop 控制。

### 8. NIST AI RMF: Generative Artificial Intelligence Profile (AI 600-1)

- URL: [https://csrc.nist.gov/pubs/ai/600/1/final](https://csrc.nist.gov/pubs/ai/600/1/final)
- 類型: NIST 框架
- 日期: 2024
- 觀察：偏治理與風險管理，但很適合拿來說明 agent 系統如何做角色分工、logging、approval gate 與最小權限。

## 初步結論

這批資料看下來，agent 權限管理 + MCP 分隔的核心思路可以濃縮成三層：

1. **授權層**
   - 先確認誰授權、怎麼授權、token / scope 怎麼管。

2. **工具層**
   - 透過 MCP tool definitions、read-only tool、destructive tool 分開管理能力。

3. **邊界層**
   - 用 MCP server、roots、sandbox、獨立 service 把高風險操作隔離出去。

## 跟既有筆記的關係

這份研究最適合和下面幾頁一起看：

- [MCP Toolbox for Databases](../topics/mcp-toolbox-for-databases.md)
- [Agent 生態近期熱點](../topics/agent-ecosystem-hot-topics.md)
- [AI Coding Agent 設計維度](../topics/agent-coding-agent-design-dimensions.md)

如果你要分享的是「agent 不只是會用工具，而是要被限制在可控邊界內」，這份整理可以當基礎資料。

## 延伸方向

如果之後要繼續補，可以再分成這三條線：

- MCP authorization / OAuth / consent flow
- tool-level permission gating / read-write separation
- sandbox / root boundary / approval gate / human-in-the-loop
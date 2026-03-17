# CLI for Agents: Rewrite or Augment?

## Problem

隨著 AI Agents 開始大量操作開發工具（如 git、docker、cloud CLI），一個問題逐漸浮現：

> 傳統 CLI 是否適合 AI Agents 使用？

部分觀點認為 CLI 應重新設計（agent-first CLI），  
但另一個更務實的方向是：

> 是否只需在現有 CLI 上「加上 metadata」，即可滿足需求？

---

## Context

CLI 原本就是：

- 已存在且成熟的 execution interface
- 被 LLM 訓練資料大量涵蓋（天然會用）
- 低 token 成本（不需額外 schema）

但對 agent 來說仍存在問題：

- flags / free-form input 易出錯
- output 不易解析
- 缺乏語意描述（無 schema）
- 權限與安全風險較高

---

## The Landscape

在討論「要不要重寫 CLI」之前，有必要先建立整體框架。針對 agent tooling，目前常見的方式可以分成兩個層次：

**CLI 設計選擇**（直接回應「要不要重寫」這個問題）：

- **Rewrite CLI for Agents**：從頭設計 agent-native CLI
- **CLI + Metadata**：保留既有 CLI，加上語意層

**更廣義的 Agent Tooling 方式**（與 CLI 設計無關，但同樣在解決 agent 呼叫工具的問題）：

- **Skills**：以 prompt/instruction 描述能力
- **MCP / Tool Schema**：完整 schema 定義的工具介面

這個分層很重要，因為：

> CLI 的設計選擇（Rewrite vs Augment）與 Agent Tooling（Skills / MCP）其實是在不同層次解決問題。

---

## Approaches

### 1. Rewrite CLI for Agents

主張：

- JSON-first input / output
- schema introspection
- non-interactive
- idempotent design

👉 目標是打造 **agent-native CLI**

---

### 2. CLI + Metadata（Augmentation）

較低成本做法：

- 保留 CLI execution
- 補充 metadata（參數描述、用途、限制）
- 作為 agent 的「輕量語意層」

👉 可視為：

> CLI + minimal semantic layer

---

### 3. Skills（Prompt-based）

- 以 prompt / instruction 描述能力
- 無強制結構

👉 特性：

- context 成本低
- 但容易產生行為偏移（hallucination）

---

### 4. MCP / Tool Schema

- 完整 schema 定義
- 強型別與 validation

👉 特性：

- 高準確性
- 但 context 成本較高

---

## Comparison

以下比較並非絕對結論，而是目前常見實務觀察，實際效果會依 implementation 而異。

| 維度                | Skills                  | CLI + Metadata             | Rewrite CLI                | MCP                       |
| ------------------- | ----------------------- | -------------------------- | -------------------------- | ------------------------- |
| Interface type      | Prompt-based            | Command + metadata         | Command（JSON-first）      | Schema-driven             |
| Execution           | 間接（透過 agent 推理） | 直接（CLI）                | 直接（CLI）                | 間接（透過 tool backend） |
| Context usage       | 低                      | 低                         | 低                         | 較高（需攜帶 schema）     |
| Constraint level    | 低（描述性）            | 中（透過 command 約束）    | 高（透過設計約束）         | 高（型別與 schema）       |
| Predictability      | 低                      | 中                         | 高                         | 高                        |
| Safety model        | 依 prompt 控制          | 需額外 sandbox / guardrail | 需額外 sandbox / guardrail | 較容易集中控管            |
| Implementation cost | 低                      | 中                         | 高（需重新設計）           | 高                        |

---

## Conclusion

CLI 並不需要被完全重寫。

- CLI 本來就是 execution layer，不需要被取代
- Skills 成本最低，但缺乏約束，容易出現行為偏移
- MCP 提供最完整的語意與安全性，但 context 成本高

不同 agent tooling 的核心差異，其實在於：

> **Constraint（約束力） vs Cost（context / implementation 成本）**

**CLI + Metadata** 是介於中間的務實選項：比 Skills 更具執行約束，比 MCP 更輕量

在許多場景下：

> **透過 metadata augment CLI，即可在成本與控制之間取得平衡**

最終架構可能不是單一解法，而是：

- Skills（輕量描述）
- CLI（執行能力）
- MCP（強結構工具）

三者共存，依場景選擇。

---

## References

- **[You Need to Rewrite Your CLI for AI Agents][ref-google]** (Justin Poehnelt, Google)  
  指出傳統 CLI 為 human 設計，需轉向 JSON、可預測輸出與 idempotent execution。

- **[Rewrite Your CLI for Agents or Get Replaced][ref-dev-rewrite]** (DEV Community)  
  強調 CLI 應轉為 machine-friendly interface，並提出 JSON-first、schema-aware 等設計方向。

- **[Hacker News Discussion: You Need to Rewrite Your CLI for AI Agents][ref-hn]**  
  討論指出 CLI 本身未必需要重寫，關鍵在於輸出結構與使用方式。

- **[Writing CLI Tools That AI Agents Actually Want to Use][ref-dev-writing]**  
  分享實務經驗：透過結構化輸出與簡化設計，使既有 CLI 更適合 agent 使用。

- **[Terminal Is All You Need][ref-arxiv]** (arXiv, 2026)  
  指出 terminal 仍是 agent 與系統互動的重要介面，具備通用性與低成本優勢。

[ref-google]: https://www.ithome.com.tw/news/174225
[ref-dev-rewrite]: https://dev.to/meimakes/rewrite-your-cli-for-agents-or-get-replaced-2a2h
[ref-hn]: https://news.ycombinator.com/item?id=47252459
[ref-dev-writing]: https://dev.to/uenyioha/writing-cli-tools-that-ai-agents-actually-want-to-use-39no
[ref-arxiv]: https://arxiv.org/abs/2603.10664

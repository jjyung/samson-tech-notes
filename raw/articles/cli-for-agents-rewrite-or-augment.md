# CLI for Agents: Rewrite or Augment?

## Problem

隨著 AI Agents 開始大量操作開發工具（如 git、docker、cloud CLI），一個問題逐漸浮現：

> 傳統 CLI 是否適合 AI Agents 使用？

部分觀點主張：

> CLI 應重新設計為 agent-first（JSON-first、schema-driven）

但實務與社群討論逐漸顯示：

> 問題不在「是否重寫 CLI」，而在「CLI 是否對 agent 友善」

---

## Context

CLI 原本就是：

- 成熟且廣泛存在的 execution interface
- 被 LLM 訓練資料大量涵蓋（天然會用）
- token 成本低（相比 schema / MCP）

但在 agent 使用場景中，仍存在挑戰：

- output 不易解析（table / text 混合）
- interactive 行為難以自動化
- flags 與參數增加推理成本
- 缺乏可預測性（predictability）

然而實務經驗顯示：

> agent 並不需要「完美結構化 CLI」，而是需要「不阻礙使用」的 CLI ([Hacker News](https://news.ycombinator.com/item?id=47252459))

---

## The Real Shift

「Rewrite CLI」是一個過度簡化的 framing。

實際上，業界觀察收斂到：

> ❌ CLI 不需要被重寫  
> ✅ CLI 需要變得 **machine-readable**

關鍵能力包括：

- JSON output（`--output json`）
- non-interactive execution
- 明確 exit codes
- deterministic behavior

這些改動通常是「incremental improvement」，而非重構整個 CLI。

---

## Human DX vs Agent DX

這個討論的核心，其實不是 CLI，而是：

> 👉 **使用者是誰？**

---

### Human DX

- 可讀性（readability）
- 可探索性（discoverability）
- 容錯性（forgiving）

---

### Agent DX

- 可解析性（machine-readable）
- 可預測性（predictability）
- 可約束性（constraint）

---

這兩者之間存在天然張力：

- JSON-first 對 agent 友善
- 但對 human 不友善

---

## The False Dichotomy

因此，一個常見但錯誤的假設是：

```text
CLI 必須選擇：
human-first 或 agent-first
```

---

## 實際上更合理的模型是

> 👉 **Dual-mode CLI**

---

## Dual-Mode CLI

CLI 不會變成 agent 專用工具，而是：

> **同時服務 multiple consumers**

---

### Human mode

```bash
mycli deploy --env prod
```

- readable output
- pretty formatting

---

### Agent mode

```bash
mycli deploy --json '{ "env": "prod" }'
mycli deploy --output json
```

- structured output
- deterministic parsing

---

👉 這種設計在實務上已經出現：

- TTY-aware output（人類 vs pipe）
- `--json` flag
- 分離 stdout / stderr ([DEV Community](https://dev.to/meimakes/rewrite-your-cli-for-agents-or-get-replaced-2a2h))

---

## The Architecture Model

在 agent architecture 中，可以拆成三個層次：

---

### 1. Guidance（Skills）

- prompt / instruction
- 描述如何使用工具

👉 提供：

> **guidance**

---

### 2. Execution（CLI）

- command interface
- 實際執行操作

👉 提供：

> **execution grounding**

---

### 3. Constraint（Schema / MCP）

- typed schema
- validation

👉 提供：

> **constraint**

---

## Hallucination vs Constraint

Justin Poehnelt 提到：

> “A skill file is cheaper than a hallucination.”
> [https://justin.poehnelt.com/posts/rewrite-your-cli-for-ai-agents/](https://justin.poehnelt.com/posts/rewrite-your-cli-for-ai-agents/)

這句話的正確解讀是：

> 提供 guidance 比讓 agent 自己猜更好

---

### 但關鍵不是 skill

而是：

> 👉 **constraint**

---

## 控制能力光譜

```text
No guidance
→ hallucination ❌

Skill（guidance）
→ 減少 hallucination ⚠️

CLI（execution grounding）
→ 更穩定 ✅

Schema（constraint）
→ 幾乎消除 ✅
```

---

## 核心模型

| 層級   | 本質       |
| ------ | ---------- |
| Skill  | Guidance   |
| CLI    | Execution  |
| Schema | Constraint |

---

## Key Insight

> Skills guide the model
> CLI executes the action
> Schema enforces correctness

---

## Approaches Revisited

### 1. Rewrite CLI（Agent-first）

- JSON-first
- schema introspection

👉 適合：

- greenfield system

---

### 2. Improve Existing CLI（主流）

- `--output json`
- non-interactive
- clear exit codes

👉 多數實務採用

---

### 3. Skills / MCP

- Skills → guidance
- MCP → constraint

👉 與 CLI **互補，而非替代**

---

## Conclusion

CLI 不會被 agent 取代，也不會變成 agent 專用。

真正的演進方向是：

> **CLI 成為 dual-mode interface**

- human-friendly
- machine-readable

---

而 agent system 的核心問題，也不是工具選擇，而是：

> **如何在 guidance、execution、constraint 之間取得平衡**

---

## Final Insight

> The future of CLI is not agent-first or human-first
> but **dual-mode: human-friendly and machine-readable**

---

## References

- [You Need to Rewrite Your CLI for AI Agents](https://justin.poehnelt.com/posts/rewrite-your-cli-for-ai-agents/) — Justin Poehnelt
- [Hacker News Discussion](https://news.ycombinator.com/item?id=47252459)
- [Rewrite Your CLI for Agents or Get Replaced](https://dev.to/meimakes/rewrite-your-cli-for-agents-or-get-replaced-2a2h) — DEV Community
- [Designing CLIs for AI Agents: Patterns That Work in 2026](https://medium.com/@dminhk/designing-clis-for-ai-agents-patterns-that-work-in-2026-29ac725850de) — Medium
- [CLI Agents and Agentic Workflows](https://medium.com/@takafumi.endo/cli-agents-and-agentic-workflows-when-workflow-becomes-invisible-164a7484d3fc) — Medium
- [Terminal-Native Agents](https://arxiv.org/html/2603.05344v1) — arXiv

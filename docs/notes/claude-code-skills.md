# Claude Code Skills - Distilled Note

## Problem

Prompt 很難重用，context window 成本高，agent 容易 hallucinate。

---

## Insight

Skill 不是 markdown，而是一個可執行的工作模組（folder）。

它可以包含：

- scripts
- data
- config
- hooks

---

## Key Principles

### 1. 不要寫模型已知知識

寫「人類踩過的坑（gotchas）」

### 2. Scripts > 說明

讓 agent 直接做，而不是推理

### 3. Skill 是可演化的

從小工具開始，逐步累積

---

## My Take

Skill = Agent 時代的 Library

它解決的是：
「如何把經驗轉成可重用能力」

---

## Connection

- CLI → skill wrapper
- MCP → runtime tool
- Skill → knowledge layer

---

## Reference

- [Lessons from Building Claude Code: How We Use Skills](https://x.com/trq212/status/2033949937936085378)

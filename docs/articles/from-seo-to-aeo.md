# From SEO to AEO: Why Agent DX is Rewriting How We Design Content

## TL;DR

傳統 SEO 是讓「搜尋引擎找到你」，  
AEO（Answer Engine Optimization）是讓「AI 直接用你當答案」。

而 llms.txt，正是這個轉變中的第一個「Agent-friendly interface」。

---

## Problem

過去 20 年，網路內容設計的核心是：

> Human-first discovery

- 內容寫給人看
- 搜尋引擎負責索引與排序
- 使用者點擊 → 閱讀 → 自行整理答案

但 AI 搜尋改變了這件事：

> 使用者不再找「頁面」，而是直接要「答案」

這導致新的系統需求：

- 可理解（understandable）
- 可抽取（extractable）
- 可引用（citable）

👉 而 HTML 並不是為這件事設計的

---

## Context: SEO → AEO

### SEO

- 單位：Page
- 目標：Ranking
- 成功指標：Clicks

---

### AEO（Answer Engine Optimization）

AEO 的核心是：

> 將內容設計成「可被 AI 直接使用作為答案」 [AEO 定義][aeo-core]

也就是：

- AI 能理解
- AI 能抽取
- AI 願意引用

👉 本質轉變：

| 面向       | SEO   | AEO             |
| ---------- | ----- | --------------- |
| 目標       | 排名  | 成為答案        |
| 單位       | Page  | Knowledge chunk |
| 使用者行為 | Click | No-click        |
| 成功指標   | 流量  | 被引用          |

👉 SEO → AEO：

> 從「被找到」→「被使用」

---

## Why AEO Emerges

### 搜尋變成 Answer Engine

現代搜尋系統：

- 理解問題
- 整合多來源
- 直接生成答案

👉 搜尋正在從 link list 轉向 answer layer [AEO 轉變][aeo-shift]

---

### 使用者行為改變

- Zero-click search
- 不再瀏覽網站

👉 成功變成：

> 被 AI 引用，而不是被點擊 [AEO 引用][aeo-citation]

---

## llms.txt: The Missing Layer

### llms.txt 是什麼

llms.txt 是：

- 一個放在 `/llms.txt` 的文件
- 提供 AI 可讀內容索引
- 幫助 LLM 理解網站內容

👉 本質：

> 幫助 AI 有效率理解與使用網站內容 [llms-definition][llms-definition]

---

### llms.txt 解決的問題

LLM 在 web 上的問題：

- HTML 太 noisy
- 無法判斷重要內容
- context window 有限

👉 llms.txt 提供：

- curated content index
- 明確優先順序

---

### 類比（非常關鍵）

| 機制         | 對象          |
| ------------ | ------------- |
| robots.txt   | crawler       |
| sitemap.xml  | search engine |
| **llms.txt** | AI agent      |

👉 更精準的說法：

> llms.txt 是 AI 時代的「內容 routing layer」 [llms-role][llms-role]

---

### 更進一步（你的觀點）

> 🔥 llms.txt = Agent DX 的 Discovery Layer

---

## AEO as System Design

AEO 不是行銷技巧，而是資訊架構問題

---

### Discovery Layer

- llms.txt
- sitemap

👉 解決：去哪找

---

### Retrieval Layer

- RAG / embedding

👉 解決：找什麼

---

### Representation Layer

- Markdown
- FAQ
- structured content

👉 解決：怎麼理解

---

### Authority Layer

- citation
- entity signals

👉 解決：信不信

---

## Design Principles

### Write for extraction

- 一段回答一個問題

---

### Prefer structure over prose

- 標題清楚
- 條列化

---

### Minimize ambiguity

- 定義明確
- 避免模糊語言

---

### Optimize for citation

- 提供結論句
- summary

---

### Design for chunking

- 每段可獨立引用

---

## Trade-offs

### 👍 優點

- 提升 AI 可見度
- 降低 hallucination
- 提高引用率

---

### 👎 限制

- 尚未標準化
- AI 不一定採用
- 對 SEO 影響有限

👉 有觀點指出：

> llms.txt 目前仍屬 early-stage，效果有限 [llms-risk][llms-risk]

---

## Insight

> 🔥 AEO 是「Content → Interface」的轉變

內容不再只是：

👉 給人閱讀  
而是：

👉 給 AI 使用

---

## Agent DX Stack

```mermaid
flowchart LR
    A["Discovery<br/>llms.txt"] --> B["Retrieval<br/>RAG"]
    B --> C["Representation<br/>structured content"]
    C --> D["Execution<br/>tools / MCP"]
```

---

## Conclusion

AEO 不是 SEO 的替代，而是進化：

- SEO：讓人找到你
- AEO：讓 AI 使用你

而 llms.txt：

> 👉 是這個轉變中的第一層協議

---

## References

- [Answer Engine Optimization — Conductor Academy][aeo-core]
- [AEO: Evolving Your SEO Strategy in the Age of AI Search — Amsive][aeo-citation]
- [Answer Engine Optimization (AEO): The Comprehensive Guide — CXL][aeo-shift]
- [What is llms.txt? — AIOSEO][llms-definition]
- [How llms.txt Supports Answer Engine Optimization — Artversion][llms-role]
- [llms.txt: What It Is and Why It Matters — Webflow][llms-risk]

[aeo-core]: https://www.conductor.com/academy/answer-engine-optimization/
[aeo-citation]: https://www.amsive.com/insights/seo/answer-engine-optimization-aeo-evolving-your-seo-strategy-in-the-age-of-ai-search/
[aeo-shift]: https://cxl.com/blog/answer-engine-optimization-aeo-the-comprehensive-guide/
[llms-definition]: https://aioseo.com/what-is-llms-txt/
[llms-role]: https://artversion.com/blog/how-llms-txt-supports-answer-engine-optimization-aeo/
[llms-risk]: https://webflow.com/blog/llms-txt

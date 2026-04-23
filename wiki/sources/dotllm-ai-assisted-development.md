---
aliases:
  - dotLLM 與 AI 輔助開發的工程方法
---
# dotLLM 與 AI 輔助開發的工程方法

## Source

- Title: `Introducing dotLLM - Building an LLM Inference Engine in C#`
- Author: `Konrad 'Dev Nerd' Kokosa`
- Published: `2026-04-14`
- Type: 技術文章 / 專案回顧
- URL: [https://kokosa.dev/blog/2026/dotllm/](https://kokosa.dev/blog/2026/dotllm/)

## 摘要

這篇文章一方面介紹 `dotLLM` 這個以 C#/.NET 10 原生實作的 LLM inference engine，另一方面更重要的是分享作者如何用高度工程化的 AI 協作流程，在約兩個月內由單人完成一個原本看起來需要整個團隊才能推動的系統級專案。

文章的真正亮點不只是「AI 幫忙寫了很多程式」，而是作者把 AI 放進一個被嚴格拆分、文件化、可審查的開發流程裡。透過 phase、issue、PR、review、修復 wave、設計文件與行為規範，AI 的不穩定性被限制在可控範圍內，最後組裝出一個功能完整而且可持續演進的成果。

## dotLLM 是什麼

`dotLLM` 是一個原生 C#/.NET 10 的 LLM 推論引擎，支援：

- GGUF 模型載入
- tokenizer、attention、sampling 等完整推論流程
- SIMD 最佳化 CPU 推論
- CUDA GPU 加速
- OpenAI 相容 API server
- 內建 chat UI
- CLI 與 NuGet 套件形式發佈

作者強調它不是 wrapper，不是 bindings，而是從底層開始的完整實作。這個選擇本身就帶有明顯的工程意圖：不依賴外部 Python 服務，不只是整合現有工具，而是直接掌握推論引擎的架構與效能特性。

## 文章最值得記住的重點

### 1. AI 成功的關鍵不是自由發揮，而是明確邊界

作者明說這不是「prompt and pray」，也不是把需求丟給 AI 後放著不管。相反地，整個專案被切成大約 60 個 implementation steps，分成 7 個 phase，每一步都有清楚範圍、相依關係與驗收標準。

這代表 AI 不是在「解一個巨大模糊問題」，而是在「完成一個被約束好的子問題」。

### 2. 文件不是附屬品，而是方法論本身

文章中最強的一句話是：寫給 AI 的結構化文件，不是開發的額外負擔，而就是開發方法本身。

作者提到三種高價值文件：

- `ROADMAP.md`：定義步驟、順序、相依性
- `CLAUDE.md`：定義 AI 在專案中的行為規則與 coding constraints
- `/docs/` 設計文件：定義各子系統的架構與實作邊界

這些文件讓 AI 不是靠猜，而是在規範內實作。

### 3. 規劃與實作必須分離

作者的流程裡，先規劃、再實作，而且規劃要先經過人工批准。這讓 AI 在真正動手前就先被導到正確方向，降低因誤解需求而造成的大量返工。

這個分離特別重要，因為 AI 很擅長快速生成，但如果方向錯了，也會很快地生成大量錯的東西。

### 4. 寫程式的 AI 不應該是唯一的 reviewer

在這個專案中，Claude Code 主要負責實作，而 Codex 與 Gemini 被拿來做 PR review。作者強調不同模型的盲點不同，因此讓不同模型扮演不同角色，比單一模型從頭到尾包辦更可靠。

文章還給了具體例子，例如：

- ring buffer indexing bug
- pinned buffer scope 問題
- race condition
- constrained decoding 的 cache key collision
- CUDA kernel 的架構層級問題

這些都不是表面瑕疵，而是會真的導致錯誤或品質下降的問題。

### 5. 工程拆分可以把 AI 的不穩定輸出壓縮成穩定成果

這篇文章最有啟發性的地方，在於它展示了：即使 AI 本身會有幻覺、誤判、遺漏與盲點，只要整體流程被設計得夠好，系統最終輸出的品質仍然可以很穩定。

穩定性不是來自單次生成的完美，而是來自：

- 問題拆分
- 邊界清楚
- 文件先行
- 規劃先於實作
- 多角色審查
- 持續修補與 hardening

## 效能與現實感

作者沒有把 `dotLLM` 包裝成已經超越 `llama.cpp` 的產品，反而很誠實地說明現況：

- decode throughput 約達到 `llama.cpp` 的 66% 到 88%
- prefill 仍慢很多，約落後 2 到 5 倍
- CUDA backend 還在早期調校階段

這個誠實很重要，因為它說明工程化不是保證一開始就最強，而是讓系統能在正確方向上持續逼近。

## 我讀到的核心啟發

這篇文章非常支持一個重要觀點：

AI 本身不必完美，關鍵是能不能透過工程把它的能力放大，並把輸出的波動收斂到可接受範圍。

也就是說，價值不只來自模型能力本身，還來自你如何設計整個工作系統：

- 怎麼拆任務
- 怎麼定義規格
- 怎麼切 review 關卡
- 怎麼讓不同模型互補
- 怎麼把每一步做成可驗證、可回滾、可追蹤

這其實很像傳統工程的精神：不是期待元件永遠完美，而是透過架構、流程與驗證，把整體系統做得可靠。

## 與這個 Repo 的關聯

這篇文章和本 repo 很契合，因為它強化了兩個方向：

- [LLM Wiki](llm-wiki.md) 講的是如何用流程與結構維護知識
- [dotLLM 與 AI 輔助開發的工程方法](dotllm-ai-assisted-development.md) 講的是如何用流程與結構穩定 AI 開發

兩者共同點都是：

- 不依賴一次性的神奇輸出
- 把 AI 放進有結構的系統中
- 讓價值來自累積、維護與組裝，而不是單次 prompt

## 可延伸頁面

- [工程化讓 AI 輸出更穩定](../concepts/engineering-stabilizes-ai-output.md)
- [AI 輔助開發工作流](../topics/ai-assisted-development-workflow.md)
- [多模型 Review](../topics/multi-model-review.md)

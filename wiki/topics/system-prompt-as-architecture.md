---
aliases:
  - Prompt as Architecture
  - Claude Design Prompt Architecture
  - 系統提示 / 架構
---
# 系統提示即架構

## 目的

把 system prompt 看成架構設計，而不是單純的文字指令。

這個觀點的核心是：好的 prompt 不只描述任務，還會提前定義身份、邊界、品味、流程、工具協議與驗證方式，讓 agent 的行為在一開始就被導向可控的軌道。

## 核心模式

### 1. Identity / Guardrails

先定義 agent 是誰、對誰負責、不能做什麼。

這一層決定了整個 system prompt 的方向：

- 是協作者，還是工具人
- 是面向使用者語言，還是暴露內部工具
- 哪些訊息必須避免洩漏

### 2. Taste / Discipline

再定義什麼叫好輸出，以及哪些模式要避免。

常見做法包括：

- 先建立設計系統再動手
- 不塞 filler content
- 加東西前先問
- 不從空白開始
- 給 3+ 變體，而不是只猜一個答案
- 從品牌與既有系統中取色，而不是自創

這層其實是在把審美變成可執行規則。

### 3. Workflow / Process

接著把工作的順序固定下來。

一個穩定的 prompt 往往會要求 agent：

- 先理解需求
- 讀上下文與相關資源
- 規劃步驟
- 早點展示中間結果
- 完成後再驗證
- 最後只做極簡總結

這樣的流程能避免 agent 一上來就直接生成成品、然後一路偏掉。

### 4. Tools / Protocols

工具本身不是重點，重點是工具怎麼被編排。

好的 prompt 會明確規定：

- 哪些工具在什麼階段使用
- 中間過程如何回饋
- 何時需要 verification
- 何時可以 silent on pass

這讓工具使用變成系統行為，而不是臨場反應。

### 5. Technical Specs

最後才是具體的技術要求，例如：

- 尺度
- 格式
- 結構
- layout rules
- implementation constraints

如果前面的層次已經做好，這些規則通常只是收尾，不是整個 prompt 的主體。

## 為什麼這個觀點重要

把 prompt 當架構，會帶來幾個好處：

- 更少 slop
- 更穩定的輸出
- 更容易驗證
- 更容易擴充
- 更容易把 prompt 和工作流對齊

這也是很多高品質 agent 工作流共同具備的特徵：不是靠單句神奇指令，而是靠整體系統設計。

## 和本 wiki 的關係

這個 topic 與以下頁面特別相關：

- [AI Coding Agent 設計維度](agent-coding-agent-design-dimensions.md)
- [AI 輔助開發工作流](ai-assisted-development-workflow.md)
- [工程化讓 AI 輸出更穩定](../concepts/engineering-stabilizes-ai-output.md)
- [Plan-Gate-Execute](../../raw/articles/plan-gate-execute.md)

它可以當作寫 system prompt、workflow prompt、design prompt 的共同框架。

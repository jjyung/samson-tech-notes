---
aliases:
  - ADK Workflow vs Skill Prompt
  - Workflow 與 Skill 分層
---
# ADK Workflow vs Skill / Prompt 的分層本質

## 一句話差異

- `ADK workflow` 負責 **控制流程（Control Flow / Orchestration）**
- `Skill / Prompt` 負責 **定義能力（Capability / Execution Unit）**

## 抽象層級

### ADK Workflow（系統層）

- 關注流程控制（if / loop / branching）
- 關注狀態管理（state）
- 關注多 agent 協作與步驟編排
- 比較接近 BPMN / state machine / orchestrator

核心問題：

> 我怎麼讓整個系統穩定地跑起來？

### Skill / Prompt（能力層）

- 關注單一任務執行（查詢、生成、呼叫 API、腳本運算）
- 主要是可重用的任務能力模組
- 比較接近 function / tool / micro capability

核心問題：

> 這個 agent 會做什麼？

## 控制權與穩定性

### Skill / Prompt 主導時

- 控制權在 LLM
- 路徑由模型即時決策
- 容易出現不穩定、不可預測、難 debug

常見症狀：

- 同樣輸入今天走 A，明天走 B
- 某些關鍵步驟被略過

### Workflow 主導時

- 控制權在工程邏輯（workflow engine / code）
- 路徑以規則與狀態為主
- 可預期、可測試、可觀測

## 可測試性與維運性

| 面向 | Skill / Prompt | ADK Workflow |
| --- | --- | --- |
| 可測試性 | 低 | 高 |
| 可觀測性 | 低（黑箱） | 高（可追 state） |
| 除錯方式 | 反覆調 prompt | 可 step-by-step 定位 |
| 穩定性 | 易波動 | 較穩定 |

## 規模判斷

### 適合 Skill / Prompt

- 單步或弱流程任務
- 探索型任務（exploration）
- 可容忍一定不穩定
- 不要求完整 audit / trace

例子：

- 幫我總結新聞
- 產生 trading insight 草稿
- 轉換輸出格式

### 適合 ADK Workflow

- 長流程、多步驟決策
- 有條件分支與狀態轉移
- 需要 retry / guardrail / gating
- 有不能錯的商業規則

例子：

- 交易進出場與風險控管
- 企業流程的審核、執行、記錄、計費
- 「先檢查狀態，不符合就先詢問使用者」這類 gating

## 常見反模式

用 prompt 硬寫 workflow，例如：

```text
If condition A do this, otherwise ask user...
```

風險：

- 模型可能忽略條件
- 模型可能自行改路徑
- 高風險場景（如交易 / 金融）容易出現不可接受錯誤

## 建議設計模式：Workflow + Skill 分層

```text
[ADK Workflow]
    ↓
流程決策（順序、分支、重試、gating）
    ↓
呼叫 Skill
    ↓
Skill 執行（LLM / API / Script）
```

交易代理的典型拆法：

1. 取得市場資料（skill）
2. 計算指標（script skill）
3. 判斷 regime（workflow）
4. 不確定則請求使用者確認（workflow gate）
5. 產生決策候選（LLM skill）
6. 風險檢查與阻擋（workflow）
7. 輸出結果與記錄（workflow）

## 可直接引用的結論

> Prompt-based agent 是讓 AI 自己決定流程；  
> Workflow-based agent 是人類定義流程，AI 負責執行能力。

## 在平台設計上的落地建議

- 把核心流程放在 workflow：entry / exit、risk control、state check、human-in-the-loop gate
- 把可替換能力放在 skill：模型判斷、外部 API、計算腳本、內容生成
- 用「流程穩定性」與「能力可替換性」做責任邊界切分

## 關聯頁面

- [AI Coding Agent 設計維度](agent-coding-agent-design-dimensions.md)
- [Agent 權限管理與 MCP 分隔](agent-permissions-and-mcp-separation.md)
- [AI 輔助開發工作流](ai-assisted-development-workflow.md)

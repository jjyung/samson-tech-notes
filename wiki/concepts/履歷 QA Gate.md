# 履歷 QA Gate

## 核心想法

履歷不是一般內容產生任務，而是高風險聲明任務。任何 JD-tailored 內容在匯出前，都應該經過 QA gate，確認沒有事實錯誤、日期衝突、捏造數字或錯誤聲稱。

## QA 要檢查什麼

- unsupported claims 是否為 0
- date conflicts 是否為 0
- 是否誤報 must-have
- metrics 是否被捏造
- skills 是否都有 evidence_ref
- 排版是否 ATS-friendly
- 日期與時態是否一致

## 為什麼重要

沒有 QA gate 的履歷 workflow，會把「看起來像真的」和「真的可證明」混在一起。這在履歷場景裡是不可接受的。

## 建議的阻擋條件

任何一項成立，就應該 block 或回到前一輪重寫：

- 任一 unsupported claim
- 任一 date conflict
- 重要 must-have 被錯誤聲稱已具備
- 明顯的 fabricated metric
- 內容無法追溯到 evidence

## 實作建議

- 用結構化 JSON 做 QA 結果
- 把 blocker 和 warning 分開
- 讓 QA 成為 pipeline 的硬閘門，而不是最後才看一眼

## 相關頁面

- [履歷與 CV 的 LLM Agent 工作流](../topics/履歷與 CV 的 LLM Agent 工作流.md)
- [履歷證據庫](履歷證據庫.md)
- [履歷 JD Mapping](履歷 JD Mapping.md)
- [履歷量化追問](履歷量化追問.md)
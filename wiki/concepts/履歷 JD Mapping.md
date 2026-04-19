# 履歷 JD Mapping

## 核心想法

JD mapping 的目標不是直接改寫履歷，而是先把職缺要求和候選人證據一一對齊。先做 mapping，後做 rewrite，流程會穩很多。

## 需要抽出的內容

- target title
- seniority
- must-have
- nice-to-have
- keywords
- domain
- hard skills
- soft skills
- do_not_claim

## 為什麼要先 mapping

如果沒有 mapping，模型很容易直接生成「像這份職缺想要的樣子」，卻沒有把內容和證據對上。

先 mapping 的好處是：

- 可清楚看到 gap
- 可分辨 transferable skill 和真正具備的能力
- 可避免誤報 must-have
- 可把重寫限制在有證據支撐的範圍內

## 實作建議

- 把 JD 分解成結構化欄位
- 為每個 requirement 找到最強 evidence_ref
- 對無法支持的要求直接列入 `do_not_claim`
- 把匹配結果當成後續 rewrite 的輸入契約

## 相關頁面

- [[履歷與 CV 的 LLM Agent 工作流]]
- [[履歷證據庫]]
- [[履歷 QA Gate]]
- [[履歷與 CV 的 LLM Agent 工作流公開資源研究]]

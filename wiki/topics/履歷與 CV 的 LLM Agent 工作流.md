# 履歷與 CV 的 LLM Agent 工作流

## 目的

這是一個把履歷 / CV 相關公開資源整理成可重用 workflow 的主題頁。重點不是蒐集 prompt，而是把「履歷生成、客製化、評估、匯出」拆成可驗證的步驟。

## 這個主題在看什麼

公開世界裡的相關資源大致分成幾類：

- 履歷客製化工具，例如 Resume Matcher
- skill/package 形式的 agent，例如 Wscats/resume-assistant、resume-assistant-skill
- prompt + workflow 套件，例如 resumePolice
- Resume as Code 類型的版本化履歷系統
- ingest / parser 層，例如 linkedin-resume-parser
- 輸出層 builder，例如 OpenResume、Reactive Resume

這些資源共同指向一件事：履歷任務不缺模型能力，缺的是穩定流程。

## 最重要的設計原則

### 1. 先結構化，再改寫

不要一開始就直接叫模型「幫我改履歷」。比較可靠的做法是：

1. 先把來源抽成固定 schema
2. 再建立 evidence / timeline
3. 再分析 JD
4. 再做 gap analysis
5. 再改寫 summary、skills、bullets

### 2. 先比對，再聲稱

所有 JD-tailored 的內容都應該來自可追溯的 evidence。若證據不足，應該輸出 `unspecified`、`null` 或 `measurement_placeholder`，而不是硬補。

### 3. 先 QA，再匯出

履歷是高風險內容，因為它牽涉事實、資歷、數字與職務聲稱。最穩健的做法是把 QA gate 放在輸出前：

- unsupported claims = 0
- date conflicts = 0
- 重要 must-have 不可誤報
- metrics 不能捏造
- ATS 友善格式要先過檢查

### 4. 人工核對不能省

AI 可以幫忙整理、重寫、排版，但候選人本人仍必須對事實負責。所有 tailored bullets、summary 與 metrics 最後都要回到原始證據核對。

## 建議的標準工作流

### A. Ingest / Parse

把原始履歷、LinkedIn export、PDF、筆記整理成結構化資料。

建議 schema：

- basics
- experience
- projects
- education
- skills
- certificates
- evidence spans

### B. Build Evidence Library

把每段經歷變成可重用的 evidence entry / timeline item，讓不同 JD 可以重組同一批事實。

### C. Analyze JD

抽出：

- must-have
- nice-to-have
- seniority
- domain
- hard skills
- soft skills
- keywords

### D. Gap Analysis

把需求分成三類：

- 已有證據，可以聲稱
- 可轉譯成 transferable skill，但要小心措辭
- 沒有證據，不可聲稱

### E. Rewrite

優先順序通常是：

1. Summary
2. Skills
3. Experience bullets
4. Projects

重寫時的原則：

- action verb + contribution + result
- 沒有真實數字就不要捏造
- 只保留對目標職位有意義的內容

### F. Quantify

若原始資料沒有數字，就先標 placeholder，而不是補假數字。之後再追問候選人補證據。

### G. QA / ATS Check

檢查：

- 標題是否標準
- 是否有表格 / 花式排版
- 關鍵字覆蓋是否足夠
- 日期與時態是否一致
- 事實是否可追溯

### H. Export

先通過 QA，再用 builder / template 匯出 Markdown、PDF、DOCX 或 HTML。

## 這個 workflow 為什麼可靠

因為它把履歷任務拆成多個可控節點，而不是只依賴單次生成品質。這跟本 wiki 中的幾個 concept 很一致：

- [[持久化 Wiki 與 RAG 的差異]]：知識先被整理成可維護資產
- [[工程化讓 AI 輸出更穩定]]：用流程壓低模型波動
- [[Query 即知識生產]]：高價值結果可以回寫成長期頁面
- [[Ingest 工作流]]：來源應該先被整理，再進入知識層

## 對實作的建議

如果要真的落地，最實用的順序通常是：

1. 先做 parser / normalize
2. 再做 JD matcher
3. 再做 rewrite agent
4. 再做 quantification coach
5. 再做 QA guard
6. 最後接 builder / exporter

如果只想先做最小版本，至少也要具備：

- 結構化輸入
- evidence 對照
- 不能捏造的約束
- 最後人工審核

## 可拆出的概念頁

- [[履歷證據庫]]
- [[履歷 JD Mapping]]
- [[履歷 QA Gate]]
- [[履歷量化追問]]
- [[ATS 友善輸出]]

## 相關頁面

- [[履歷與 CV 的 LLM Agent 工作流公開資源研究]]
- [[Ingest 工作流]]
- [[Query 即知識生產]]
- [[工程化讓 AI 輸出更穩定]]
- [[持久化 Wiki 與 RAG 的差異]]

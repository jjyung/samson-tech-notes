---
aliases:
  - 履歷與 CV 的 LLM Agent 工作流公開資源研究
---
# 履歷與 CV 的 LLM Agent 工作流公開資源研究

## 問題意識

這份整理的核心問題是：公開網路上是否已經存在可重用的履歷／CV LLM Agent 工作流、提示詞模板、skill package，甚至接近 AGENTS.md 的操作規格。

## 結論摘要

- 有，而且數量不少；但它們目前還沒有收斂成一個單一、廣泛接受的「履歷版 LLM wiki」標準。
- 現有資源比較常見的形態是：`SKILL.md`、workflow YAML、prompt package、repo-specific docs/agent、以及少量 AGENTS.md。
- 真正穩健的工作流不是「一次生成整份履歷」，而是「先結構化、再比對、再改寫、再 QA、最後人工核對」。

## 最值得重用的資源類型

### 1. 可執行的履歷客製化工具

代表：Resume Matcher

特徵：
- 上傳 master resume，再貼 JD 產生客製內容
- 有 JD Match / 比對頁
- 適合當成二次開發骨架

### 2. 封裝成 skill/package 的代理

代表：Wscats/resume-assistant、resume-assistant-skill

特徵：
- 把 score / polish / customize / export 這些任務明確拆開
- 通常會搭配多代理分工
- 很適合當作可重用 workflow 範本

### 3. prompt + workflow 套件

代表：resumePolice

特徵：
- 有明確的「批判 → 解析 → 建議」流程
- 常見於 Dify / n8n / 低程式碼編排
- 適合做為互動式批改或顧問式工具

### 4. Resume as Code 類型

代表：Resume as Code

特徵：
- 把履歷當成可版本化的資料與產物
- 常見流程是 timeline → JD 分析 → YAML → export
- 很適合做成長期維護的個人履歷系統

### 5. 先正規化資料的 ingest / parser 層

代表：linkedin-resume-parser

特徵：
- 把 PDF / LinkedIn 來源轉成 JSON Resume、Europass XML、LaTeX/PDF 等結構化輸出
- 很適合放在工作流最前面
- 能先把資料抽乾淨，再做後續匹配與改寫

## 最穩健的工作流

本次研究整理出的最佳實踐，可以濃縮成九個步驟：

1. 匿名化與輸入清理
   - 若要送雲端模型，先移除不必要個資
   - 若重視隱私，優先考慮 local-first / self-hosted 路線

2. 抽取成固定 schema
   - basics
   - experience
   - projects
   - education
   - skills
   - certificates
   - evidence spans

3. 建立經歷證據庫
   - 把每段經驗變成可重用的 timeline / evidence entry
   - 後續不同職缺都可以重組

4. 分析 JD
   - 抽 must-have / nice-to-have
   - 抽 seniority、domain、hard skills、soft skills、keyword

5. 做 gap analysis
   - 哪些需求有證據
   - 哪些只能轉譯成 transferable skill
   - 哪些根本沒有，不要硬湊

6. 先寫 summary 和 skills，再寫 bullets
   - 先決定 target role 敘事
   - 再把經歷內容壓縮成高相關 bullet

7. 句子層級重寫 bullets
   - action verb + contribution + result
   - 沒有真實數字就保留 placeholder，不要捏造

8. 做 ATS / QA
   - 標題是否標準
   - 是否使用表格或花式排版
   - 關鍵字覆蓋是否足夠
   - 日期與時態是否一致

9. 人工核對與匯出
   - 所有 JD-tailored 內容都要回到原始證據核對
   - 再交給 builder / template 工具輸出 PDF / Word / HTML

## 這個領域的共識

最一致的共識不是「要用哪個 prompt」，而是以下五件事要同時到位：

- 證據庫
- JD mapping
- 量化追問
- QA gate
- 授權清楚

這也是為什麼單一 mega-prompt 往往不如多步驟 workflow 穩。

## 授權與重用注意

- MIT / Apache-2.0 通常最適合二次開發
- Apache-2.0 額外有專利授權
- AGPL-3.0 若拿去做公開服務要特別小心
- 沒有 license 的 repo 不要默認可自由重用
- X / LinkedIn / 文章型內容通常適合吸收方法，不適合整包複製

## 直接可優先閱讀的來源

### 工具 / workflow

- Resume Matcher
- Resume as Code
- Wscats/resume-assistant
- resume-assistant-skill
- resumePolice
- linkedin-resume-parser

### 實務文章

- Cake
- 104 人力銀行
- Jobscan
- Teal
- 大學職涯中心資源

## 跟這個 wiki 的關聯

這份研究很適合跟以下頁面一起看：

- [[履歷與 CV 的 LLM Agent 工作流]]
- [[Ingest 工作流]]
- [[Query 即知識生產]]
- [[工程化讓 AI 輸出更穩定]]

這份 query note 是原始研究整理；`[[履歷與 CV 的 LLM Agent 工作流]]` 則是把它上升成長期可維護的 topic synthesis。


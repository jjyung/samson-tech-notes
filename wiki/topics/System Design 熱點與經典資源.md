# System Design 熱點與經典資源

## 概覽

系統設計內容可以分成兩類一起看：

1. **近期熱門文章**：反映社群現在在討論什麼 trade-off
2. **經典資源**：提供長期穩定的底層概念與設計語言

最實用的方法不是只看熱門，也不是只看教科書，而是把兩者合併：

- 用經典資源建立基礎框架
- 用熱門文章觀察這個框架在當代架構上的應用方式

## 最近熱門的 system design 議題

### 1. 什麼才算 good system design

`Good system design` 這類文章之所以熱門，是因為它觸及 system design 最常見的誤區：大家常把 system design 簡化成圖，而忽略了可維護性、失敗模式、協作成本與演進路徑。

### 2. database / storage / data architecture 的演進

像 `Databases in 2025: A Year in Review`、Discord 的 messages storage 案例，都在提醒一件事：

- system design 很多時候其實就是 data design
- 真正的難題不只是 schema，而是 scale、migration、consistency、operability

### 3. 架構簡化比架構炫技更重要

`Leaving serverless led to performance improvement and a simplified architecture` 這類文章很有代表性：

- 不是所有流行架構都適合每個團隊
- 真的成熟的 system design 往往會往「簡化」方向收斂
- 成本、性能、可觀測性、故障排查都會影響架構選擇

### 4. distributed systems 的舊教訓仍然會被重提

MCP 那篇關於 distributed systems / RPC lessons 的文章，雖然主題不是純 system design 教材，但它的價值在於提醒：

- 協定設計不是新問題
- 錯誤處理、邊界、重試、兼容性這些老問題仍然存在
- 新工具如果忽略舊教訓，常常會在生產環境吃虧

## 經典資源

### Designing Data-Intensive Applications

這本/這頁是系統設計的長期基礎資源。它適合拿來理解：

- replication
- partitioning
- transactions
- stream processing
- batch processing
- data models

### The System Design Primer

適合作為：

- interview study 的骨架
- system design checklist
- 對照自己的盲點

### Google SRE / Building Secure and Reliable Systems

這類資源補的是 reliability / operations / resilience：

- 監控
- 失敗處理
- service ownership
- incident response
- production readiness

這部分常常是很多系統設計題目真正缺的層次。

### Discord messages storage 案例

這類大型產品的真實架構文章很值得長期保留，因為它能幫你把抽象概念變成具體工程決策：

- 怎麼分層
- 怎麼做 migration
- 怎麼處理 data growth
- 怎麼讓系統持續演進

## 可以重複使用的分析框架

之後看 system design 文章時，可以固定用這幾個問題切：

1. **資料層**
   - 資料如何存放與查詢？
   - partition / replication / indexing 怎麼做？

2. **演進層**
   - 系統如何從小規模長到大規模？
   - 有沒有明顯的 migration / simplification path？

3. **可靠性層**
   - 失敗怎麼處理？
   - 有沒有 retries、idempotency、fallback、backpressure？

4. **邊界層**
   - 服務切分是否合理？
   - API / protocol / ownership 的邊界是否清楚？

5. **成本層**
   - 這個設計的運維成本高不高？
   - 複雜度是被壓下來，還是被轉移到別處？

## 關聯頁面

- [近期 System Design 熱門與經典資源研究](../queries/近期 System Design 熱門與經典資源研究.md)
- [Agent 生態近期熱點](agent-ecosystem-hot-topics.md)
- [AI Coding Agent 設計維度](agent-coding-agent-design-dimensions.md)
- [Ingest 工作流](ingest-workflow.md)
# 近期 System Design 熱門與經典資源研究

## 問題意識

我想找的是：有哪些 *system design* 相關文章或資源，既有近期討論度高的熱門文章，也有長期被反覆引用的經典內容，可以一起放進筆記。

這次的整理方式是：

- 先挑近期在 HN 上討論度高、可當作現代 system design 觀察窗口的文章
- 再補上幾個長期經典資源，作為基本功參照
- 最後把它們收斂成一個可長期更新的 topic page

## 近期熱門文章

### 1. Good system design

- URL: https://www.seangoedecke.com/good-system-design/
- HN: 957 points / 390 comments
- 日期: 2025-08-16
- 觀察：這篇很適合當近期 system design 討論的入口。它的高討論度顯示，大家仍然很在意「什麼才算是好系統設計」，而不只是架構圖本身。

### 2. Databases in 2025: A Year in Review

- URL: https://www.cs.cmu.edu/~pavlo/blog/2026/01/2025-databases-retrospective.html
- HN: 717 points / 192 comments
- 日期: 2026-01-05
- 觀察：這類年度回顧文章很好用，因為它不只談單一技巧，而是把 database / storage / scaling 的變化整理成一個時間視角。

### 3. Leaving serverless led to performance improvement and a simplified architecture

- URL: https://www.unkey.com/blog/serverless-exit
- HN: 480 points / 260 comments
- 日期: 2025-10-15
- 觀察：這篇屬於很典型的架構 trade-off 文章。它不是在吹某個 buzzword，而是在講 performance、complexity、operational simplicity 之間的取捨。

### 4. MCP overlooks hard-won lessons from distributed systems

- URL: https://julsimon.medium.com/why-mcps-disregard-for-40-years-of-rpc-best-practices-will-burn-enterprises-8ef85ce5bc9b
- HN: 409 points / 227 comments
- 日期: 2025-08-09
- 觀察：雖然主題偏 MCP，但本質上是在討論 distributed systems 的經典教訓是否被忽略。很適合拿來補 system design 的「協定、RPC、邊界與失敗模式」視角。

### 5. How Discord Stores Trillions of Messages

- URL: https://discord.com/blog/how-discord-stores-trillions-of-messages
- HN: 435 points / 234 comments
- 日期: 2024-09-28
- 觀察：這是很標準的 large-scale storage / data architecture 案例。它比純理論文章更容易幫助建立 system design 的具體感。

## 經典必讀資源

### 1. Designing Data-Intensive Applications

- URL: https://dataintensive.net/
- HN: 598 points / 59 comments
- 特性：系統設計領域最常被引用的經典之一，重點不是某個產品架構，而是把 replication、partitioning、transactions、streaming、batch 等核心概念建立起來。

### 2. The System Design Primer

- URL: https://github.com/donnemartin/system-design-primer
- HN: 508 points / 57 comments
- 特性：很適合當 system design interview / study 的骨架參考，覆蓋面廣，適合補盲點。

### 3. Google SRE / Building Secure and Reliable Systems

- URL: https://landing.google.com/sre/books/
- HN: 1429 points / 217 comments
- 特性：偏 reliability / operations / resilience，但對 system design 非常重要。它補的是「設計要能長期運作」而不只是「能跑」這件事。

### 4. Discord 的歷史案例

- 2017 版：
  - URL: https://blog.discord.com/how-discord-stores-billions-of-messages-7fa6ec7ee4c7
  - HN: 696 points / 368 comments
- 2023/2024 更新版：
  - URL: https://discord.com/blog/how-discord-stores-trillions-of-messages
  - HN: 435 points / 234 comments
- 特性：同一家公司不同時期的架構演進很有參考價值，可以拿來看 scale up / migration / storage evolution。

## 這些文章共同在講什麼

把這些文章放在一起看，會發現它們其實都在回答同一組問題：

1. **資料怎麼存**
   - storage model
   - partitioning / sharding
   - replication

2. **系統怎麼擴**
   - horizontal scaling
   - service boundaries
   - migration 與 simplification

3. **故障怎麼處理**
   - reliability
   - retries / idempotency
   - fallback 與 graceful degradation

4. **複雜度怎麼控制**
   - 不是只看吞吐量
   - 還要看運維、認知負擔、協作成本

5. **知識怎麼累積**
   - 經典資源給基本概念
   - 熱門文章給最新 trade-off 與語境

## 跟這個 wiki 的關係

這份研究可以和下面幾頁一起看：

- [[System Design 熱點與經典資源]]
- [[Ingest 工作流]]
- [[Query 即知識生產]]
- [[Engineering stabilizes AI output]]

如果之後再看到新的 system design 文章，可以直接加進這份 query note，再決定要不要升級成新的 topic page。

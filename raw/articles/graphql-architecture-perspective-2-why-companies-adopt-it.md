# 大型企業其實是怎麼使用 GraphQL 的

在上一篇文章中，我們討論了為什麼很多大型企業架構師對 GraphQL 保留。

其中提到的原因包括：

* API governance
* security boundary
* query complexity
* service ownership

但如果 GraphQL 有這些問題，為什麼 GitHub、Shopify、Airbnb、Netflix 等公司仍然採用 GraphQL？

答案其實很簡單：

> 多數企業並沒有用 GraphQL 取代 REST。

GraphQL 在企業架構中的定位通常是 **資料聚合層（data composition layer）**。

---

## GraphQL 最成功的場景：Frontend Data Aggregation

現代前端頁面通常需要來自多個服務的資料。

例如一個使用者頁面可能需要：

* user profile
* order history
* recommendation
* notification

如果使用 REST，前端通常需要呼叫多個 API：

```text
GET /user
GET /orders
GET /recommendations
GET /notifications
```

這會帶來幾個問題：

* request 次數增加
* latency 疊加
* 前端邏輯複雜

GraphQL 可以將這些資料整合成一次 query：

```graphql
query {
  user {
    name
    orders { id price }
    recommendations { title }
  }
}
```

這種模式通常稱為：

**Frontend-driven data fetching**

---

## GraphQL 作為 BFF（Backend For Frontend）

在許多企業中，GraphQL 的角色其實是 **BFF layer**。

典型架構如下：

```text
Frontend / Mobile
        │
        ▼
      GraphQL
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
User   Order  Payment
Service Service Service
```

GraphQL server 負責：

* 聚合資料
* 組合 response
* 隱藏 backend 複雜度

這樣 frontend 只需要面對一個 API schema。

---

## GraphQL Federation

在更大的組織中，單一 GraphQL schema 可能會變得難以維護。

因此一些企業採用 **GraphQL Federation** 模式。

概念如下：

```text
Supergraph
   │
 ├ User Graph
 ├ Order Graph
 └ Payment Graph
```

每個團隊負責自己的 schema。

Gateway 會將這些 schema 組合成一個 unified graph。

這讓 GraphQL 可以在大型組織中運作，而不會變成 monolith。

---

## GraphQL 的真正定位

很多關於 GraphQL 的爭議，其實來自一個誤解：

> GraphQL 被當作 REST replacement。

但在多數成功案例中，GraphQL 的角色其實是：

```text
GraphQL = Data Composition Layer
```

而不是：

```text
GraphQL = Service API
```

當 GraphQL 用於 **資料組合**，它可以顯著簡化 frontend。

但如果用於 **服務 API**，則可能引入治理與運維問題。

---

## 小結

GraphQL 並沒有取代 REST。

在多數大型企業中，它更像是一層 **資料查詢與組合的抽象層**。

理解這個定位，就比較容易解釋兩個看似矛盾的現象：

* 為什麼很多架構師對 GraphQL 保留
* 為什麼許多大型公司仍然採用 GraphQL

因為兩者其實在談的是 **不同層級的問題**。

---

下一篇，我想討論一個更有趣的問題：

> AI Agent 可能會讓 GraphQL 再次流行。

因為 GraphQL 的設計，其實非常適合 **machine client**。

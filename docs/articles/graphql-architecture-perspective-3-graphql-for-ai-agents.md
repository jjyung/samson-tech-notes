# AI Agent 可能會讓 GraphQL 再次流行

在前兩篇文章中，我們討論了兩件事情：

* 為什麼很多大型企業架構師對 GraphQL 保留
* GraphQL 在企業架構中的實際定位

結論其實很簡單：

> GraphQL 最適合的角色不是 Service API，而是 Data Composition Layer。

但最近在研究 AI Agent 架構時，我開始覺得一件有趣的事情：

**GraphQL 可能正好非常適合 AI Agent。**

甚至有可能在 AI 時代重新流行。

原因其實和 GraphQL 的原始設計理念有關。

---

## GraphQL 其實是「給機器使用的 API」

大多數 API 其實是為人類設計的。

例如 REST API。

開發者通常需要閱讀：

* API 文件
* endpoint 說明
* request / response 格式

例如：

```text
GET /users
GET /users/{id}/orders
```

開發者需要理解：

* endpoint 命名
* API workflow
* response schema

這些資訊主要是為 **人類理解**而存在。

但 AI Agent 的情境其實不同。

AI Agent 不會閱讀 API 文件，它更擅長理解的是 **結構化資料**。

例如：

* schema
* graph
* type system

而 GraphQL 的 API 其實正是以 schema 為中心。

---

## GraphQL Schema 是 Machine-Readable API

GraphQL API 的核心是 schema。

例如：

```graphql
type User {
  id: ID
  name: String
  orders: [Order]
}

type Order {
  id: ID
  price: Int
}
```

這個 schema 同時描述了：

* 資料結構
* 資料關係
* 可查詢欄位

對 AI agent 來說，這其實就是一個 **machine-readable data graph**。

Agent 不需要閱讀文件，只需要理解 schema，就可以推理出可查詢的資料。

---

## AI Agent 可以動態組合 Query

GraphQL 的設計理念是：

> client 可以自由組合需要的資料。

但在人類開發中，query 通常是手寫的。

例如 frontend developer 會寫：

```graphql
query {
  user(id: 123) {
    name
    orders {
      price
    }
  }
}
```

但 AI agent 的工作方式不同。

Agent 可以：

1️⃣ 讀取 schema
2️⃣ 推理需要的資料
3️⃣ 自動生成 query

例如任務是：

> 找出某個使用者最近訂單的總金額。

Agent 可以生成：

```graphql
query {
  user(id:123) {
    orders(last:30days) {
      price
    }
  }
}
```

這其實就是一種 **semantic query generation**。

---

## GraphQL 很像一種 Knowledge Graph Query

GraphQL schema 本質上是一個 **typed graph**。

例如：

```text
User → Orders → Items → Product
```

這種結構與知識圖（knowledge graph）非常接近。

而 AI agent 很擅長進行 **graph traversal**。

例如：

```text
user → orders → product → supplier
```

GraphQL 的查詢模型其實非常適合這種 traversal。

---

## GraphQL Resolver 與 Agent Tool 很像

另一個有趣的相似點是：

GraphQL resolver 的角色，其實與 AI agent 的 tool orchestration 非常接近。

GraphQL：

```text
query
  │
resolver
  ├ user service
  ├ order service
  └ payment service
```

AI Agent：

```text
task
  │
planner
  ├ tool A
  ├ tool B
  └ tool C
```

兩者其實都在做一件事情：

> 將多個資料來源組合成一個結果。

因此 GraphQL 可以被視為一種 **資料查詢 orchestration layer**。

---

## AI Agent 可能是 GraphQL 最理想的 Client

GraphQL 最初是為 frontend 設計的。

但 frontend 其實並沒有完全發揮 GraphQL 的能力。

很多 query 仍然是手動寫死的。

AI agent 則不同。

Agent 可以：

* 自動生成 query
* 根據任務動態組合資料
* 在不同服務之間進行資料推理

換句話說：

> GraphQL 的 client-driven query 模型，正好符合 AI agent 的工作方式。

---

## GraphQL 可能在 AI 架構中扮演的新角色

如果把 client 從 frontend 換成 AI agent，系統架構可能變成：

```text
User
 │
 ▼
AI Agent
 │
 ▼
GraphQL Data Layer
 │
 ├ User Service
 ├ Order Service
 └ Payment Service
```

GraphQL 變成：

```text
AI Data Query Layer
```

而不是：

```text
Frontend API
```

---

## 小結

GraphQL 在企業架構中常被質疑，但這並不代表它沒有價值。

在多數成功案例中，GraphQL 的角色其實是：

```text
Data Composition Layer
```

而 AI Agent 的出現，可能讓 GraphQL 的另一個特性變得更重要：

> schema-driven query。

如果未來越來越多 client 是 **machine client**，GraphQL 的設計可能會再次顯得非常合理。

也許 GraphQL 的最佳 client，從一開始就不是 frontend，而是 **機器本身**。

# 為什麼很多大型企業架構師對 GraphQL 保留

GraphQL 在開發者社群中一直很受歡迎。
許多文章會提到 Facebook、GitHub、Shopify、Airbnb 等公司都採用了 GraphQL，看起來像是 API 的未來。

但在不少大型企業的架構評審（Architecture Review）中，GraphQL 卻常常被質疑，甚至被否決。

這並不是因為 GraphQL 技術不好，而是因為 **大型企業面對的問題與產品團隊不同**。

在企業架構的視角下，GraphQL 其實會帶來幾個新的挑戰。

---

## 1 API 治理（Governance）變得更困難

在企業環境中，API 不只是程式介面，它還是一種 **需要被治理的資產**。

常見的治理需求包括：

* API versioning
* API catalog
* API lifecycle management
* API audit / compliance

REST API 在這方面其實非常清楚：

```text
GET /v1/users
GET /v2/users
```

API endpoint 本身就是治理單位。

但 GraphQL 的設計是：

```text
POST /graphql
```

所有查詢都透過同一個 endpoint。

這帶來一個問題：

> API gateway 很難從 endpoint 層級理解實際的 API 行為。

換句話說，GraphQL 的 API 不再是 endpoint，而是 **query**。
而 query 是在 request payload 裡。

這讓很多既有的 API 管理工具變得比較難使用。

---

## 2 安全邊界變得模糊

在 REST 架構中，很多安全控制可以在 API Gateway 層完成，例如：

* rate limiting
* RBAC
* API key 管理
* WAF 防護

例如：

```text
GET /admin/users
```

Gateway 可以直接限制只有 admin 角色可以呼叫。

但在 GraphQL 中：

```text
POST /graphql

query {
  users {
    salary
  }
}
```

API Gateway 很難理解 query 的語意。

結果很多權限檢查需要放到 **resolver 層**。

這會讓安全控制：

* 分散在程式邏輯中
* 難以集中管理
* 審計（audit）變得困難

對資安團隊來說，這意味著 **安全邊界往應用層移動**。

---

## 3 查詢成本不可預測

另一個企業架構師常提到的問題是 **operational risk**。

REST API 的行為通常比較容易預測：

```text
GET /orders
```

後端大致知道這個 API 會做什麼查詢。

但 GraphQL 的 query 可以非常複雜，例如：

```graphql
query {
  users {
    orders {
      items {
        product {
          supplier {
            address
          }
        }
      }
    }
  }
}
```

這種 nested query 可能造成：

* N+1 query
* 高 DB 負載
* latency spikes

因此 GraphQL 通常需要額外機制，例如：

* query depth limit
* query complexity limit
* query cost analysis

這些機制本身並不困難，但會增加 **系統運維的複雜度**。

---

## 4 系統責任邊界變得模糊

在微服務架構中，系統通常會依據 domain 分工，例如：

```text
User Service
Order Service
Payment Service
```

每個團隊負責自己的服務與 SLA。

但 GraphQL 的 query 很容易跨越多個 domain：

```graphql
query {
  user {
    orders {
      payments
    }
  }
}
```

這會帶來一個常見問題：

> 如果這個 query 變慢，誰負責？

是：

* GraphQL team
* Order service team
* Payment service team

還是三者都有？

這種 **ownership boundary** 在大型組織中特別重要。

---

## 5 可觀察性（Observability）變得更困難

企業系統通常會監控：

* API latency
* error rate
* traffic pattern

在 REST 中，metrics 通常是：

```text
GET /users
GET /orders
```

但 GraphQL 的 endpoint 通常只有：

```text
POST /graphql
```

如果沒有額外工具，很難知道：

* 哪些 query 最常被呼叫
* 哪些 query 最慢
* 哪些 query 最耗資源

因此 GraphQL 系統通常需要額外的 tracing 或 query analytics 工具。

---

## GraphQL 的問題，其實不是技術問題

值得注意的是，上面這些問題 **並不代表 GraphQL 不好**。

事實上，GraphQL 解決了一個很真實的問題：

> 前端需要組合來自多個服務的資料。

GraphQL 在這個場景下非常強大。

因此很多大型企業採取的做法是：

```text
Frontend / Mobile
        │
        ▼
   GraphQL (BFF / Data Layer)
        │
        ▼
   REST / gRPC services
```

GraphQL 被用作 **資料聚合層（data composition layer）**，而不是取代所有 API。

---

## 小結

GraphQL 在開發者社群中很受歡迎，但企業架構師的保留並不是沒有原因。

GraphQL 帶來的挑戰主要在於：

* API governance
* security boundary
* operational predictability
* service ownership
* observability

這些都是 **大型企業系統特別重視的問題**。

換句話說：

> GraphQL 解決的是「資料組合」問題，而不是「服務 API」問題。

理解這一點，就比較容易找到 GraphQL 在企業架構中的合理位置。

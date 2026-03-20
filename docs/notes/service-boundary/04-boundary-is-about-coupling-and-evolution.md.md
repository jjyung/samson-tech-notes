# Boundary Is About Coupling and Evolution

## Problem

在前兩篇，我們已經建立了兩個關鍵原則：

- Boundary 應該從語意開始
- Boundary 的可行性取決於一致性需求

但這還缺一個很實務的問題：

> 即使可以拆，應不應該拆？

很多系統在這一步出現問題：

- 語意分得很清楚
- 一致性也設計過

但拆完之後，系統反而變得：

- 更難改
- 更難部署
- 更難理解

這代表：

> boundary 的決策，只考慮了「可行性」，但沒有考慮「價值」。

---

## 常見誤解：拆分本身就是目標

在許多架構討論中，「拆 service」常被當成一種進步：

- 更 modular
- 更 scalable
- 更符合 microservices

但這裡有一個隱含前提：

> 拆分會降低耦合，並提升系統的演化能力。

問題是，這個前提不一定成立。

---

## Coupling：邊界真正要解的問題

如果回到最根本的問題：

> 為什麼我們需要 service boundary？

答案其實很單純：

> 為了降低不必要的耦合。

但「耦合」不是單一維度，而是多種形式的組合：

---

### 1. 語意耦合（Semantic Coupling）

- 共享相同模型與語意
- 修改一個概念，影響多個地方

---

### 2. 時序耦合（Temporal Coupling）

- 必須同時執行
- 必須同步呼叫
- 無法容忍延遲

---

### 3. 資料耦合（Data Coupling）

- 共享資料結構
- 直接依賴彼此資料

---

### 4. 部署耦合（Deployment Coupling）

- 必須一起發版
- 無法獨立部署

---

### 5. 組織耦合（Team Coupling）

- 多個團隊必須協調才能完成變更
- ownership 不清

---

一個好的 boundary，應該要：

> 降低這些耦合，而不是只是把它們分散到不同地方。

---

## 拆分的代價：耦合不會消失，只會轉移

這是很多系統會踩的坑：

> 拆分 service 並不會消除耦合，只會改變耦合的形式。

例如：

- 從 in-process call → network call
- 從 function dependency → API dependency
- 從 shared memory → data synchronization

如果這些耦合本質上沒有被降低，那結果就是：

> 系統變得更複雜，但沒有更解耦。

---

## Evolvability：boundary 的真正價值

如果 coupling 是問題，那 evolvability 就是目標。

所謂的 evolvability，可以用一個很實際的方式理解：

> 系統是否能在不影響其他部分的情況下持續改變？

這包含：

- 獨立修改
- 獨立部署
- 獨立擴展
- 獨立理解

---

## Boundary 的第三原則：演化邊界

延續前兩篇：

- 第一原則：語意邊界
- 第二原則：一致性邊界

這一篇補上第三個：

> Service boundary 的最終目標，是建立可演化的邊界。

也就是說：

- boundary 不是為了拆而拆
- 而是為了讓變更成本可控

---

## 一個關鍵判斷：變更是否被隔離？

在實務上，可以用一個簡單但非常有效的問題來判斷：

> 如果這裡的需求改變，是否會影響其他 boundary？

如果答案是：

- 經常會 → boundary 可能不合理
- 很少會 → boundary 是有效的

---

## 常見反模式

以下幾種情況，通常代表 boundary 雖然存在，但沒有發揮作用：

---

### ❌ 邏輯拆開，但變更仍然同步

- 每次改 A，都要改 B
- release 必須一起做

👉 deployment coupling 仍然存在

---

### ❌ 使用事件，但仍高度依賴彼此

- event schema 緊密耦合
- consumer 必須理解 producer 的內部邏輯

👉 semantic coupling 被隱藏，但沒有消失

---

### ❌ 資料被複製，但責任不清

- 多份資料來源
- 無法確定哪一份是 source of truth

👉 data ownership 失敗

---

### ❌ boundary 過細

- 每個小功能一個 service
- interaction cost 過高

👉 complexity 超過收益

---

## 整合前三篇：一個完整的決策模型

把整個系列整理起來，可以得到一個簡單但實用的模型：

---

### Step 1：語意（Semantic Boundary）

> 這裡是不是同一件事？

如果不是 → 應該分開

---

### Step 2：一致性（Consistency Boundary）

> 這些規則是否必須同時成立？

如果是 → 應該放在同一個邊界

---

### Step 3：耦合與演化（Coupling & Evolvability）

> 拆開之後，是否真的降低耦合並提升演化能力？

如果沒有 → 不應該拆

---

這三步驟一起，才構成合理的 service boundary 判斷。

---

## Insight

如果用一句話總結整個系列：

> Service boundary 的本質，不是拆分系統，而是管理耦合與變更成本。

---

## What This Means for Practice

當你用這個模型來看系統時：

- 不會再盲目追求 microservices
- 不會因為技術而決定邊界
- 可以清楚說明每一個 boundary 的理由

更重要的是：

> 你可以解釋「為什麼不拆」，而不是只會說「怎麼拆」。

---

## Closing

當 boundary 的決策回到：

- 語意
- 一致性
- 耦合
- 演化

系統設計就不再只是結構問題，而是：

> 一種關於成本、風險與變更的決策過程。

---
aliases:
  - multi-model review
  - 多模型交叉審查
---
# 多模型 Review

## 概覽

多模型 Review 指的是：把不同模型放在不同位置，讓它們各自發揮擅長的地方，例如一個負責實作，另一個負責審查與挑錯。

## 為什麼有用

- 不同模型的盲點不同
- Review 角色和實作角色可以分離
- 這比單一模型一路到底更容易抓到邏輯錯誤、邊界問題與一致性問題

## 常見搭配方式

- 一個模型負責產出
- 另一個模型負責 code review
- 另一個模型負責安全性、邊界或文件審查

## 跟既有筆記的關係

- [dotLLM 與 AI 輔助開發的工程方法](../sources/dotllm-ai-assisted-development.md)
- [AI 輔助開發工作流](ai-assisted-development-workflow.md)
- [AI Coding Agent 設計維度](agent-coding-agent-design-dimensions.md)
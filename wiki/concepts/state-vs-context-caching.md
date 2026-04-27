---
aliases:
  - 放在 State vs Context Caching
  - State 與 Context Caching 的本質差異
  - State vs Context Caching
---
# 放在 State 與使用 Context Caching 的本質區別

## 一句話差異

- `State` 解決的是「應用程式怎麼記住」。
- `Context Caching` 解決的是「模型端怎麼避免重算」。

## 分層理解

### State（應用層快取）

- 由你的程式（前端或後端）保存資訊。
- 下一次呼叫模型時，仍需把資訊重新塞進 `Instruction` 或 `History`。
- 對模型 API 來說這是全新輸入，仍要重新 tokenize 與 prefilling。

結果：

- 會收完整 input token 成本。
- 內容越長，latency 越高。

### Context Caching（模型伺服器層快取）

- 把重複且大型的上下文（長文件、固定背景、few-shot）快取在模型服務端。
- 後續請求以 cache identifier 重用已計算的中間狀態。

結果：

- 降低重複輸入成本（命中部分通常有折扣）。
- 顯著降低 prefilling 時間，回應更快。

## 你的情境判斷

情境是：把資訊放在 app state，並在後續對話插入 instruction。

結論：

- 若內容很短，維持 state 即可。
- 若內容很長且會重複使用，context caching 有明顯效益。

## 何時值得啟用 Context Caching

優先看三件事：

1. 長度是否夠大：常見需要達到服務門檻（你目前提到的 Gemini 門檻是 `32,768 tokens`）。
2. 重複使用是否頻繁：同一段上下文是否會跨多輪重複引用。
3. 存活時間是否合理：在 TTL 內是否有足夠請求次數攤平成本。

## 情境對照

| 情境 | 建議 | 原因 |
| --- | --- | --- |
| 短指令、少量歷史 | 放在 `State` | 未達快取門檻，管理 cache 的額外成本不划算。 |
| 大型知識庫、長參考文件 | 用 `Context Caching` | 避免每輪重送長文本，降成本與延遲。 |
| 固定且複雜的 system prompt（含 few-shot） | 用 `Context Caching` | 高重複、長前綴，快取命中效益高。 |

## Best Practices

1. 前綴優先：把可快取內容放在 prompt 最前面，動態內容放後面。
2. TTL 設計：依互動頻率設定存活時間，避免過短失效或過長浪費。
3. 監控命中率：確認每次請求真的 hit cache。
4. 控制變動：避免在可快取段落摻入每次都變的值（如即時時間）。
5. 成本平衡：同時考慮計算折扣與儲存成本，不是所有資料都要快取。

## 總結

把內容放在 `State`，只是讓系統「記得」；  
使用 `Context Caching`，才是讓模型「不用再算一次」。

當資訊量大、變動低、重複使用高時，context caching 才會成為真正有效的效能與成本優化手段。

## 關聯頁面

- [AI 輔助開發工作流](../topics/ai-assisted-development-workflow.md)
- [工程化讓 AI 輸出更穩定](engineering-stabilizes-ai-output.md)

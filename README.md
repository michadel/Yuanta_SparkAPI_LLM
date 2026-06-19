# 元大證券 SparkAPI (原 OneAPI) IO 規格文件集 | Yuanta Securities SparkAPI (formerly OneAPI) IO Specification Collection

這是一個專門為大型語言模型 (LLM) 設計的知識庫，包含了元大證券 **SparkAPI** (原名 OneAPI) 的完整輸入/輸出 (Input/Output) 規格說明。
Keywords: 元大證券, SparkAPI, OneAPI, 交易 API, IO 規格, LLM Knowledge Base, Trading API Specification, Yuanta Securities, Stock Trading API, Futures API

## 專案目的 | Project Purpose

本專案的主要目的是提供結構化、易於解析的 API 規格文件，讓 LLM 在執行交易任務或輔助開發時，能夠精確理解：
1. **API 功能 (API Functions)**：每個 API 的具體用途。
2. **請求參數 (Request Parameters)**：呼叫 API 時需要提供的欄位名稱、資料型態及限制條件。
3. **回應結構 (Response Structure)**：API 回傳結果的 JSON 格式與欄位含義。

透過將此文件集作為 LLM 的上下文 (Context) 或知識庫，可以顯著提升 AI Agent 在處理交易指令、查詢市場資訊及執行策略時的準確性。

## API 功能分類 | API Categories

本專案的文件涵蓋了以下主要的業務領域：

### 1. 股票交易與資訊 (Stock Trading & Information)
- `GetStockInformation_IO_Spec.md`: 股票基本資料查詢 (Stock Basic Info)。
- `SendStockOrder_IO_Spec.md`: 下單功能 (Stock Order Placement)。
- `GetStkTickDetail_IO_Spec.md`: 即時逐筆成交明細 (Real-time Tick Detail)。
- ...以及其他相關的股票歷史與交易紀錄規格。

### 2. 期貨與選擇權 (Futures & Options)
- `SendFutureOrder_IO_Spec.md`: 期貨下單 (Futures Order Placement)。
- `GetFutStoreSummary_IO_Spec.md`: 期貨部位總結 (Futures Position Summary)。
- ...以及相關的保證金與利息規格。

### 3. 市場行情與訂閱 (Market Data & Subscription)
- `SubscribeStockInformation_IO_Spec.md`: 即時股票資訊訂閱 (Real-time Stock Info Subscription)。
- `GetKLine_IO_Spec.md`: K 線圖資料查詢 (K-Line Chart Query)。
- `GetQuoteList_IO_Spec.md`: 行情列表查詢 (Market Quote List)。

### 4. 帳戶與資產管理 (Account & Asset Management)
- `GetBankBalance_IO_Spec.md`: 銀行帳戶餘額查詢 (Bank Balance Inquiry)。
- `GetUnrealizedGainLossDetail_IO_Spec.md`: 未實現損益明細 (Unrealized Gain/Loss Detail).

### 5. 自動交易策略與演算法 (Algo & Strategy)
- `SendAlgoCOOdrStrategy.md`: 發送演算法策略指令 (Algorithm Strategy Command)。
- `DeleteAlgoCOOdrStrategy.md`: 刪除演算法策略 (Delete Algorithm Strategy).

## 如何使用此文件集 (For LLMs)

**重要提示：請務始先閱讀 `元大SparkAPI_IO規格_LLM.md` 作為主要的進入點與總覽指南。**

當你作為一個交易助手或開發工具時，請參考目錄下的 `*_IO_Spec.md` 文件來獲取 API 的詳細定義。

**範例指令邏輯 (Example Instruction Logic)：**
1. **識別意圖 (Identify Intent)**：判斷使用者想要執行的操作（例如：「查詢我的股票部位」）。
2. **匹配 API (Match API)**：從文件集中找到對應的 API 規格（例如：`GetStoreSummary_IO_Spec.md`）。
3. **構建請求 (Construct Request)**：根據該文件的 `Input` 規範，提取必要的參數並組成 JSON 物件。
4. **解析回應 (Parse Response)**：當收到 API 回傳結果時，參考該文件的 `Output` 規格來解釋數據內容。

## 注意事項
- 本文件僅提供 **IO 規格說明**，不包含實際的 API Endpoint URL 或身份驗證 (Authentication) 機制。
- 所有操作應遵循元大證券之相關交易規範與風險控管原則。

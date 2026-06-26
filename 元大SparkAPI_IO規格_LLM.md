# 元大 Spark API IO 規格 LLM 整理版

> 來源：`doc/IO_Doc/FunctionList.xlsx` 與同資料夾內已轉成 Markdown 的 `*_IO_Spec.md`。
> 本檔供 LLM 快速理解、檢索與生成程式時參考；股名檔對照表筆數過大，依使用者指示未納入。

- 產生日期：2026-06-19
- 使用方式：先看「功能總覽」決定 Function ID 與分類，再到「API 詳細規格」查看輸入、輸出物件與欄位。
- OnResponse 分派：`intMark=0` 是系統訊息；`intMark=1` 是查詢回應；`intMark=2` 是訂閱回應；`dwIndex` 通常對應 Function ID。
- 語系常見參數：`enumLangType` 預設 `Normal`/Big5，另有 `UTF8` 與 `SC`。
- 帳號格式：證券常見 `S+分公司代號(4)+帳號(7)`；期貨常見 `F + 固定 F021013 + 分公司BRANCH + 帳號ACCOUNT`，實際字串開頭會是 `FF021013...`。

## LLM 實作指南

### 目標讀法

- 本檔的前段說明「怎麼接 API」；後段每個 API 小節說明「欄位長什麼樣」。
- 實作時先依功能總覽找到 Function 與 Function ID，再依該 Function 小節建立輸入物件、送出方法，最後在 `OnResponse` 依 `intMark + strIndex` 轉型 `objValue`。
- 這是公開版文件；帳號、密碼、憑證路徑都以占位字串表示，請在程式中從安全來源讀取，不要硬編在原始碼或 log。

### C# 最小生命週期

```csharp
using System.Text;
using YuantaOneAPI;

Encoding.RegisterProvider(CodePagesEncodingProvider.Instance); // Big5/CP950 相關輸出需要

var api = new YuantaSparkAPITrader();
api.OnResponse += OnResponse;
api.SetLogType(enumLogType.COMMON);

api.Open(enumEnvironmentMode.UAT);   // 測試環境；正式環境用 PROD
// 等待 intMark=0 且訊息含「交易主機」與「Is Connected」後再登入

api.Login(account, password);
// Windows: Login(Account, Pass)
// Linux/macOS: Login(PfxPath, PfxPass, Account, Pass)

// 關閉時：LogOut(); Close(); Dispose();
```

- `YuantaSparkAPITrader` 與所有主要物件/列舉都在 `YuantaOneAPI` namespace。
- 官方 C# 範例會先訂 `OnResponse`、設定 `SetLogType(enumLogType.COMMON)`，再 `Open()`。
- `Open()`、查詢、訂閱、下單的同步回傳值只代表送出呼叫是否成立；真正資料都從 `OnResponse` 回來。
- 不要在 `OnResponse` 裡做耗時工作；實務上建議把強型別物件轉成內部事件或丟進 queue/channel。

### OnResponse 分派模板

```csharp
static void OnResponse(int intMark, uint dwIndex, string strIndex, object objHandle, object objValue)
{
    switch (intMark)
    {
        case 0:
            var systemMessage = Convert.ToString(objValue);
            break;
        case 1:
            switch (strIndex)
            {
                case "Login": HandleLogin((LoginResult)objValue); break;
                case "GetWatchListAll": HandleWatchList((QueryWatchListResult)objValue); break;
                case "GetStkTickDetail": HandleTickDetail((StickDetailResult)objValue); break;
                case "GetKLine": HandleKLine((KLineResult)objValue); break;
                case "SendFutureOrder": HandleFutureOrder((FutOrderResult)objValue); break;
                default: HandleUnknown(strIndex, objValue); break;
            }
            break;
        case 2:
            switch (strIndex)
            {
                case "SubscribeWatchlistAll": HandleWatch((WatchListAllResult)objValue); break;
                case "SubscribeStockTick": HandleStockTick((StockTickResult)objValue); break;
                case "SubscribeFiveTickA": HandleFiveTick((FiveTickAResult)objValue); break;
                case "RR_RealReport": HandleRealReport((RealReport)objValue); break;
                default: HandleUnknown(strIndex, objValue); break;
            }
            break;
    }
}
```

- `intMark=0` 通常是系統字串訊息；連線/斷線也在這裡。
- `intMark=1` 是查詢、登入、下單回應；`strIndex` 是 Function 名稱。
- `intMark=2` 是訂閱推播與即時回報；`strIndex` 一樣是 Function 名稱。
- 若 `strIndex` 空字串，通常代表查詢/訂閱失敗或 SDK 回傳一般錯誤文字，請把 `objValue` 當 string 記錄。

### 建立輸入物件的通用模式

```csharp
var quotes = new List<Quote>
{
    new Quote { MarketType = enumMarketType.TWSE, StockCode = "2330" },
    new Quote { MarketType = enumMarketType.TAIFEX, StockCode = "TMFF6" },
};
api.GetWatchListAll(loginAccount, quotes);

var subs = new List<WatchlistAll>
{
    new WatchlistAll { MarketType = enumMarketType.TAIFEX, StockCode = "TMFF6" },
};
api.SubscribeWatchlistAll(loginAccount, subs);

var ticks = new List<StockTick>
{
    new StockTick { MarketType = enumMarketType.TWSE, StockCode = "2330" },
};
api.SubscribeStockTick(loginAccount, ticks);

var five = new List<FiveTickA>
{
    new FiveTickA { MarketType = enumMarketType.TAIFEX, StockCode = "TMFF6" },
};
api.SubscribeFiveTickA(loginAccount, five);
```

- 查詢類清單常用 `Quote`、`StkInfo`；訂閱類則各自用 `WatchlistAll`、`StockTick`、`FiveTickA`。
- 商品物件通常至少有 `MarketType` 與 `StockCode`。
- `enumMarketType` 常用值：`TWSE=1`、`TWOTC=2`、`TAIFEX=3`、`TWEMERGING=4`、海外市場 202 起。

### Python/pythonnet 最小模式

```python
from pathlib import Path
from pythonnet import load

load("coreclr")

import clr, os, sys
from System.Collections.Generic import List

sdk_dir = Path(__file__).resolve().parent
sys.path.append(str(sdk_dir))
if sys.platform == "win32":
    os.add_dll_directory(str(sdk_dir))

clr.AddReference("YuantaSparkAPI")
from YuantaOneAPI import (
    YuantaSparkAPITrader, OnResponseEventHandler, enumEnvironmentMode, enumLogType,
    enumMarketType, Quote, WatchlistAll
)

def on_response(intMark, dwIndex, strIndex, objHandle, objValue):
    print(intMark, dwIndex, strIndex, objValue)

api = YuantaSparkAPITrader()
api.OnResponse += OnResponseEventHandler(on_response)
api.SetLogType(enumLogType.COMMON)
api.Open(enumEnvironmentMode.UAT)
api.Login(account, password)

items = List[Quote]()
items.Add(Quote(MarketType=enumMarketType.TWSE, StockCode="2330"))
api.GetWatchListAll(account, items)
```

- Python 範例使用 `pythonnet` 載入 .NET runtime，再 `clr.AddReference("YuantaSparkAPI")`。
- Windows 需讓 DLL 目錄進 `os.add_dll_directory()`；Linux/macOS 需確保 native library 位於 runtime 可搜尋路徑。
- Python 主程式要維持行程存活，否則訂閱推播還沒回來程序就結束。

### 帳號、密碼與公開文件安全

- 帳號格式只保留規則，不保留真實或看似真實的帳號字串：證券 `S + 分公司代號(4) + 帳號(7)`；期貨 `F + 固定 F021013 + 分公司BRANCH + 帳號ACCOUNT`，實際字串開頭會是 `FF021013...`。
- Windows 登入用 `Login(Account, Pass)`；Linux/macOS 登入用 `Login(PfxPath, PfxPass, Account, Pass)`。
- 密碼、PFX 密碼、憑證路徑不可寫入程式碼、設定檔、log、console 或公開文件；請用 OS secret store、環境變數、互動輸入或專案既有安全機制。
- `LoginResult.LoginList` 可能含姓名、身分證字號、營業員代碼；公開 log 前必須遮罩。

### 已踩過的實作雷點

- SparkAPI 價格多數是 `double` 直接值，不要沿用舊 OneAPI 的股票除 10000、期貨除 1000 規則。
- 但 `GetStkTickDetail` 對期貨回補價格曾實測比即時行情少 10 倍；若做期貨回補，應用即時價/歷史價自動偵測尺度，不要盲信單一來源。
- 微台連續碼 `TMF0/TMFPM0/TMF8` 的即時行情曾實測為月份契約的 1/10；需用商品規則與參考價防止重複放大。
- `GetStkTickDetail` 沒有交易日期參數，只查伺服器認定的當交易日；不可用它指定補過去某天夜盤。
- `GetStkTickDetail` 實測每秒最多約 3 次；多商品回補請節流。
- `GetKLine` 主要適用台股上市櫃 K 線；期貨 K 線需自行由 tick/報價聚合。
- 非 Windows 登入加簽需要 native library：macOS `libYuantaCGCrypt.dylib`、Linux `libCGCGCrypt.so`。NuGet targets 檔名曾不會自動匯入，若登入回 `dwIndex=9` 或憑證檢核失敗，先檢查 native 檔是否複製到輸出目錄。
- `Login` 呼叫頻率建議間隔 **5 秒以上**；短時間內重複呼叫登入可能造成伺服器端拒絕或帳號凍結風險，請勿在迴圈或重試邏輯中無節流地連續呼叫。
- 等待連線不要比對完整字串；用關鍵字判斷，例如系統訊息同時包含「交易主機」與「Is Connected」。斷線可看 `Is Disconnected`，且先判斷斷線再判斷連線。
- 訂閱與查詢錯誤可能以 `strIndex=""` 回傳一般字串，請保留原始訊息以便診斷。
- 官方 IO 規格內有拼字沿用，例如 `Fileld`、`StickDetailResult`；寫程式要以 SDK 實際型別名稱為準。
- `GetWatchListAll` 是取得報價快照的好入口，可在訂閱後主動補齊昨收、開盤參考價、漲跌停、試撮與五檔摘要；策略洗價仍應使用即時 tick/推播事件。
- 期貨訂閱代碼、下單商品代碼、期交所官方資料商品代碼不一定完全相同；例如報價可能用 `TMFF6`，下單商品欄可能用 `FITX/TMF` 類商品代號，請依各 API 欄位說明轉換。

### 下單安全預設

- 實作交易功能時先接 UAT，先完成查詢/回報解析，再接下單。
- `SendStockOrder`、`SendFutureOrder` 的送出回傳值不等於成交；實際委託結果看 `StkOrderResult/FutOrderResult` 與即時回報。
- 正式下單前必須由使用者明確啟用；公開範例應避免預設呼叫真實下單。

## 功能總覽

### 連線/通用
| Function | 中文名稱 | Function ID | 備註 | 來源規格 |
| --- | --- | --- | --- | --- |
| Open | 開啟API連線 |  |  |  |
| Login | 登入 | 100000 |  | Login_IO_Spec.md |
| LogOut | 登出 |  | 登入的帳號全部登出 |  |
| Close | 關閉API連線 |  |  |  |
| Dispose | 釋放API連線 |  |  |  |
| SetLogType | 設定Log類別 |  |  |  |
| OnResponse | 回應事件 |  | Server資料回應至Client端時所觸發的事件 | OnResponse_IO_Spec.md |

### 行情查詢
| Function | 中文名稱 | Function ID | 備註 | 來源規格 |
| --- | --- | --- | --- | --- |
| GetQuoteList | 取得己訂閱即時報價商品清單 | 100001 |  | GetQuoteList_IO_Spec.md |
| GetWatchListAll | 報價表查詢 | 500016 | 報價類發送 | GetWatchListAll_IO_Spec.md |
| GetStockInformation | 標的資訊查詢 | 20100027 | 報價類發送 | GetStockInformation_IO_Spec.md |
| GetStkTickDetail | 當日分時明細查詢 | 500012 | 報價類發送 | GetStkTickDetail_IO_Spec.md |
| GetStkClassifyPrice | 分價量表查詢 | 500041 | 報價類發送 | GetStkClassifyPrice_IO_Spec.md |
| GetKLine | K線查詢 | 500017 | 報價類發送 | GetKLine_IO_Spec.md |

### 即時訂閱/回報
| Function | 中文名稱 | Function ID | 備註 | 來源規格 |
| --- | --- | --- | --- | --- |
| RR_RealReport | 即時回報訂閱 | 3356101146 | 登入即訂閱 | RR_RealReport_IO_Spec.md |
| RR_RealReportMerge | 彙整的即時回報訂閱 | 3356101147 | 登入即訂閱 | RR_RealReportMerge_IO_Spec.md |
| SubscribeWatchlistAll | 行情報價表訂閱 | 1644840458 | 訂閱 | SubscribeWatchlistAll_IO_Spec.md |
| UnSubscribeWatchlistAll | 行情報價表解訂閱 | 1644840458 | 解訂閱 | SubscribeWatchlistAll_IO_Spec.md |
| SubscribeStockTick | 分時明細訂閱 | 3523880970 | 訂閱 | SubscribeStocktick_IO_Spec.md |
| UnSubscribeStockTick | 分時明細解訂閱 | 3523880970 | 解訂閱 | SubscribeStocktick_IO_Spec.md |
| SubscribeFiveTickA | 最佳五檔行情訂閱 | 3523886090 | 訂閱 | SubscribeFiveTickA_IO_Spec.md |
| UnSubscribeFiveTickA | 最佳五檔行情解訂閱 | 3523886090 | 解訂閱 | SubscribeFiveTickA_IO_Spec.md |
| SubscribeWatchlist | 行情報價表訂閱(指定欄位) | 3523888651 | 訂閱 | SubscribeWatchlist_IO_Spec.md |
| UnSubscribeWatchlist | 行情報價表解訂閱(指定欄位) | 3523888651 | 解訂閱 | SubscribeWatchlist_IO_Spec.md |
| SubscribeMarketInformation | 個股盤前資訊訂閱 | 3523954191 | 訂閱，特殊功能需申請權限 | SubscribeMarketInformation_IO_Spec.md |
| UnSubscribeMarketInformation | 個股盤前資訊解訂閱 | 3523954191 | 解訂閱，特殊功能需申請權限 | SubscribeMarketInformation_IO_Spec.md |
| SubscribeStockInformation | 個股其他資訊訂閱 | 3523954192 | 訂閱，特殊功能需申請權限 | SubscribeStockInformation_IO_Spec.md |
| UnSubscribeStockInformation | 個股其他資訊解訂閱 | 3523954192 | 解訂閱，特殊功能需申請權限 | SubscribeStockInformation_IO_Spec.md |

### 帳務查詢
| Function | 中文名稱 | Function ID | 備註 | 來源規格 |
| --- | --- | --- | --- | --- |
| GetRealReportMerge | 即時回報彙總查詢 | 100016 | 帳務類發送 | GetRealReportMerge_IO_Spec.md |
| GetRealReport | 即時回報查詢 | 100020 | 帳務類發送 | GetRealReport_IO_Spec.md |
| GetOrderTradeReport | 委託成交綜合回報 | 20101018 | 帳務類發送 | GetOrderTradeReport_IO_Spec.md |
| GetStoreSummary | 股票庫存綜合總表 | 20103022 | 帳務類發送 | GetStoreSummary_IO_Spec.md |
| GetFutStoreSummary | 期貨庫存總表查詢 | 201032013 | 帳務類發送 | GetFutStoreSummary_IO_Spec.md |
| GetOVFutStoreSummary | 國際期貨庫存總表查詢 | 201034018 | 帳務類發送 | GetOVFutStoreSummary_IO_Spec.md |
| GetFutInterestStore | 期貨權益數查詢 | 201042020 | 帳務類發送 | GetFutInterestStore_IO_Spec.md |
| GetFutDepositOptimum | 期貨保證金最佳化查詢 | 201042017 | 帳務類發送，特殊功能需申請權限 | GetFutDepositOptimum_IO_Spec.md |
| GetFutSprStore | 期貨複式單庫存明細查詢 | 201032012 | 帳務類發送，特殊功能需申請權限 | GetFutSprStore_IO_Spec.md |
| GetUnrealizedGainLossDetail | 未實現損益明細查詢 | 201031018 | 帳務類發送 | GetUnrealizedGainLossDetail_IO_Spec.md |
| GetHisRealizedGainLoss | 已實現損益查詢 | 201021011 | 帳務類發送 | GetHisRealizedGainLoss_IO_Spec.md |
| GetStkHistoryReportReversal | 沖銷明細查詢 | 201021025 | 帳務類發送 | GetStkHistoryReportReversal_IO_Spec.md |
| GetStkTransactionOutlay | 現貨交割款查詢(台幣) | 201041010 | 帳務類發送 | GetStkTransactionOutlay_IO_Spec.md |
| GetBankBalance | 銀行餘額查詢 | 201041014 | 帳務類發送 | GetBankBalance_IO_Spec.md |

### 交易/條件單
| Function | 中文名稱 | Function ID | 備註 | 來源規格 |
| --- | --- | --- | --- | --- |
| SendStockOrder | 國內證券下單 | 301001031 | 交易類發送 | SendStockOrder_IO_Spec.md |
| SendFutureOrder | 國內期貨下單 | 301002024 | 交易類發送 | SendFutureOrder_IO_Spec.md |
| SendFutureCombined | 期貨複式單組合 | 301002014 | 交易類發送，特殊功能需申請權限 | SendFutureCombined_IO_Spec.md |
| SendFutureApart | 期貨複式單拆解 | 301002013 | 交易類發送，特殊功能需申請權限 | SendFutureApart_IO_Spec.md |
| SendAlgoCOOdrStrategy | 新增條件單 | 100002 | 交易類發送 | SendAlgoCOOdrStrategy.md |
| GetConditionStrategy | 有效策略查詢 | 100003 | 交易類發送 | GetConditionStrategy_IO_Spec.md |
| GetHisConditionStrategy | 歷史策略查詢 | 100004 | 交易類發送 | GetHisConditionStrategy_IO_Spec.md |
| DeleteAlgoCOOdrStrategy | 刪除條件單 | 100005 | 交易類發送 | DeleteAlgoCOOdrStrategy.md |

## OnResponse 分派速查

| 條件 | 意義 | objValue 解析方式 |
| --- | --- | --- |
| intMark=0 | 系統資訊回應 | `strIndex` 通常空字串；多以 string 解析系統訊息。 |
| intMark=1 | 查詢資訊回應 | `dwIndex` 為 Function ID 時，依 `strIndex` 指定 Function 將 `objValue` 轉型成對應 Result 物件。 |
| intMark=2 | 訂閱資訊回應 | `dwIndex` 為 Function ID 時，依訂閱規格解析 `objValue`；`dwIndex=1` 表示訂閱/取消訂閱失敗。 |
| strIndex 空字串 | 查詢或訂閱功能可能有誤 | 用 string 格式解析 `objValue`，並保留原始訊息供診斷。 |

## API 詳細規格

### Open

- 中文名稱：開啟API連線
- Function ID：(FunctionList 未列)
- 備註：(無)
- 狀態：此項只有 FunctionList 條目，`doc/IO_Doc` 內未找到對應 IO spec md。

### Login

- 中文名稱：登入
- Function ID：100000
- 來源：`Login_IO_Spec.md`
- Service ID：API Login
- Service Desc：登入
- 呼叫簽名：`bool Login(Account, Pass)`

#### Windows 環境使用
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 登入帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| Pass | 登入密碼 | string |  |

#### Linux 環境使用
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| PfxPath | Pfx憑證路徑 | string | 絕對路徑 |
| PfxPass | Pfx憑證密碼 | string |  |
| Account | 登入帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| Pass | 登入密碼 | string |  |

#### LoginResult 登入結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginStatus | 登入狀態 | Status |  |
| LoginList | 登入取得資料清單 | List&lt;LoginData&gt; |  |

#### Status 登入狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MsgCode | 訊息代碼 | string | 0000:執行失敗<br>0001:執行成功<br>0102: 密碼凍結或未啟用<br>0112:無此權限使用功能 |
| MsgContent | 中文訊息 | string |  |
| Count | 筆數 | Int |  |

#### LoginData 登入取得資料
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S_BRANCH4_ACCOUNT7<br>期貨: F_F021013_BRANCH_ACCOUNT |
| Name | 客戶姓名 | string |  |
| InvestorID | 身分證字號 | string |  |
| SellerNo | 營業員代碼 | Short |  |

### LogOut

- 中文名稱：登出
- Function ID：(FunctionList 未列)
- 備註：登入的帳號全部登出
- 狀態：此項只有 FunctionList 條目，`doc/IO_Doc` 內未找到對應 IO spec md。

### Close

- 中文名稱：關閉API連線
- Function ID：(FunctionList 未列)
- 備註：(無)
- 狀態：此項只有 FunctionList 條目，`doc/IO_Doc` 內未找到對應 IO spec md。

### Dispose

- 中文名稱：釋放API連線
- Function ID：(FunctionList 未列)
- 備註：(無)
- 狀態：此項只有 FunctionList 條目，`doc/IO_Doc` 內未找到對應 IO spec md。

### SetLogType

- 中文名稱：設定Log類別
- Function ID：(FunctionList 未列)
- 備註：(無)
- 狀態：此項只有 FunctionList 條目，`doc/IO_Doc` 內未找到對應 IO spec md。

### OnResponse

- 中文名稱：回應事件
- Function ID：(FunctionList 未列)
- 備註：Server資料回應至Client端時所觸發的事件
- 來源：`OnResponse_IO_Spec.md`
- Service Desc：接收封包事件
- Delegate：`事件回應  OnResponseEventHandler(intMark, dwIndex, strIndex, objHandle, objValue)`

#### Output Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| intMark | 回應種類 | int | 0:系統資訊回應<br>1:查詢資訊回應<br>2:訂閱資訊回應 |
| dwIndex | 回應狀態 | uint | intMark為0：<br>0:其他訊息<br>1:Connect<br>2:Disconect<br>3:網路異常<br>4:需下載新版API<br>5:尚未連線<br>6:系統公告<br>intMark為1：<br>0:總帳/子帳登入<br>3:尚未登入<br>4:輸入的登入帳號錯誤<br>5:功能代碼錯誤,或權限不足<br>6:訂閱即時回報失敗<br>7:SocketRPRead失敗<br>9:加簽失敗/憑證異常<br>10:Logout!<br>11:帳號資訊異常<br>12:取得己訂閱商品清單異常<br>13:使用限制觸發<br>14:停權觸發<br>其他(FunctionID):功能回應<br>intMark為2：<br>1:訂閱/取消訂閱失敗<br>其他(FunctionID):功能回應<br>FunctionID請參考FunctionList.xlsx功能對照表 |
| strIndex | 功能名稱 | string | intMark為0：<br>空字串<br>intMark為1or2：<br>Function 例:SendStockOrder<br>空字串:查詢or訂閲功能有誤，請用string格式解析objValue<br>Function請參考FunctionList.xlsx功能對照表 |
| objHandle | Handle值 | object | 回傳訂閱事件時所傳入的Handle值(不處理) |
| objValue | 回傳資料 | object | intMark為0：<br>strIndex為空字串：<br>請用string格式解析<br>功能回應請依說明文件進行物件轉型並解析<br>非功能對照表功能請依舊元件方式解析byte[]<br>請參考FunctionList.xlsx功能對照表 |

### GetQuoteList

- 中文名稱：取得己訂閱即時報價商品清單
- Function ID：100001
- 來源：`GetQuoteList_IO_Spec.md`
- Service ID：API GetQuoteList
- Service Desc：取得己訂閱即時報價商品清單
- 呼叫簽名：`bool GetQuoteList(Account)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |

#### SubQuoteListResult 訂閱商品清單回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| QuoteList | 訂閱商品清單 | List&lt;Quote&gt; |  |

#### Quote 訂閱商品明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

### GetRealReportMerge

- 中文名稱：即時回報彙總查詢
- Function ID：100016
- 備註：帳務類發送
- 來源：`GetRealReportMerge_IO_Spec.md`
- Service ID：API GetRealReportMerge
- Service Desc：即時回報彙總查詢
- 呼叫簽名：`bool GetRealReportMerge(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### RealReportMergeResult 即時回報彙總結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| RealReportMergeList | 結果清單 | List&lt;RealReportMerge&gt; |  |

#### RealReportMerge 即時回報彙總物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| RptType | 回報類別 | Byte | 1:股票<br>2:期貨<br>3:選擇權<br>4:海外期貨<br>5:海外股票 |
| OrderNo | 委託單號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| CompanyNo | 商品代碼 | string | 2854, 05311<br>FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| OrderDate | 交易日 | TYuantaDate | 請參考API說明文件-物件 |
| OrderTime | 委託時間 | TYuantaTime | 請參考API說明文件-物件 |
| OrderType | 委託種類 | string | 現貨<br>0:普通<br>1,3:資<br>2,4:券<br>5:策略借券<br>6:避險借券<br>7:資沖<br>8:券沖<br>期權<br>M:市價<br>L:限價<br>P:範圍市價<br>海外期<br>LMT:限價單<br>MKT:市價單<br>STP:停損單<br>SWL:停損限價單<br>CXL:取消單<br>海外股票<br>1:Market<br>2:Limit 限價單 |
| BS | 買賣別 | string | S:賣<br>B:買 |
| Price | 委託價 | double | Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| TouchPrice | 停損執行價 | double | 000116'21.75 |
| LastDealPrice | 最新成交價 | double |  |
| AvgDealPrice | 成交均價 | double |  |
| BeforeQty | 改量前數量 | Int |  |
| OrderQty | 委託股數 | Int | 股數/口數<br>(有效數量含成交) |
| OkQty | 成交股數 | Int | 股數/口數 |
| OpenOffsetKind | 新增/沖銷別 | string | 期<br>0:新增<br>1:沖銷<br>2:新倉且當日沖銷單<br>權<br>0: 新增<br>1: 沖銷<br>海外股票(SettleType)<br>0:外幣<br>1:台幣 |
| DayTrade | 當沖記號 | string | 證券：' ' OR 'X'<br>期權：' ' OR 'Y' |
| OrderCond | 委託條件 | string | 證券<br>3:IOC<br>4:FOK<br>0:ROD<br>期權<br>F:FOK<br>I:IOC<br>R:ROD<br>海外期<br>0:DAY<br>2:IOC<br>1:FOK<br>N:非GTC單<br>海外股票<br>0:DAY<br>3:IOC<br>4:FOK |
| OrderErrorNo | 錯誤碼 | string | 證券以外的錯誤碼 |
| APCode | 委託類別 | Byte | 現貨<br>0:現股<br>2:零股<br>4:盤中零股<br>7:盤後<br>99:興櫃 |
| OrderStatus | 狀態碼 | Short | 0:傳輸中<br>5:預約單<br>10:委託失敗<br>20:委託成功<br>24:委託失效<br>25:價穩失效<br>30:取消 |
| LastOrderStatus | 最新一筆即回資料狀態 | Byte | 0:委託成功<br>1:委託失敗<br>2:取消成功<br>3:取消失敗<br>4:減量成功<br>5:減量失敗<br>6:查詢成功<br>7:查詢失敗<br>8:已成交<br>10:組合成功<br>11:拆解成功<br>12:平轉新<br>13:新轉平<br>18:委託收到<br>19:取消收到(國外股票)<br>20:改價成功<br>21:改價失敗<br>23:取消成交 (國外股票)<br>24:委託失效<br>25:價穩失效 |
| StkCName | 商品名稱 | string |  |
| TradeCode | 實體交易代號 | string | TradeCode 放下單格式<br>台股證券:"2854","03038","03152P"<br>台股期權:"FITX 200903","XIO C200811"<br>(商品名稱[6Byte]+買賣權[1Byte]+商品年月[6Byte])<br>港股證券:"0001","14200"港股期權:"HSIK8","HSI19800K8","HSI198I8/194U8"<br>美股:"A","MSFT" |
| StrikePrice | 履約價 | double |  |
| BasketNo | 一籃子下單編號 | string | 條件單識別資訊 |
| StkType1 | 屬性1 | Byte | Bit 1: 管理商品<br>Bit 2: 交易記號<br>Bit 3: 受益憑證<br>Bit 4: ETF商品<br>Bit 5: 權證記號<br>Bit 6: 特別股<br>Bit 7: 存託憑證<br>Bit 8: 外國股票 |
| StkType2 | 屬性2 | Byte | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: 保留 |
| BelongMarketNo | 所屬市場代碼 | Byte |  |
| BelongStkCode | 所屬股票代碼 | string |  |
| StkType | 價格種類 | string | 證券使用<br>1:市價<br>2:限價<br>H:漲停<br>L:跌停<br>“-”:平盤 |
| StkErrorNo | 證券回報錯誤碼 | string | 證券專用的錯誤碼 |

### GetRealReport

- 中文名稱：即時回報查詢
- Function ID：100020
- 備註：帳務類發送
- 來源：`GetRealReport_IO_Spec.md`
- Service ID：API GetRealReport
- Service Desc：即時回報查詢
- 呼叫簽名：`bool GetRealReport(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### RealReportResult 即時回報結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| RealReportList | 結果清單 | List&lt;RealReport&gt; |  |

#### RealReport 即時回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| RptType | 回報類別 | byte | 50:股票委託<br>51:股票成交<br>2:期貨委託<br>3:期貨成交<br>4:期貨價差成交回報<br>5:期貨委託減量取消<br>07:期貨改價回報<br>10:選擇權委託回報<br>11:單式成交回報<br>12:複式成交回報<br>13:選擇權減量取消回報<br>17:選擇權改價回報<br>21:組合拆解回報<br>22:改變新/平倉回報<br>30:海外期貨委託<br>31:海外期貨成交<br>32:海外期貨風控委託失敗單<br>40:海外股票委託,<br>41:海外股票委託取消<br>42:海外股票委託回覆,<br>43:海外股票委託取消回覆<br>44:海外股票成交 |
| OrderNo | 委託單號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| CompanyNo | 商品代碼 | string | 2854, 05311<br>FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| StkCName | 商品名稱 | string |  |
| OrderDate | 交易日 | TYuantaDate | 請參考API說明文件-物件 |
| OrderTime | 交易時間 | TYuantaTime | 請參考API說明文件-物件<br>委託時間/成交時間 |
| OrderType | 委託種類 | string | 現貨<br>0:普通<br>1,3:資<br>2,4:券<br>5:策略借券<br>6:避險借券<br>7:資沖<br>8:券沖<br>期權<br>M:市價<br>L:限價<br>P:範圍市價<br>海外期<br>LMT:限價單<br>MKT:市價單<br>STP:停損單<br>SWL:停損限價單<br>CXL:取消單<br>海外股票<br>1:Market<br>2:Limit 限價單 |
| BS | 買賣別 | String | S:賣<br>B:買 |
| Price | 價格 | double | 委託價 / 成交價<br>Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| TouchPrice | 停損執行價 | double | 000116'21.75 |
| BeforeQty | 改量前數量 | Int |  |
| OrderQty | 數量 | Int | 委託股數 / 成交股數 |
| OpenOffsetKind | 新增/沖銷別 | String | 期<br>0:新增<br>1:沖銷<br>2:新倉且當日沖銷單<br>權<br>0: 新增<br>1: 沖銷<br>海外股票(SettleType)<br>0:外幣<br>1:台幣 |
| DayTrade | 當沖記號 | String | 證券：' ' OR 'X'<br>期權：' ' OR 'Y' |
| OrderCond | 委託條件 | String | 證券<br>3:IOC<br>4:FOK<br>0:ROD<br>期權<br>F:FOK<br>I:IOC<br>R:ROD<br>海外期<br>0:DAY<br>2:IOC<br>1:FOK<br>N:非GTC單<br>海外股票<br>0:DAY<br>3:IOC<br>4:FOK |
| OrderErrorNo | 錯誤碼 | String | P201<br>證券以外的錯誤碼 |
| TradeKind | 交易性質 | byte | 現貨<br>1:B<br>2:S<br>3:改量<br>4:取消<br>5:查詢<br>6:改價<br>9:交易所主動刪單<br>期權<br>1:新增<br>2:減量<br>3:取消<br>5:查詢<br>6:改價 |
| APCode | 委託類別 | byte | 現貨<br>0:現股<br>2:零股<br>4:盤中零股<br>7:盤後<br>組合拆解回報<br>83:拆解<br>67:組合<br>改變新/平倉回報<br>83:新轉平<br>79:平轉新 |
| BasketNo | 一籃子下單編號 | String | 條件單識別資訊 |
| OrderStatus | 狀態碼 | short | 0:委託成功<br>1:委託失敗<br>2:取消成功<br>3:取消失敗<br>4:減量成功<br>5:減量失敗<br>6:查詢成功<br>7:查詢失敗<br>8:已成交<br>10:組合成功<br>11:拆解成功<br>12:平轉新<br>13:新轉平<br>18:委託收到<br>19:取消收到(國外股票)<br>20:改價成功<br>21:改價失敗<br>23:取消成交 (國外股票)<br>24:委託失效<br>25:價穩失效 |
| StkType1 | 屬性1 | Byte | Bit 1: 管理商品<br>Bit 2: 交易記號<br>Bit 3: 受益憑證<br>Bit 4: ETF商品<br>Bit 5: 權證記號<br>Bit 6: 特別股<br>Bit 7: 存託憑證<br>Bit 8: 外國股票 |
| StkType2 | 屬性2 | Byte | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: TSE/OTC創新板/興櫃戰略新板 |
| BelongMarketNo | 所屬市場代碼 | Byte |  |
| BelongStkCode | 所屬股票代碼 | String |  |
| SeqNo | 成交序號 | Uint | For 股票,期貨成交單<br>(複委託,國際期 -&gt;０)<br>若OrderStatus =25且StkErrCode =13051、19351，此欄位會帶入成交數量 |
| PriceType | 價格型態 | String | 只有證券使用<br>1:市價<br>2:限價<br>H:漲停<br>L:跌停<br>“-”:平盤 |
| StkErrorNo | 證券回報錯誤碼 | String | 證券回報錯誤碼 |

### GetOrderTradeReport

- 中文名稱：委託成交綜合回報
- Function ID：20101018
- 備註：帳務類發送
- 來源：`GetOrderTradeReport_IO_Spec.md`
- Service ID：API GetOrderTradeReport
- Service Desc：委託成交綜合回報
- 呼叫簽名：`GetOrderTradeReport(NotshowCancel, Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| NotshowCancel | 是否不列出取消單 | bool |  |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### OrderTradeReportResult 查詢委託成交回報結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| StkOrderList | 現貨委託回報清單 | List&lt;StkOrder&gt; |  |
| StkTradeList | 現貨成交回報清單 | List&lt;StkTrade&gt; |  |
| FutOrderList | 期貨委託回報清單 | List&lt;FutOrder&gt; |  |
| FutTradeList | 期貨成交回報清單 | List&lt;FutTrade&gt; |  |
| OVStkOrderList | 國外股票委託回報清單 | List&lt;OVStkOrder&gt; |  |
| OVStkTradeList | 國外股票成交回報清單 | List&lt;OVStkTrade&gt; |  |
| OVFutOrderList | 國外期貨委託回報清單 | List&lt;OVFutOrder&gt; |  |
| OVFutTradeList | 國外期貨成交回報清單 | List&lt;OVFutTrade&gt; |  |

#### StkOrder 現貨委託回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| TradeDate | 交易日 | TYuantaDate | 請參考API說明文件-物件 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string | 上市/上櫃 |
| CompanyNo | 股票代碼 | string |  |
| StkName | 股票名稱 | string |  |
| OrderType | 委託種類 | Short | 0:現貨<br>3:融資<br>4:融券<br>5:策略借券<br>6:避險借券<br>7:資沖<br>8:券沖 |
| BS | 買賣別 | string | S:賣<br>B:買 |
| Price | 價位 | double | 現貨小數4位,興櫃小數4位 |
| PriceFlag | 價格種類 | string | H:漲停<br>L:跌停<br>“-”:平盤<br>1-市價<br>2-限價 |
| BeforeQty | 前一次委託量 | Int | For 委託狀態=取消成功 |
| AfterQty | 目前委託量 | Int | 委託狀態=取消成功時,委託口數為0, 前端要改讀前一次委託量<br>委託狀態=10or24 |
| OkQty | 成交量 | Int |  |
| OrderStatus | 委託狀態 | Short | 0:傳輸中<br>5:預約單<br>10:委託失敗<br>20:委託成功<br>24:委託失效<br>25:價穩失效 <br>30:取消成功 |
| AcceptDate | 委託日期 | TYuantaDate | 請參考API說明文件-物件<br>年月日 |
| AcceptTime | 委託時間 | TYuantaTime | 請參考API說明文件-物件<br>時分秒毫秒 |
| OrderNo | 委託單號 | string | “H00001” |
| ErrorNo | 錯誤碼 | string |  |
| ErrorMessage | 錯誤訊息 | string |  |
| Seller | 營業員代碼 | Short |  |
| Channel | Channel | string |  |
| APCode | APCode | Short | 0:現貨<br>2:盤後零股<br>7:盤後<br>4:盤中零股<br>99:盤中零股 |
| OTax | 證交稅 | Int |  |
| OCharge | 手續費 | Int |  |
| ODueAmt | 應收付 | Int |  |
| CancelFlag | 可取消Flag | string | ‘Y’/’N’<br>盤中or 預約單才可取消 |
| ReduceFlag | 可減量Flag | string | ‘Y’/’N’<br>盤中or 預約單才可減量 |
| TraditionFlag | 傳統單Flag | string | ‘Y” :傳統單 |
| BasketNo | BasketNo | string | 條件單識別資訊 |
| TradeCurrency | 報價幣別 | string | TWD<br>CNY<br>HKD<br>USD |
| Time_in_Force | 委託效期 | string | 0:當日有效<br>3:IOC<br>4:FOK |
| Order_Success | 委託成功旗標 | string |  |
| Reduce_Flag | 本委託下單是否被減量 | string |  |
| Chg_Prz_Flag | 本委託下單是否進行改價 | string |  |
| TSE_Cancel | 本委託下單是否<br>被交易所主動刪單 | string |  |
| CancelQty | 取消數量 | Int |  |
| OR_QTY | 原委託量 | Int |  |
| UpdateDate | 更新日期 | TYuantaDate | 請參考API說明文件-物件<br>年月日 |
| UpdateTime | 更新時間 | TYuantaTime | 請參考API說明文件-物件<br>時分秒毫秒 |

#### StkTrade 現貨成交回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| CompanyNo | 股票代碼 | string |  |
| StkName | 股票名稱 | string |  |
| OrderType | 委託種類 | Short | 0:現貨<br>3:融資<br>4:融券<br>5:策略借券<br>6:避險借券<br>7:資沖<br>8:券沖 |
| BS | 買賣別 | string | S:賣<br>B:買 |
| OkQty | 成交量 | Int |  |
| OPrice | 委託價 | double | 現貨小數4位,興櫃小數4位 |
| SPrice | 成交價 | double | 現貨小數4位,興櫃小數4位 |
| DateTime | 交易日 | DateTime | 年月日時分秒毫秒 |
| OrderNo | 委託單號 | string | “H0001” |
| TradeCurrency | 報價幣別 | string | TWD<br>CNY<br>HKD<br>USD |
| Price_Flag | 價位Flag | string | 1-市價<br>2-限價 |
| Exchange_Code | 委託別 | Short | 0-一般委託<br>1-鉅額<br>2-零股<br>4-盤後定價<br>5 盤中零股 |

#### FutOrder 期貨委託回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| TradeDate | 交易日期 | TYuantaDate | 請參考API說明文件-物件 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| Commodity1 | 商品代碼1 | string | 選擇權第7碼是C或P |
| SettlementMonth1 | 商品月份1 | Int |  |
| StrikePrice1 | 履約價1 | double |  |
| BuySellKind1 | 買賣別1 | string |  |
| Commodity2 | 商品代碼2 | string | 選擇權第7碼是C或P |
| SettlementMonth2 | 商品月份2 | Int |  |
| StrikePrice2 | 履約價2 | double |  |
| BuySellKind2 | 買賣別2 | string |  |
| OpenOffsetKind | 新/平倉 | string | 0:新倉<br>1:平倉<br>2系統 |
| OrderCondition | 委託條件 | string | “ ”:ROD<br>”1”:FOK<br>”2”:IOC |
| OrderPrice | 委託價 | string | M:市價<br>P:範圍市價 |
| BeforeQty | 前一次委託量 | Int | For 委託狀態=取消成功 |
| AferQty | 目前委託量 | Int | 委託狀態=取消成功時,委託口數為0, 前端要改讀前一次委託量 |
| OKQty | 成交口數 | Int |  |
| OrderStatus | 委託狀態 | short | 0:傳輸中<br>5:預約單<br>10:委託失敗<br>20:委託成功<br>30:取消成功 |
| AcceptDate | 委託日期 | TYuantaDate | 請參考API說明文件-物件 |
| AcceptTime | 委託時間 | TYuantaTime | 請參考API說明文件-物件 |
| ErrorNo | 錯誤碼 | string |  |
| ErrorMessage | 錯誤訊息 | string |  |
| OrderNO | 委託單號 | string |  |
| ProductType | 商品種類 | string | O:選擇權<br>F:期貨 |
| Seller | 營業員代碼 | short |  |
| TotalMatFee | 手續費總和 | double |  |
| TotalMatExchTax | 交易稅總和 | double |  |
| TotalMatPremium | 應收付 | double |  |
| DayTradeID | 當沖註記 | string | Y:當沖 |
| CancelFlag | 可取消Flag | string | ‘Y’/’N’<br>盤中or 預約單才可取消 |
| ReduceFlag | 可減量Flag | string | ‘Y’/’N’<br>盤中or 預約單才可減量 |
| StkName1 | 商品名稱1 | string | Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’ |
| StkName2 | 商品名稱2 | string | Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’ |
| TraditionFlag | 傳統單Flag | string | ‘Y” :傳統單 |
| TRID | 商品代碼 | string | FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| CurrencyType | 交易幣別 | string | NTD:台幣<br>USD:美元 |
| CurrencyType2 | 交割幣別 | string | NTD:台幣<br>USD:美元 |
| BasketNo | BasketNo | string |  |
| MarketNo1 | 市場代碼1 | enumMarketType | 請參考API說明文件-列舉物件<br>&lt;第1支腳&gt; |
| StkCode1 | 行情股票代碼1 | string | &lt;第1支腳&gt; |
| MarketNo2 | 市場代碼2 | enumMarketType | 請參考API說明文件-列舉物件<br>&lt;第2支腳&gt; |
| StkCode2 | 行情股票代碼2 | string | &lt;第2支腳&gt; |

#### FutTrade 期貨成交回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| Commodity1 | 商品代號1 | string | 選擇權第7碼是C或P |
| SettlementMonth1 | 商品月份1 | Int |  |
| BuySellKind1 | 買賣別1 | string |  |
| OkQty | 成交口數 | Int |  |
| MatchPrice1 | 成交價1 | double |  |
| MatchPrice2 | 成交價2 | double |  |
| MatchTime | 成交時間 | TYuantaTime | 請參考API說明文件-物件 |
| MatchDate | 成交日期 | TYuantaDate | 請參考API說明文件-物件 |
| OrderNO | 委託單號 | string |  |
| StrikePrice1 | 履約價1 | double |  |
| Commodity2 | 商品代碼2 | string | 選擇權第7碼是C或P |
| SettlementMonth2 | 商品月份2 | Int |  |
| BuySellKind2 | 買賣別2 | string |  |
| StrikePrice2 | 履約價2 | double |  |
| RecType | 單式單/複式單 | string | “1”:單式<br>“2”:複式 |
| ProductType | 商品種類 | string |  |
| OrderPrice | 委託價 | double |  |
| StkName1 | 商品名稱1 | string | Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’ |
| StkName2 | 商品名稱2 | string | Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’ |
| DayTradeID | 當沖註記 | string |  |
| SprMatchPrice | 複式單成交價 | double |  |
| TRID | 商品代碼 | string | 2854, 05311<br>FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| CurrencyType | 交易幣別 | string | NTD:台幣<br>USD:美元 |
| CurrencyType2 | 交割幣別 | string | NTD:台幣<br>USD:美元 |
| SubNo | 子成交序號 | string | 0(單式)<br>1(複式腳1)<br>2(複式腳2) |

#### OVStkOrder 國外股票委託回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 證券帳號 | string |  |
| TradeDate | 交易日 | TYuantaDate | 請參考API說明文件-物件<br>西元年 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| CompanyNo | 商品代碼 | string |  |
| StkName | 商品名稱 | string |  |
| BS | 買賣別 | string | S:賣<br>B:買 |
| CurrencyType | 交易幣別 | string | USD:美元<br>HDK:港幣 |
| Price | 委託價 | double | 港股小數3位,美股小數4位 |
| PriceType | 價格型態 | string | ‘LMT’:限價單 |
| OrderQty | 委託量 | Int | 股數 |
| OkQty | 成交量 | Int |  |
| OrderStatus | 狀態碼 | short | 0:傳輸中<br>5:預約單<br>10:委託失敗<br>20:委託成功<br>30:取消成功 |
| OrderTime | 委託時間 | DateTime |  |
| OrderType | 委託單型態 | string | DAY:當日有效單<br>GTD:指定日期單 |
| OrderNo | 委託單號 | string |  |
| Fee | 手續費 | double |  |
| PolarisAMT | 應收付金額 | double |  |
| ErrorNo | 錯誤碼 | string |  |
| ErrorMessage | 錯誤訊息 | string |  |
| CurrencyType2 | 交割幣別 | string | USD:美元<br>HDK:港幣 |
| CancelFlag | 可取消Flag | string | ‘Y’/’N’<br>盤中or 預約單才可取消 |
| ReduceFlag | 可減量Flag | string | ‘Y’/’N’<br>＊美股不提供改量改價功能,由元件固定回N |
| TraditionFlag | 傳統單Flag | string | ‘Y” :傳統單 |
| SettleType | 交割方式 | string | 0:外幣<br>1:台幣 |
| BasketNo | BasketNo | string | smart-04:長效單 |

#### OVStkTrade 國外股票成交回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| CompanyNo | 商品代碼 | string |  |
| StkName | 商品名稱 | string |  |
| BS | 買賣別 | string | S:賣<br>B:買 |
| CurrencyType | 交易幣別 | string | USD:美元<br>HDK:港幣 |
| OkQty | 成交量 | Int |  |
| OrderPrice | 委託價 | double | 港股小數3位,美股小數4位 |
| MatchPrice | 成交價 | double | 港股小數3位,美股小數4位 |
| DateTime | 成交時間 | DateTime |  |
| Fee | 手續費 | double |  |
| OrderNo | 委託單號 | string |  |
| SettlementAMT | 成交金額 | double | 含手續費 |
| CurrencyType2 | 交割幣別 | string | USD:美元<br>HDK:港幣 |

#### OVFutOrder 國外期貨委託回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| TradeDate | 交易日 | TYuantaDate | 請參考API說明文件-物件<br>西元年 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| CompanyNo | 商品代碼 | string | URO,JGL |
| SettlementMonth | 商品年月 | Int | 200909 |
| StkName | 商品名稱 | string |  |
| BS | 買賣別 | string | “B”:買<br>“S”:賣 |
| OrderType | 委託方式 | string | LMT:限價單<br>MKT:市價單<br>STP:停損市價單<br>SWL:停損限價單 |
| Price | 委託價 | double | 000116’21.75 |
| TouchPrice | 停損執行價 | double | 000116’21.75 |
| OrderQty | 委託口數 | int |  |
| OkQty | 成交口數 | int |  |
| OrderStatus | 狀態碼 | short | 0:傳輸中<br>5:預約單<br>10:委託失敗<br>20:委託成功<br>30:取消成功 |
| AcceptDate | 委託日期 | TYuantaDate | 請參考API說明文件-物件 |
| AcceptTime | 委託時間 | TYuantaTime | 請參考API說明文件-物件 |
| ErrorNo | 錯誤代碼 | string |  |
| ErrorMessage | 錯誤訊息 | string |  |
| OrderNo | 委託單號 | string | AA0484 |
| DayTradeID | 當沖註記 | string | Y :當沖 |
| CancelFlag | 可取消Flag | string | ‘Y’/’N’<br>盤中or 預約單才可取消 |
| ReduceFlag | 可減量Flag | string | 國際期貨目前無提供減量<br>‘P’:可改價 |
| UtPrice | 委託價格整數位 | double | 市價或市價停損單= 0<br>&lt;For 取消下單時使用&gt; |
| UtPrice2 | 委託價格分子 | double | &lt;For 取消下單時使用&gt; |
| MinPrice2 | 委託價格分母 | Int | &lt;For 取消下單時使用&gt; |
| UtPrice4 | 停損執行價整數位 | double | 非停損單=0<br>&lt;For 取消下單時使用&gt; |
| UtPrice5 | 停損執行價格分子 | double | &lt;For 取消下單時使用&gt; |
| UtPrice6 | 停損執行價格分母 | Int | &lt;For 取消下單時使用&gt; |
| TraditionFlag | 傳統單Flag | string | ‘Y” :傳統單 |
| BasketNo | BasketNo | string |  |
| MarketNo1 | 市場代碼1 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode1 | 行情股票代碼1 | string |  |
| CurrencyType | 交易幣別 | string |  |
| CurrencyType2 | 交割幣別 | string |  |

#### OVFutTrade 國外期貨成交回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| CompanyNo | 商品代碼 | string | URO,JGL |
| SettlementMonth | 商品年月 | Int | 200909 |
| StkName | 商品名稱 | string |  |
| BS | 買賣別 | string | “B”:買<br>“S”:賣 |
| OkQty | 成交口數 | int |  |
| OrderPrice | 委託價 | double | 000116’21.75 |
| MatchPrice | 成交價 | double | 000116’21.75 |
| MatchDate | 成交日期 | TYuantaDate | 請參考API說明文件-物件 |
| MatchTime | 成交時間 | TYuantaTime | 請參考API說明文件-物件 |
| OrderNo | 委託單號 | string | AA0484 |
| CurrencyType | 交易幣別 | string | NTD:台幣<br>USD:美元 |
| CurrencyType2 | 交割幣別 | string | NTD:台幣<br>USD:美元 |

### GetStoreSummary

- 中文名稱：股票庫存綜合總表
- Function ID：20103022
- 備註：帳務類發送
- 來源：`GetStoreSummary_IO_Spec.md`
- Service ID：API GetStoreSummary
- Service Desc：股票庫存綜合總表
- 呼叫簽名：`bool GetStoreSummary(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StoreSummaryResult 查詢股票庫存總表結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| StkStoreList | 現貨庫存清單 | List&lt;StkStore&gt; |  |
| OVStkStoreList | 國外股票庫存清單 | List&lt;OVStkStore&gt; |  |

#### StkStore 現貨庫存物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| TradeKind | 交易種類 | Int | 0:現股 <br>3:資買  <br>4:券賣 <br>6:借券 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string | 上市/上櫃 |
| StkCode | 股票代號 | string |  |
| StkName | 股票名稱 | string |  |
| StockQty | 股數 | Long |  |
| Price | 成交均價 | double |  |
| Cost | 持有成本 | double |  |
| Interest | 預估利息 | Long |  |
| BuyNotInNos | 買進未入帳股數 | Int |  |
| SellNotInNos | 賣出未入帳股數 | Int |  |
| TradingQty | 可交易股數 | Long |  |
| Loan | 資保證金/券擔保價品 | Long |  |
| TaxRate | 交易稅率 | double | 0:Reits 股票 <br>1:基金,認股權證,債券,存託憑證<br>3:一般股票<br>(單位千分之一) |
| LotSize | 交易單位 | Int | 每手股數 |
| MarketPrice | 市價 | double | 盤前市價若為0則給開盤參考價 |
| Decimal | 小數位數 | Int | +為小數位數<br>-為分數分母<br>0為整數 |
| StkType1 | 屬性1 | Int | Bit 1: 管理商品<br>Bit 2: 交易記號<br>Bit 3: 受益憑證<br>Bit 4: ETF商品<br>Bit 5: 權證記號<br>Bit 6: 特別股<br>Bit 7: 存託憑證<br>Bit 8: 外國股票 |
| StkType2 | 屬性2 | Int | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: 保留 |
| BuyPrice | 買價 | double |  |
| SellPrice | 賣價 | double |  |
| UpStopPrice | 漲停價 | double |  |
| DownStopPrice | 跌停價 | double |  |
| PriceMultiplier | 計價倍數 | uint | 1，乘1倍<br>10，乘10倍 |
| CurrencyType | 幣別 | string | TWD<br>CNY<br>HKD<br>USD |
| CDQTY | 借貸股數 | Long |  |
| OddTradingQty | 零股可下單股數 | Long |  |
| ReturnAmt | 未實現損益 | double |  |
| MarketAmt | 股票市值 | double |  |

#### OVStkStore 國外股票庫存物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 現貨帳號 | string |  |
| CurrencyType | 幣別 | string | USD:美元<br>HKD:港幣 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| MarketName | 市場名稱 | string |  |
| StkCode | 股票代號 | string |  |
| StkName | 股票名稱 | string |  |
| StkFullName | 股票全名 | string |  |
| StockQty | 庫存股數 | Long |  |
| TradingQty | 可交易股數 | Long |  |
| Price | 成交均價 | double |  |
| Cost | 持有成本 | double |  |
| CloseRate | 匯率 | double |  |
| RateKind | 匯率運算模式 | Int | 1:除以匯率<br>2:乘以匯率 |
| LotSize | 交易單位 | int | 每手股數 |
| MarketPrice | 市價 | double | 固定為0,前端自行根據登入權限查詢 |
| Decimal | 小數位數 | Int | +為小數位數<br>-為分數分母<br>0為整數 |
| BuyPrice | 買價 | int |  |
| SellPrice | 賣價 | int |  |

### GetFutStoreSummary

- 中文名稱：期貨庫存總表查詢
- Function ID：201032013
- 備註：帳務類發送
- 來源：`GetFutStoreSummary_IO_Spec.md`
- Service ID：API GetFutStoreSummary
- Service Desc：期貨庫存總表查詢
- 呼叫簽名：`bool GetFutStoreSummary(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FutStoreSummaryResult 查詢期貨庫存總表結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| FutStoreList | 期貨庫存清單 | List&lt;FutStore&gt; |  |

#### FutStore 期貨庫存物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| FutAccount | 帳號 | string |  |
| Kind | 期權別 | string | 期貨(F)/選擇權(O)/期貨+選擇權(C) |
| Trid | 商品代碼 | string | TX109100E4/TXO09000E4 |
| BS | 買賣別 | string | 買(B)/賣(S) |
| Qty | 未平倉口數 | Int |  |
| Amt | 總成交點數 | double |  |
| Fee | 手續費 | double |  |
| Tax | 交易稅 | double |  |
| CurrencyType | 幣別 | string | NTD:台幣 |
| DayTradeID | 當沖註記 | string | “Y”:當沖 “ ”:空白 |
| Commodity1 | 商品代碼1 | string | TXO |
| CallPut1 | 買賣權1 | string | C/P |
| SettlementMonth1 | 商品月份1 | Int | 200712 |
| StrikePrice1 | 履約價1 | double |  |
| BS1 | 買賣別1 | string | 買(B)/賣(S) |
| StkName1 | 商品名稱1 | string | Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’ |
| MarketNo1 | 市場代碼1 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode1 | 行情報價代碼1 | string | 7799,TXO04600A9 |
| Commodity2 | 商品代碼2 | string | TXO |
| CallPut2 | 買賣權2 | string | C/P |
| SettlementMonth2 | 商品月份2 | Int | 200712 |
| StrikePrice2 | 履約價2 | double |  |
| BS2 | 買賣別2 | string | 買(B)/賣(S) |
| StkName2 | 股票名稱2 | string | Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’ |
| MarketNo2 | 市場代碼2 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode2 | 行情報價代碼2 | string | 7799,TXO04700A9 |
| BuyPrice1 | 買入價1 | double |  |
| SellPrice1 | 賣出價1 | double |  |
| MarketPrice1 | 市價1 | double | 盤前市價若為0 則給開盤參考價 |
| BuyPrice2 | 買入價2 | double |  |
| SellPrice2 | 賣出價2 | double |  |
| MarketPrice2 | 市價2 | double | 盤前市價若為0 則給開盤參考價 |
| Decimal | 小數位數 | Short | +為小數位數,-為分數分母,<br>0為整數 |
| ProductType1 | 商品類別1 | string | “F”:期貨 “O”:選擇權 |
| ProductKind1 | 商品屬性1 | string | “I”:指數 “R”:利率 “B”:債券<br>“C”:商品 “S”:股票 |
| ProductType2 | 商品類別2 | string | “F”:期貨 “O”:選擇權 |
| ProductKind2 | 商品屬性2 | string | “I”:指數 “R”:利率 “B”:債券<br>“C”:商品 “S”:股票 |
| UpStopPrice1 | 漲停價1 | double |  |
| DownStopPrice1 | 跌停價1 | double |  |
| UpStopPrice2 | 漲停價2 | double |  |
| DownStopPrice2 | 跌停價2 | double |  |
| StkCode1opp | 行情股票代碼1反向 | string | &lt;第1支腳&gt; |
| StkCode2opp | 行情股票代碼2反向 | string | &lt;第2支腳&gt; |

### GetOVFutStoreSummary

- 中文名稱：國際期貨庫存總表查詢
- Function ID：201034018
- 備註：帳務類發送
- 來源：`GetOVFutStoreSummary_IO_Spec.md`
- Service ID：API GetOVFutStoreSummary
- Service Desc：國際期貨庫存總表查詢
- 呼叫簽名：`bool GetOVFutStoreSummary(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### OVFutStoreSummaryResult 查詢國際期貨庫存總表結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| OVFutStoreList | 國際期貨庫存清單 | List&lt;OVFutStore&gt; |  |

#### OVFutStore 國際期貨庫存物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| FutAccount | 帳號 | string |  |
| Kind | 委託種類 | string | 期貨(F)/選擇權(O) |
| Trid | 商品代碼 | string |  |
| BS | 買賣別 | string | 買(B)/賣(S) |
| Qty | 未平倉口數 | long |  |
| Amt | 總成交點數 | double |  |
| Commodity1 | 商品代碼1 | string | EC, URO |
| CallPut1 | 買賣權1 | string | C/P |
| SettlementMonth1 | 交易月份1 | Int | 201101 |
| StkName1 | 商品名稱1 | string | 中文名稱 |
| StrikePrice1 | 履約價1 | double |  |
| Commodity2 | 商品代碼2 | string | EC |
| CallPut2 | 買賣權2 | string | C/P |
| SettlementMonth2 | 交易月份2 | Int | 201101 |
| StkName2 | 商品名稱2 | string | 中文名稱 |
| StrikePrice2 | 履約價2 | double |  |
| Fee | 手續費 | double |  |
| CurrencyType | 幣別 | string | AUD澳幣,EUR歐元,GBP英鎊,HKD港幣,JPY日幣,NTD新台幣,SGD新加坡幣,USD美金 |
| DayTradeID | 當沖註記 | string | “Y”:當沖 “ ”:空白 |
| BS1 | 買賣別1 | string | 買(B)/賣(S) |
| BS2 | 買賣別2 | string | 買(B)/賣(S) |
| OptProdKind1 | 選擇權商品種類1 | string | &lt;第1支腳&gt;<br>"0":期貨選擇權<br>"1":現貨選擇權 |
| OptProdKind2 | 選擇權商品種類2 | string | &lt;第2支腳&gt;<br>“0”:期貨選擇權<br>“1”:現貨選擇權 |
| MarketNo1 | 市場代碼1 | enumMarketType | 請參考API說明文件-列舉物件<br>&lt;第1支腳&gt; |
| StkCode1 | 行情報價代碼1 | string | &lt;第1支腳&gt; |
| MarketNo2 | 市場代碼2 | enumMarketType | 請參考API說明文件-列舉物件<br>&lt;第2支腳&gt; |
| StkCode2 | 行情股票代碼2 | string | &lt;第2支腳&gt; |
| BuyPrice1 | 買入價1 | double | &lt;第1支腳&gt; |
| SellPrice1 | 賣出價1 | double | &lt;第1支腳&gt; |
| MarketPrice1 | 市價1 | double | &lt;第1支腳&gt;<br>盤前市價若為0 則給開盤參考價 |
| BuyPrice2 | 買入價2 | double | &lt;第2支腳&gt; |
| SellPrice2 | 賣出價2 | double | &lt;第2支腳&gt; |
| MarketPrice2 | 市價2 | double | &lt;第2支腳&gt;<br>盤前市價若為0 則給開盤參考價 |
| Decimal | 小數位數 | Short | +為小數位數,-為分數分母,<br>0為整數 |
| Decimal2 | 小數位數2 | Short | +為小數位數,-為分數分母,<br>0為整數 |
| TickDiff | 檔差 | Int | 檔差不是固定的就為0，例如台股都為0；海外股票跟海外期貨預留用的；若檔差是0.05，且他的小數位是3位，檔差就是50 |

### GetFutInterestStore

- 中文名稱：期貨權益數查詢
- Function ID：201042020
- 備註：帳務類發送
- 來源：`GetFutInterestStore_IO_Spec.md`
- Service ID：API GetFutInterestStore
- Service Desc：期貨權益數查詢
- 呼叫簽名：`bool GetFutInterestStore(Account, Type, Currency, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| Type | 型態 | string | 1:基本幣別<br>2:明細幣別 |
| Currency | 幣別 | string | TWD:台幣<br>USA:美金<br>CNA:人民幣<br>JPA:日圓 |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FutInterestStoreResult 查詢期貨權益數結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ReplyCode | 委託結果代碼 | Short | 0:委託成功 others:委託失敗 |
| Advisory | 錯誤說明 | String |  |
| Type | 型態 | String | 1:基本幣別<br>2:明細幣別 |
| Currency | 幣別 | String | TWD:台幣<br>USA:美金<br>CNA:人民幣<br>JPA:日圓 |
| Equity | 權益數 | double |  |
| AllFullIm | 全額原始保證金 | double |  |
| CanuseMargin | 可運用保證金 | double |  |
| RiskRate | 權益比率 | String |  |
| DaytradeRisk | 當沖風險指標 | String |  |
| AllRiskRate | 風險指標 | String |  |
| CashForward | 前日餘額 | double |  |
| OpenGlYes | 昨日未平倉損益 | double |  |
| UpdateTime | 風險更新時間 | DateTime |  |
| Accounting | 存/提 | double |  |
| FloatMargin | 未沖銷期貨浮動損益 | double |  |
| FloatPremium | 未沖銷買方選擇權市值+<br>未沖銷賣方選擇權市值 | double |  |
| CommissionAll | 手續費 | double |  |
| TotalValue | 權益總值 | double |  |
| TaxRate | 期交稅 | double |  |
| AllIm | 原始保證金 | double |  |
| CallMargin | 追繳保證金 | double |  |
| Grantal | 本日期貨平倉損益淨額+<br>到期履約損益 | double |  |
| AllMm | 維持保證金 | double |  |
| OrderIm | 委託保證金 | double |  |
| Premium | 權利金收入與支出 | double |  |
| OrderPremium | 委託權利金 | double |  |
| Balance | 本日餘額 | double |  |
| CanusePremium | 可動用(出金)保證金(含抵委) | double |  |
| CoveredOim | 委託抵繳保證金 | double |  |
| BondAmt | 債券實物交割款 | double |  |
| NobondAmt | 債券實物不足交割款 | double |  |
| BondMargin | 債券待交割保證金 | double |  |
| CoveredIm | 有價證券抵繳總額 | double |  |
| ReduceIm | 期貨多空減收保證金 | double |  |
| IncreaseIm | 加收保證金 | double |  |
| YTotalValue | 昨日權益總值 | double |  |
| Rate | 匯率 | double |  |
| BestFlag | 客戶保證金計收方式 | string | ‘ ’: 傳統(策略)<br>‘S’:整戶風險(SPAN)<br>‘Y’:保證金最佳化 |
| GlToday | 本日損益 | double |  |
| DspEquity | 風險權益總值 | double |  |
| DspFloatmargin | 未沖銷期貨風險浮動損益 | double |  |
| DspFloatpremium | 未沖銷買方選擇權風險市值+未沖銷賣方選擇權風險市值 | double |  |
| DspIM | 風險原始保證金 | double |  |
| DspRiskRate | 盤後風險指標 | double |  |

### GetFutDepositOptimum

- 中文名稱：期貨保證金最佳化查詢
- Function ID：201042017
- 備註：帳務類發送，特殊功能需申請權限
- 來源：`GetFutDepositOptimum_IO_Spec.md`
- Service ID：API GetFutDepositOptimum
- Service Desc：期貨保證金最佳化查詢
- 呼叫簽名：`bool GetFutDepositOptimum(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### DepositOptimumResult 期貨保證金最佳化查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| DepositOptimumList | 結果清單 | List&lt;DepositOptimum&gt; |  |

#### DepositOptimum 期貨保證金最佳化物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| StrategyID | 策略ID | Byte | 6.買賣權混合部位(跨式,勒式)<br>7.多頭價差<br>8.Put空頭價差<br>9.溫跌作莊<br>10.溫漲作莊<br>11.Call時間價差<br>12.Put時間價差 |
| FutAccountInfo | 期貨帳號 | string |  |
| Qty | 口數 | Short |  |
| BuySell1 | 買賣別1 | string | B, S |
| BuySell2 | 買賣別2 | string | B, S |
| DealPrice1 | 成交價1 | double | 此值即為市價 |
| DealPrice2 | 成交價2 | double | 此值即為市價 |
| Decimal1 | 小數位數1 | Short | +為小數位數,-為分數分母<br>0為整數 |
| CurrentIM1 | 商品一保證金 | Int |  |
| CurrentIM2 | 商品二保證金 | Int |  |
| SaveIM | 可節省保證金 | Int |  |
| CommodityID1 | 商品ID1 | string | TXO |
| CallPut1 | 買賣權1 | string | C/P |
| SettlementMonth1 | 商品年月1 | Int | 202502 |
| StrikePrice1 | 履約價1 | double |  |
| StkName1 | 商品名稱1 | string | 台指選 02 22800 P |
| CommodityID2 | 商品ID2 | string | TXO |
| CallPut2 | 買賣權2 | string | C/P |
| SettlementMonth2 | 商品年月2 | Int | 202502 |
| StrikePrice2 | 履約價2 | double |  |
| StkName2 | 商品名稱2 | string | 台指選 02 23000 P |

### SendStockOrder

- 中文名稱：國內證券下單
- Function ID：301001031
- 備註：交易類發送
- 來源：`SendStockOrder_IO_Spec.md`
- Service ID：API SendStockOrder
- Service Desc：國內證券下單
- 呼叫簽名：`bool SendStockOrder(LoginAcno, lstStockOrder, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 下單帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| lstStockOrder | 下單物件清單 | List&lt;StockOrder&gt; |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StockOrder 國內現貨下單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identity | 識別碼 | Int |  |
| Account | 下單帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| OrderNo | 委託書編號 | string | 委託新單不需填 |
| TradeDate | 交易日期 | string | yyyy/MM/dd |
| APCode | 交易單市場別 | short | 0:一般<br>2:零股<br>4:盤中零股<br>7:盤後 |
| TradeKind | 交易性質 | short | 00:委託單<br>03:改量<br>04:取消<br>07:改價 |
| OrderType | 委託種類 | string | "0":現貨<br>"3":融資<br>"4":融券<br>"5":策略借券(賣出)<br>"6":避險借券(賣出)<br>"9":現股當沖委託控管 |
| StkCode | 股票代號 | string |  |
| BuySell | 買賣記號 | string | "B":買<br>"S":賣 |
| PriceFlag | 價格種類 | string | H:漲停<br>-:平盤<br>L:跌停<br>" ":限價<br>M:市價單 |
| Price | 委託價格 | double | 非限價請填0 |
| BasketNo | 使用者自訂欄位 | string | (限32個英數字內)<br>若為條件單委託請將識別資訊帶入 |
| OrderQty | 委託單位 | long |  |
| Time_in_force | 委託時間效期 | string | 0:ROD<br>3:IOC<br>4:FOK |

#### StkOrderResult 國內證券下單結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultCount | 交易狀態 | OrderStatus |  |
| ResultList | 國內證券下單結果清單 | List&lt;StkOrderData&gt; |  |

#### OrderStatus 交易類狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MsgCode | 訊息代碼 | string | 0001:執行成功 其它:失敗 |
| MsgContent | 訊息內容 | string |  |
| Count | 筆數 | Int |  |

#### StkOrderData 國內證券下單結果明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identify | 識別碼 | Int |  |
| ReplyCode | 委託結果代碼 | Short | 0:委託成功 others:委託失敗 |
| OrderNO | 委託書編號 | Tbyte5 |  |
| TradeDate | 交易日期 | DateTime | 日期 |
| ErrType | 錯誤類別 | string |  |
| ErrNO | 錯誤代號 | string | A003:預約單不支援改價或無此委託單<br>A004:委託已成交，無法改價<br>A005:委託已取消，無法改價 |
| Advisory | 錯誤說明 | string |  |

### SendFutureOrder

- 中文名稱：國內期貨下單
- Function ID：301002024
- 備註：交易類發送
- 來源：`SendFutureOrder_IO_Spec.md`
- Service ID：API SendFutureOrder
- Service Desc：國內期貨下單
- 呼叫簽名：`bool SendFutureOrder(LoginAcno, lstFutureOrder, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 下單帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| lstFutureOrder | 下單物件清單 | List&lt;FutureOrder&gt; |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FutureOrder 國內期貨下單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identity | 識別碼 | Int |  |
| Account | 下單帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| OrderNo | 委託書編號 | string | 委託新單不需填 |
| TradeDate | 交易日期 | string | yyyy/MM/dd |
| FunctionCode | 功能別 | short | 00:委託單<br>04:取消<br>05:改量<br>07:改價<br>(Opt複式單沒有改價) |
| CommodityID1 | 商品名稱1 | string | 請參考 FunctionList.xlsx<br>股名檔對照表的下單代碼<br>如:台指-&gt;FITX<br>如:台指選-&gt;TXO |
| CallPut1 | 買賣權1 | string | "C":Call<br>"P":Put<br>(選擇權才需填值) |
| SettlementMonth1 | 商品月份1 | Int | 如:201912 |
| Price | 委託價格 | double | 非限價請填0 |
| StrikePrice1 | 履約價1 | double |  |
| OrderQty1 | 委託口數1 | short |  |
| BuySell1 | 買賣別1 | string | "B":買<br>"S":賣 |
| CommodityID2 | 商品名稱2 | string |  |
| CallPut2 | 買賣權2 | string | "C":Call<br>"P":Put<br>(選擇權才需填值) |
| SettlementMonth2 | 商品月份2 | Int | 如:201912 |
| StrikePrice2 | 履約價2 | double |  |
| OrderQty2 | 委託口數2 | short |  |
| BuySell2 | 買賣別2 | string | "B":買<br>"S":賣 |
| OpenOffsetKind | 新平倉 | string | 0:新倉<br>1:平倉<br>2:自動 |
| DayTradeID | 當沖註記 | string | "Y":當沖<br>" ":空白 |
| OrderType | 委託方式 | string | 1:市價<br>2:限價<br>3:範圍市價 |
| OrderCond | 委託條件 | string | " ":ROD<br>I:FOK<br>2:IOC |
| SellerNo | 營業員代碼 | short | 請填0 |
| BasketNo | BasketNo | string | 目前無作用 |
| Session | 盤別 | string | 1:預約<br>其他:盤中單 |

#### FutOrderResult 國內期貨下單結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultCount | 交易狀態 | OrderStatus |  |
| ResultList | 國內期貨下單結果清單 | List&lt;FutOrderData&gt; |  |

#### OrderStatus 交易類狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MsgCode | 訊息代碼 | string | 0001:執行成功 其它:失敗 |
| MsgContent | 訊息內容 | string |  |
| Count | 筆數 | Int |  |

#### FutOrderData 國內期貨下單結果明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identify | 識別碼 | Int |  |
| ReplyCode | 委託結果代碼 | Short | 0:委託成功 others:委託失敗 |
| OrderNO | 委託書編號 | string |  |
| TradeDate | 交易日期 | DateTime | 日期 |
| ErrType | 錯誤類別 | string |  |
| ErrNO | 錯誤代號 | string |  |
| Advisory | 錯誤說明 | string |  |

### SendFutureCombined

- 中文名稱：期貨複式單組合
- Function ID：301002014
- 備註：交易類發送，特殊功能需申請權限
- 來源：`SendFutureCombined_IO_Spec.md`
- Service ID：API SendFutureCombined
- Service Desc：期貨複式單組合
- 呼叫簽名：`bool SendFutureCombined(LoginAcno, lstDepositOptimum, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 組合帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| lstDepositOptimum | 組合物件清單 | List&lt;DepositOptimum&gt; | 建議由保證金最佳化查詢結果篩選代入 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### DepositOptimum 期貨保證金最佳化物件
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| StrategyID | 策略ID | Byte | 6.買賣權混合部位(跨式,勒式))<br>7.多頭價差<br>8.Put空頭價差<br>9.溫跌作莊<br>10.溫漲作莊<br>11.Call時間價差<br>12.Put時間價差 |
| FutAccountInfo | 期貨帳號 | string |  |
| Qty | 口數 | Short |  |
| BuySell1 | 買賣別1 | string | B, S |
| BuySell2 | 買賣別2 | string | B, S |
| DealPrice1 | 成交價1 | double | 此值即為市價 |
| DealPrice2 | 成交價2 | double | 此值即為市價 |
| Decimal1 | 小數位數1 | Short | +為小數位數,-為分數分母,0為整數 |
| CurrentIM1 | 商品一保證金 | Int |  |
| CurrentIM2 | 商品二保證金 | Int |  |
| SaveIM | 可節省保證金 | Int |  |
| CommodityID1 | 商品ID1 | string | TXO |
| CallPut1 | 買賣權1 | string | C/P |
| SettlementMonth1 | 商品年月1 | Int | 202502 |
| StrikePrice1 | 履約價1 | double |  |
| StkName1 | 商品名稱1 | string | 台指選 02 22800 P |
| CommodityID2 | 商品ID2 | string | TXO |
| CallPut2 | 買賣權2 | string | C/P |
| SettlementMonth2 | 商品年月2 | Int | 202502 |
| StrikePrice2 | 履約價2 | double |  |
| StkName2 | 商品名稱2 | string | 台指選 02 23000 P |

#### FutCombinedResult 複合式組合下單結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultCount | 交易狀態 | OrderStatus |  |
| ResultList | 複合式組合下單結果清單 | List&lt;FutCombinedData&gt; |  |

#### OrderStatus 交易類狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MsgCode | 訊息代碼 | string | 0001:執行成功 其它:失敗 |
| MsgContent | 訊息內容 | string |  |
| Count | 筆數 | Int |  |

#### FutCombinedData複合式組合下單結果明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identify | 識別碼 | Int |  |
| ReplyCode | 委託結果代碼 | Short | 0:委託成功 others:委託失敗 |
| ErrType | 錯誤類別 | string |  |
| ErrNO | 錯誤代號 | string |  |
| Advisory | 錯誤說明 | string |  |

### GetWatchListAll

- 中文名稱：報價表查詢
- Function ID：500016
- 備註：報價類發送
- 來源：`GetWatchListAll_IO_Spec.md`
- Service ID：API GetWatchListAll
- Service Desc：報價表查詢
- 呼叫簽名：`bool GetWatchListAll(Account, QuoteList, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| QuoteList | 查詢商品清單 | List&lt;Quote&gt; |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### Quote 訂閱商品明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### QueryWatchListResult 查詢報價表結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| QueryWatchList | 結果清單 | List&lt;QueryWatchList&gt; |  |

#### QueryWatchList 報價表物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| StkName | 股票名稱 | string |  |
| YstPrice | 昨收價 | double |  |
| OpenRefPrice | 開盤參考價 | double |  |
| UpStopPrice | 漲停價 | double |  |
| DownStopPrice | 跌停價 | double |  |
| YstVol | 昨量 | int |  |
| ExtName | 擴充名 | string |  |
| Decimal | 小數位數 | short |  |
| CreditPercent | 融資成數 | int | 未提供,回傳0 |
| LenBondPercent | 融券成數 | int | 未提供,回傳0 |
| OpenPrice | 開盤價 | double |  |
| HighPrice | 最高價 | double |  |
| LowPrice | 最低價 | double |  |
| BuyPrice | 買價 | double | 市價買:999999999 |
| TotalOutVol | 累計外盤量 | int |  |
| SellPrice | 賣價 | double | 市價賣:-999999999 |
| TotalInVol | 累計內盤量 | int |  |
| DealPrice | 成交價 | double |  |
| TotalDealAmt | 總成交金額 | int |  |
| VolFlag | 單量內外盤標記 | Byte | 0:內盤/1:外盤 |
| Vol | 單量 | int | 最高位元的Bit，<br>表示內/外盤的旗標，<br>0:內盤/1:外盤 |
| TotalVol | 總成交量 | long |  |
| FixedPriceVol | 定價量 | int |  |
| ReserveVol | 未平倉量 | int |  |
| SettlementPrice | 結算價 | double |  |
| HiContractPrice | 合約高價 | double |  |
| LoContractPrice | 合約低價 | double |  |
| OrderBuyCount | 委託買進總筆數 | int |  |
| OrderBuyQty | 委託買進總口數 | int |  |
| OrderSellCount | 委託賣出總筆數 | int |  |
| OrderSellQty | 委託賣出總口數 | int |  |
| DealBuyCount | 累計買進成交筆數 | int |  |
| DealSellCount | 累計賣出成交筆數 | int |  |
| Volatility | 波動率 | int |  |
| Time | 時間 | DateTime | 時間 |
| TimeDiff | 時差 | string | 台股為0，（晚＝正值，早＝負值）。日本比台灣早一小時，時差就是等於-1 |
| StkType2 | 屬性2 | Byte | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: 保留 |
| ReserveVolDiff | 未平倉量增減 | int |  |
| BelongCode | 所屬產業分類碼 | string | 01: 水泥工業<br>02: 食品工業<br>03: 塑膠工業 |
| IndustryName | 產業類股名稱 | string |  |
| PrincipalPercent | 市值(%) | double | 小數點兩位數(單位％) |
| UpDownDay | 連續漲跌(天) | short | +：連續漲天數<br>–：連續跌天數 |
| BidQty | 第一買量 | int |  |
| AskQty | 第一賣量 | int |  |
| PriceTrends | 瞬間價格趨勢 | Byte | 10: 一般揭示<br>11: 暫緩撮合且瞬間趨跌<br>12: 暫緩撮合且瞬間趨漲<br>13: 試算後延後收盤<br>14: 暫停交易<br>15: 恢復交易 |
| EstDealPrice | 盤前揭露價 | double |  |
| EstDealVol | 盤前揭露量 | int |  |
| EstDealVolFlag | 盤前揭露量內外盤標記 | Byte | 0:內盤/1:外盤 |

### RR_RealReport

- 中文名稱：即時回報訂閱
- Function ID：3356101146
- 備註：登入即訂閱
- 來源：`RR_RealReport_IO_Spec.md`
- Service ID：RR_RealReport
- Service Desc：即時回報訂閱

#### RealReport 即時回報物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| RptType | 回報類別 | byte | 50:股票委託<br>51:股票成交<br>2:期貨委託<br>3:期貨成交<br>4:期貨價差成交回報<br>5:期貨委託減量取消<br>10:選擇權委託回報<br>11:單式成交回報<br>12:複式成交回報<br>13:選擇權減量取消回報<br>21:組合拆解回報<br>22:改變新/平倉回報<br>30:海外期貨委託<br>31:海外期貨成交 |
| OrderNo | 委託單號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| CompanyNo | 商品代碼 | string | 2854, 05311<br>FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| StkCName | 商品名稱 | string |  |
| OrderDate | 交易日 | TYuantaDate | 請參考API說明文件-物件 |
| OrderTime | 交易時間 | TYuantaTime | 請參考API說明文件-物件<br>委託時間/成交時間 |
| OrderType | 委託種類 | string | 現貨<br>0:普通<br>1,3:資<br>2,4:券<br>5,6:借券(賣出)<br>期權<br>M:市價<br>L:限價<br>P:範圍市價<br>海外期<br>LMT:限價單<br>MKT:市價單<br>STP:停損單<br>SWL:停損限價單<br>CXL:取消單 |
| BS | 買賣別 | string | S:賣<br>B:買 |
| Price | 價格 | double | 委託價 / 成交價<br>Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| TouchPrice | 停損執行價 | double |  |
| BeforeQty | 改量前數量 | Int |  |
| OrderQty | 數量 | Int | 委託股數 / 成交股數 |
| OpenOffsetKind | 新增/沖銷別 | String | 期<br>0:新增<br>1:沖銷<br>2:新倉且當日沖銷單<br>權<br>0: 新增<br>1: 沖銷 |
| DayTrade | 當沖記號 | String | 證券：' ' OR 'X'<br>期權：' ' OR 'Y' |
| OrderCond | 委託條件 | String | 證券<br>3:IOC<br>4:FOK<br>0:ROD<br>期權<br>F:FOK<br>I:IOC<br>R:ROD<br>海外期<br>0:DAY<br>2:IOC<br>1:FOK<br>N:非GTC單 |
| OrderErrorNo | 錯誤碼 | String | P201<br>證券錯誤碼改5碼，使用另一欄位 |
| TradeKind | 交易性質 | byte | 現貨<br>1:B<br>2:S<br>3:改量<br>4:取消<br>5:查詢<br>6:改價<br>9:交易所主動刪單<br>期權<br>1:新增<br>2:減量<br>3:取消<br>5:查詢<br>6:改價 |
| APCode | 委託類別 | byte | 現貨<br>0:現股<br>2:零股<br>4:盤中零股<br>7:盤後<br>99:興櫃<br>組合拆解回報<br>83:拆解<br>67:組合<br>改變新/平倉回報<br>83:新轉平<br>79:平轉新 |
| BasketNo | 一籃子下單編號 | String |  |
| OrderStatus | 狀態碼 | short | 0委託成功<br>1委託失敗<br>2取消成功<br>3取消失敗<br>4減量成功<br>5減量失敗<br>6查詢成功<br>7查詢失敗<br>8已成交<br>10組合成功<br>11拆解成功<br>12平轉新<br>13新轉平<br>18委託收到<br>19取消收到<br>20改價成功<br>21改價失敗<br>23取消成交<br>24委託失效<br>25價穩失效 |
| StkType1 | 屬性1 | Byte | Bit 1: 管理商品<br>Bit 2: 交易記號<br>Bit 3: 受益憑證<br>Bit 4: ETF商品<br>Bit 5: 權證記號<br>Bit 6: 特別股<br>Bit 7: 存託憑證<br>Bit 8: 外國股票 |
| StkType2 | 屬性2 | Byte | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: 保留 |
| BelongMarketNo | 所屬市場代碼 | Byte |  |
| BelongStkCode | 所屬股票代碼 | String |  |
| SeqNo | 成交序號 | Uint | For 股票,期貨成交單<br>(複委託,國際期 -&gt;０)<br>若OrderStatus =25且StkErrCode = 13051、19351，此欄位會帶入成交數量 |
| PriceType | 價格型態 | String | 只有證券使用<br>1:市價<br>2:限價<br>H:漲停<br>L:跌停<br>-:平盤 |
| StkErrorNo | 證券回報錯誤碼 | String | 證券回報錯誤碼 |

### RR_RealReportMerge

- 中文名稱：彙整的即時回報訂閱
- Function ID：3356101147
- 備註：登入即訂閱
- 來源：`RR_RealReportMerge_IO_Spec.md`
- Service ID：RR_RealReportMerge
- Service Desc：彙整的即時回報訂閱

#### RealReportMerge 即時回報彙總物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| RptType | 回報標記 | byte | 1:股票<br>2:期貨<br>3:選擇權<br>4:海外期貨<br>5:海外股票 |
| OrderNo | 委託單號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| CompanyNo | 商品代碼 | string | 2854, 05311<br>FITX 200709,<br>URO200709,<br>FIGTL7/C8,<br>TXO09000T7,<br>TXO08000/08100U7 |
| OrderDate | 交易日 | TYuantaDate | 請參考API說明文件-物件 |
| OrderTime | 委託時間 | TYuantaTime | 請參考API說明文件-物件 |
| OrderType | 委託種類 | string | 現貨<br>0:普通<br>1,3:資<br>2,4:券<br>5,6:借券(賣出)<br>期權<br>1:市價<br>2:限價<br>3:範圍市價<br>海外期<br>LMT:限價單<br>MKT:市價單<br>STP:停損單<br>SWL:停損限價單<br>CXL:取消單<br>海外股票<br>1:Market<br>2:Limit 限價單 |
| BS | 買賣別 | string | S:賣<br>B:買 |
| Price | 價格 | double | Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| TouchPrice | 停損執行價 | double |  |
| LastDealPrice | 最新成交價 | double | Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| AvgDealPrice | 成交均價 | double | Ex. 23.50,1.0585<br>0000125’23.5(海外期) |
| BeforeQty | 改量前數量 | Int |  |
| OrderQty | 委託股數 | Int | 股數/口數<br>(有效數量含成交) |
| OkQty | 成交股數 | Int | 股數/口數 |
| OpenOffsetKind | 新增/沖銷別 | string | 期<br>0:新增<br>1:沖銷<br>2:新倉且當日沖銷單<br>權<br>0: 新增<br>1: 沖銷<br>海外股票 (SettleType)<br>0:外幣<br>1:台幣 |
| DayTrade | 當沖記號 | string | 證券：' ' OR 'X'<br>期權：' ' OR 'Y' |
| OrderCond | 委託條件 | string | 證券<br>3:IOC<br>4:FOK<br>0:ROD<br>期權<br>F:FOK<br>I:IOC<br>R:ROD<br>海外期<br>0:DAY<br>2:IOC<br>1:FOK<br>N:非GTC單<br>海外股票<br>0:DAY<br>3:IOC<br>4:FOK |
| OrderErrorNo | 錯誤碼 | string | P201 |
| APCode | 委託類別 | byte | 現貨<br>0:現股<br>2:零股<br>4:盤中零股<br>7:盤後<br>99:興櫃 |
| OrderStatus | 狀態碼 | short | 0：傳輸中<br>5：預約單<br>10：委託失敗<br>20：委託成功<br>24：委託失效<br>25：價穩失效<br>30：取消 |
| LastOrderStatus | 最新一筆即回資料狀態 | Byte | 0:委託成功<br>1:委託失敗<br>2:取消成功<br>3:取消失敗<br>4:減量成功<br>5:減量失敗<br>6:查詢成功<br>7:查詢失敗<br>8:已成交<br>10:組合成功<br>11:拆解成功<br>12:平轉新<br>13:新轉平<br>18:委託收到<br>19:取消收到(國外股票)<br>20:改價成功<br>21:改價失敗<br>23:取消成交 (國外股票)<br>24:委託失效<br>25:價穩失效 |
| StkCName | 商品名稱 | string | 此欄位代表股票名稱;但是在期貨價差的CASE下,此欄位代表第二個商品的tradecode |
| TradeCode | 實體交易代號 | string | 當期貨價差時,此欄位代表第一個商品的tradecode |
| StrikePrice | 履約價 | double |  |
| BasketNo | 一籃子下單編號 | string |  |
| StkType1 | 屬性1 | Byte | Bit 1: 管理商品<br>Bit 2: 交易記號<br>Bit 3: 受益憑證<br>Bit 4: ETF商品<br>Bit 5: 權證記號<br>Bit 6: 特別股<br>Bit 7: 存託憑證<br>Bit 8: 外國股票 |
| StkType2 | 屬性2 | Byte | Bit 1: 可轉換公司債<br>Bit 2: 附認股權公司債<br>Bit 3: 警示股<br>Bit 4: 指數記號<br>Bit 5: 期貨<br>Bit 6: 個股選擇權<br>Bit 7: 指數選擇權<br>Bit 8: 保留 |
| BelongMarketNo | 所屬市場代碼 | Byte |  |
| BelongStkCode | 所屬股票代碼 | string |  |
| StkType | 價格型態 | string | 證券使用<br>1:市價<br>2:限價<br>H:漲停<br>L:跌停<br>-:平盤 |
| StkErrorNo | 證券回報錯誤碼 | string | 證券回報錯誤碼 |

### SubscribeWatchlistAll

- 中文名稱：行情報價表訂閱
- Function ID：1644840458
- 同規格涵蓋：UnSubscribeWatchlistAll
- 備註：訂閱
- 來源：`SubscribeWatchlistAll_IO_Spec.md`
- Service ID：API SubscribeWatchlistAll  API UnSubscribeWatchlistAll
- Service Desc：行情報價表訂閱  行情報價表解訂閱
- 呼叫簽名：`bool SubscribeWatchlistAll(LoginAcno, LstWatchlistAll, Lng)  bool UnSubscribeWatchlistAll(LoginAcno, LstWatchlistAll, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstWatchlistAll | 訂閱商品清單 | List&lt;WatchlistAll&gt; |  |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### WatchlistAll 行情報價表物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### WatchListAllResult 行情報價表訂閱回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | MarketNo+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| SeqNo | 序號 | Long | 090000000000<br>後八碼代表序號，前四碼代表時間 |
| IndexFlag | 索引值 | enumQuoteIndexType | 請參考API說明文件-列舉物件 |
| Value | 資料值 | double | 此值定義請參考IndexFlag<br>若IndexFlag=IndexFlag22、IndexFlag28、IndexFlag29則無值<br>IndexFlag=瞬間價格趨勢<br>10: 一般揭示<br>11: 暫緩撮合且瞬間趨跌<br>12: 暫緩撮合且瞬間趨漲<br>13: 試算後延後收盤<br>14: 暫停交易<br>15: 恢復交易<br>16: 試算後延後開盤<br>IndexFlag=交易狀態<br>0x00: 初始狀態<br>0x01: 收單階段<br>0x02: 不可刪單階段<br>0x03: 集合競價階段<br>IndexFlag=試撮量<br>最高位元的Bit,表示內/外盤的旗標,<br>0:內盤/1:外盤 |
| IndexFlag_22 | 訂閱報價表Flag22 | WatchListAll_Flag22 | IndexFlag=IndexFlag22才有值 |
| IndexFlag_28 | 訂閱報價表Flag28 | WatchListAll_Flag28 | IndexFlag=IndexFlag28才有值 |
| IndexFlag_29 | 訂閱報價表Flag29 | WatchListAll_Flag29 | IndexFlag=IndexFlag29才有值 |

#### WatchListAll_Flag22 訂閱報價表IndexFlag22物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| BuyVol | 第一買量 | Int |  |
| SellVol | 第一賣量 | Int |  |

#### WatchListAll_Flag28 訂閱報價表IndexFlag28物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| BuyPrice | 買價 | double | 市價買:999999999 |
| SellPrice | 賣價 | double | 市價賣:-999999999 |

#### WatchListAll_Flag29 訂閱報價表IndexFlag29物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Time | 時間 | TYuantaTime |  |
| TotalOutVol | 累計外盤量 | Int |  |
| TotalInVol | 累計內盤量 | Int |  |
| Deal | 成交價 | double |  |
| Vol | 單量 | Int | 最高位元的Bit，表示內/外盤的旗標，<br>0:內盤/1:外盤 |
| TotalVol | 總成交量 | Int | 海外期貨之現貨單位是千股 |
| TotalAmt | 總成交金額 | Int | 單位萬元 |

### SubscribeStockTick

- 中文名稱：分時明細訂閱
- Function ID：3523880970
- 同規格涵蓋：UnSubscribeStockTick
- 備註：訂閱
- 來源：`SubscribeStocktick_IO_Spec.md`
- Service ID：API SubscribeStockTick  API UnSubscribeStockTick
- Service Desc：分時明細訂閱  分時明細解訂閱
- 呼叫簽名：`bool SubscribeStockTick(LoginAcno, LstStocktick, Lng)  bool UnSubscribeStockTick(LoginAcno, LstStocktick, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstStocktick | 訂閱商品清單 | List&lt;Stocktick&gt; |  |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### Stocktick 分時明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### StockTickResult 分時明細回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | MarketNo+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| SerialNo | 序號 | int | 以股票代碼個別編序號,從1開始<br>-1代表商品清盤 |
| Time | 時間 | TYuantaTime | 請參考API說明文件-物件 |
| BuyPrice | 買價 | double | 當SerialNo=-1時,此欄位代表漲停價<br>市價買:999999999 |
| SellPrice | 賣價 | double | 當SerialNo=-1時,此欄位代表跌停價<br>市價賣:-999999999 |
| DealPrice | 成交價 | double | 當SerialNo=-1時,此欄位代表開盤參考價 |
| DealVol | 成交量 | Int | 海外期貨之現貨單位是千股 |
| InOutFlag | 內外盤註記 | Byte | 0:內盤<br>1:外盤<br>2:定價內盤<br>3:定價外盤<br>10:一般揭示<br>11:暫緩撮合且瞬間趨跌<br>12:暫緩撮合且瞬間趨漲<br>13:試算後延後收盤<br>14:暫停交易<br>15:恢復交易<br>註1：當是10,11,12,13時,只有市場碼與股票代碼有值,其餘的欄位皆是0<br>註2：當是14,15時,只有市場碼、股票代碼與時間有值,其餘的欄位皆是0 |
| Type | 明細類別 | Byte | 0:Normal |

### SubscribeFiveTickA

- 中文名稱：最佳五檔行情訂閱
- Function ID：3523886090
- 同規格涵蓋：UnSubscribeFiveTickA
- 備註：訂閱
- 來源：`SubscribeFiveTickA_IO_Spec.md`
- Service ID：API SubscribeFiveTickA  API UnSubscribeFiveTickA
- Service Desc：最佳五檔行情訂閱  最佳五檔行情解訂閱
- 呼叫簽名：`bool SubscribeFiveTickA(LoginAcno, LstFiveTickA, Lng)  bool UnSubscribeFiveTickA(LoginAcno, LstFiveTickA, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstFiveTickA | 訂閱商品清單 | List&lt;FiveTickA&gt; |  |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FiveTickA 最佳五檔行情物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### FiveTickAResult 最佳五檔行情回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | MarketNo+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| IndexFlag | 索引值 | enumQuoteFiveTickIndexType | 請參考API說明文件-列舉物件 |
| Value | 資料值 | double | 此值定義請參考IndexFlag<br>若IndexFlag=IndexFlag20、<br>IndexFlag21、IndexFlag42、<br>IndexFlag43、IndexFlag50、<br>IndexFlag51 則無值 |
| IndexFlag_20 | 五檔報價Flag20 | FiveTick_Flag20 | IndexFlag=IndexFlag20才有值 |
| IndexFlag_21 | 五檔報價Flag21 | FiveTick_Flag21 | IndexFlag=IndexFlag21才有值 |
| IndexFlag_42 | 五檔報價Flag42 | FiveTick_Flag42 | IndexFlag=IndexFlag42才有值 |
| IndexFlag_43 | 五檔報價Flag43 | FiveTick_Flag43 | IndexFlag=IndexFlag43才有值 |
| IndexFlag_50 | 五檔報價Flag50 | FiveTick_Flag50 | IndexFlag=IndexFlag50才有值 |
| IndexFlag_51 | 五檔報價Flag51 | FiveTick_Flag51 | IndexFlag=IndexFlag51才有值 |

#### FiveTick_Flag20 五檔報價IndexFlag20物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Price1 | 第一買價 | double |  |
| Price2 | 第二買價 | double |  |
| Price3 | 第三買價 | double |  |
| Price4 | 第四買價 | double |  |
| Price5 | 第五買價 | double |  |
| Vol1 | 第一買量 | Int |  |
| Vol2 | 第二買量 | Int |  |
| Vol3 | 第三買量 | Int |  |
| Vol4 | 第四買量 | Int |  |
| Vol5 | 第五買量 | Int |  |

#### FiveTick_Flag21 五檔報價IndexFlag21物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Price1 | 第一賣價 | double |  |
| Price2 | 第二賣價 | double |  |
| Price3 | 第三賣價 | double |  |
| Price4 | 第四賣價 | double |  |
| Price5 | 第五賣價 | double |  |
| Vol1 | 第一賣量 | Int |  |
| Vol2 | 第二賣量 | Int |  |
| Vol3 | 第三賣量 | Int |  |
| Vol4 | 第四賣量 | Int |  |
| Vol5 | 第五賣量 | Int |  |

#### FiveTick_Flag42 五檔報價IndexFlag42物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Price1 | 第六買價 | double |  |
| Price2 | 第七買價 | double |  |
| Price3 | 第八買價 | double |  |
| Price4 | 第九買價 | double |  |
| Price5 | 第十買價 | double |  |
| Vol1 | 第六買量 | Int |  |
| Vol2 | 第七買量 | Int |  |
| Vol3 | 第八買量 | Int |  |
| Vol4 | 第九買量 | Int |  |
| Vol5 | 第十買量 | Int |  |

#### FiveTick_Flag43 五檔報價IndexFlag43物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Price1 | 第六賣價 | double |  |
| Price2 | 第七賣價 | double |  |
| Price3 | 第八賣價 | double |  |
| Price4 | 第九賣價 | double |  |
| Price5 | 第十賣價 | double |  |
| Vol1 | 第六賣量 | Int |  |
| Vol2 | 第七賣量 | Int |  |
| Vol3 | 第八賣量 | Int |  |
| Vol4 | 第九賣量 | Int |  |
| Vol5 | 第十賣量 | Int |  |

#### FiveTick_Flag50 五檔報價IndexFlag50物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| BuyPrice1 | 第一買價 | double |  |
| BuyPrice2 | 第二買價 | double |  |
| BuyPrice3 | 第三買價 | double |  |
| BuyPrice4 | 第四買價 | double |  |
| BuyPrice5 | 第五買價 | double |  |
| BuyVol1 | 第一買量 | Int |  |
| BuyVol2 | 第二買量 | Int |  |
| BuyVol3 | 第三買量 | Int |  |
| BuyVol4 | 第四買量 | Int |  |
| BuyVol5 | 第五買量 | Int |  |
| SellPrice1 | 第一賣價 | double |  |
| SellPrice2 | 第二賣價 | double |  |
| SellPrice3 | 第三賣價 | double |  |
| SellPrice4 | 第四賣價 | double |  |
| SellPrice5 | 第五賣價 | double |  |
| SellVol1 | 第一賣量 | Int |  |
| SellVol2 | 第二賣量 | Int |  |
| SellVol3 | 第三賣量 | Int |  |
| SellVol4 | 第四賣量 | Int |  |
| SellVol5 | 第五賣量 | Int |  |

#### FiveTick_Flag51 五檔報價IndexFlag51物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| BuyPrice1 | 第六買價 | double |  |
| BuyPrice2 | 第七買價 | double |  |
| BuyPrice3 | 第八買價 | double |  |
| BuyPrice4 | 第九買價 | double |  |
| BuyPrice5 | 第十買價 | double |  |
| BuyVol1 | 第六買量 | Int |  |
| BuyVol2 | 第七買量 | Int |  |
| BuyVol3 | 第八買量 | Int |  |
| BuyVol4 | 第九買量 | Int |  |
| BuyVol5 | 第十買量 | Int |  |
| SellPrice1 | 第六賣價 | double |  |
| SellPrice2 | 第七賣價 | double |  |
| SellPrice3 | 第八賣價 | double |  |
| SellPrice4 | 第九賣價 | double |  |
| SellPrice5 | 第十賣價 | double |  |
| SellVol1 | 第六賣量 | Int |  |
| SellVol2 | 第七賣量 | Int |  |
| SellVol3 | 第八賣量 | Int |  |
| SellVol4 | 第九賣量 | Int |  |
| SellVol5 | 第十賣量 | Int |  |

### SubscribeWatchlist

- 中文名稱：行情報價表訂閱(指定欄位)
- Function ID：3523888651
- 同規格涵蓋：UnSubscribeWatchlist
- 備註：訂閱
- 來源：`SubscribeWatchlist_IO_Spec.md`
- Service ID：API SubscribeWatchlist  API UnSubscribeWatchlist
- Service Desc：行情報價表訂閱(指定欄位)  行情報價表解訂閱(指定欄位)
- 呼叫簽名：`bool SubscribeWatchlist(LoginAcno, LstWatchlist, Lng)  bool UnSubscribeWatchlist(LoginAcno, LstWatchlist, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstWatchlist | 訂閱商品清單 | List&lt;Watchlist&gt; |  |
| Lng | 語系 | enumLangType | 預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### Watchlist 行情報價表(指定欄位)物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| IndexFlag | 訂閱報價欄位 | enumQuoteIndexType | 請參考API說明文件-列舉物件 |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### WatchListResult 行情報價表訂閱(指定欄位)回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | IndexFlag+MarketNo<br>+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| IndexFlag | 索引值 | enumQuoteIndexType | 請參考API說明文件-列舉物件 |
| Value | 資料值 | double | 此值定義請參考IndexFlag<br>IndexFlag=買價<br>市價買:999999999<br>IndexFlag=賣價<br>市價賣:-999999999<br>IndexFlag=單量<br>最高位元的Bit,表示內/外盤的旗標,0-內盤/1-外盤<br>IndexFlag=delay一秒的成交價<br>海外股無此資料,請使用索引值=7的成交價<br>IndexFlag=瞬間價格趨勢<br>10:一般揭示<br>11:暫緩撮合且瞬間趨跌<br>12:暫緩撮合且瞬間趨漲<br>13:試算後延後收盤<br>14:暫停交易<br>15:恢復交易<br>16:試算後延後開盤<br>IndexFlag=交易狀態<br>0x00:初始狀態<br>0x01:收單階段<br>0x02:不可刪單階段<br>0x03:集合競價階段<br>IndexFlag=試撮量<br>最高位元的Bit,表示內/外盤的旗標,<br>0:內盤/1:外盤 |

### SubscribeMarketInformation

- 中文名稱：個股盤前資訊訂閱
- Function ID：3523954191
- 同規格涵蓋：UnSubscribeMarketInformation
- 備註：訂閱，特殊功能需申請權限
- 來源：`SubscribeMarketInformation_IO_Spec.md`
- Service ID：API SubscribeMarketInformation  API UnSubscribeMarketInformation
- Service Desc：個股盤前資訊訂閱  個股盤前資訊解訂閱
- 呼叫簽名：`bool SubscribeMarketInformation(LoginAcno, LstMarketInfo, Lng)  bool UnSubscribeMarketInformation(LoginAcno, LstMarketInfo, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstMarketInfo | 訂閱商品清單 | List&lt;MarketInformation&gt; |  |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### MarketInformation 個股盤前資訊物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### MarketInfoResult 個股盤前資訊回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | MarketNo+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| DealPrice | 成交價 | int |  |
| TickVol | 單量 | int | 最高位元的Bit，表示內/外盤的旗標<br>0:內盤/1:外盤 |
| Time | 時間 | TYuantaTime | 請參考API說明文件-物件 |
| TradeStatus | 交易狀態 | Byte | 0 : 初始狀態<br>1 : 收單階段<br>2 : 不可刪單階段<br>3 : 集合競價階段 |

### SubscribeStockInformation

- 中文名稱：個股其他資訊訂閱
- Function ID：3523954192
- 同規格涵蓋：UnSubscribeStockInformation
- 備註：訂閱，特殊功能需申請權限
- 來源：`SubscribeStockInformation_IO_Spec.md`
- Service ID：API SubscribeStockInformation  API UnSubscribeStockInformation
- Service Desc：個股其他資訊訂閱  個股其他資訊解訂閱
- 呼叫簽名：`bool SubscribeStockInformation(LoginAcno, LstStockInfo, Lng)  bool UnSubscribeStockInformation(LoginAcno, LstStockInfo, Lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 訂閱帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| LstStockInfo | 訂閱商品清單 | List&lt;StockOtherInformation&gt; |  |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StockOtherInformation 個股其他資訊物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### StockOtherInfoResult 個股其他資訊回傳結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Key | 鍵值 | string | MarketNo+StkCode (不足補0) |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代碼 | string |  |
| IndexFlag | 索引值 | enumQuoteStkInfoIndexType | 請參考API說明文件-列舉物件<br>僅提供試搓成交時間 |
| TradeTime | 試搓成交時間 | TYuantaTime | 請參考API說明文件-物件 |

### GetFutSprStore

- 中文名稱：期貨複式單庫存明細查詢
- Function ID：201032012
- 備註：帳務類發送，特殊功能需申請權限
- 來源：`GetFutSprStore_IO_Spec.md`
- Service ID：API GetFutSprStore
- Service Desc：期貨複式單庫存明細查詢
- 呼叫簽名：`bool GetFutSprStore(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| Lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FutSprStoreResult 查詢期貨複式單庫存明細結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| FutSprStoreList | 結果清單 | List&lt;FutSprStore&gt; |  |

#### FutSprStore 期貨複式單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| FutAccount | 帳號 | string |  |
| Trid | 商品代碼 | string | TX109100E4/TXO09000E4 |
| SeqNo | 流水號 | string | 流水號相同為同一複式單組合商品 |
| SprNum | 組合編號 | Short |  |
| BS | 買賣別 | string | B, S |
| CommodityID | 商品名稱 | string | TXO |
| CallPut | 買賣權 | string | C/P |
| SettlementMonth | 商品年月 | Int | 200708 |
| StrikePrice | 履約價 | double |  |
| Qty | 口數 | Short |  |
| TradeDate | 交易日期 | TYuantaDate | 請參考API說明文件-物件 |
| MatchPrice | 成交價 | double |  |
| StkName | 股票名稱 | string | Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’ |

### SendFutureApart

- 中文名稱：期貨複式單拆解
- Function ID：301002013
- 備註：交易類發送，特殊功能需申請權限
- 來源：`SendFutureApart_IO_Spec.md`
- Service ID：API SendFutureApart
- Service Desc：期貨複式單拆解
- 呼叫簽名：`bool SendFutureApart(LoginAcno, futureApart, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| LoginAcno | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT<br>註1 |
| lstFutSprStore | 拆解物件 | List&lt;FutSprStore&gt; | 註2 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### FutureApart 複式單拆解物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| FutAccount | 帳號 | string | 期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| TradeDate | 交易日期 | TYuantaDate | 請參考API說明文件-物件 |
| SeqNo | 流水號 | string |  |
| Trid | 商品代碼 | string | TX109100E4/TXO09000E4 |
| Qty | 口數 | Short |  |

#### FutureApartResult 複式單拆解結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultCount | 交易狀態 | OrderStatus |  |
| ResultList | 複式單拆解結果清單 | List&lt;FutureApartData&gt; |  |

#### OrderStatus 交易狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MsgCode | 訊息代碼 | string | 0001:執行成功 其它:失敗 |
| MsgContent | 訊息內容 | string |  |
| Count | 筆數 | Int |  |

#### FutureApartData 複式單拆解結果明細
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Identify | 識別碼 | Int |  |
| ReplyCode | 委託結果代碼 | Short | 0:委託成功 others:委託失敗 |
| ErrType | 錯誤類別 | string |  |
| ErrNO | 錯誤代號 | string |  |
| Advisory | 錯誤說明 | string |  |

### GetStockInformation

- 中文名稱：標的資訊查詢
- Function ID：20100027
- 備註：報價類發送
- 來源：`GetStockInformation_IO_Spec.md`
- Service ID：API GetStockInformation
- Service Desc：標的資訊查詢
- 呼叫簽名：`bool GetStockInformation(Account, StkList, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| StkList | 查詢商品清單 | List&lt;StkInfo&gt; |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StkInfo 標的資訊
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |

#### StkInformationResult 標的資訊查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| StockInformationList | 結果清單 | List&lt;StkInformation&gt; |  |

#### StkInformation 標的資訊物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |
| Dayoffmark | 可否當沖 | string | "X"：現股當沖<br>"Y"：現股當沖(暫停先賣後買)<br>其他：不可現股當沖 |
| Creditpercent | 融資成數 | int |  |
| Lendpercent | 融券成數 | int |  |
| Creditremnants | 融資餘額 | int | 999999：無限制<br>-1：停資<br>-2：有限制 |
| Lendremnants | 融券餘額 | int | 999999：無限制<br>-1：停券<br>0：無券 |
| LendSellMark | 平盤下可放空 | string | "N"：不可放空<br>"Y"：可放空 |
| RecallDate | 融券回補日期 | string | yyyyMMdd民國年 |
| LendQty | 借賣配額 | long |  |
| StockWarning | 股票警示狀態 | List&lt;enumStkWarningType&gt; | 請參考API說明文件-列舉物件 |
| UpdateDate | 更新日期 | string | yyyyMMdd民國年 |

### GetStkTickDetail

- 中文名稱：當日分時明細查詢
- Function ID：500012
- 備註：報價類發送
- 來源：`GetStkTickDetail_IO_Spec.md`
- Service ID：API GetStkTickDetail
- Service Desc：當日分時明細查詢
- 呼叫簽名：`bool GetStkTickDetail  (Account, MarketType, StkCode, SelectType, Stime, Etime, LastCount, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 商品代號 | string |  |
| SelectType | 查詢種類 | enumStkTickSelectType | 請參考API說明文件-列舉物件 |
| Stime | 開始時間 | string | 預設為00:00:00 |
| Etime | 結束時間 | string | 預設為23:59:59 |
| LastCount | 最後筆數 | int | 預設為20 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StickDetailResult 當日分時明細查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |
| StickDetailList | 結果清單 | List&lt;StickDetail&gt; |  |

#### StickDetail 當日分時明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| TimeStamp | 時間 | DateTime |  |
| DealPrice | 成交價 | double |  |
| DealVol | 成交量 | int |  |
| BuyPrice | 買價 | double |  |
| SellPrice | 賣價 | double |  |
| SeqNo | 序號 | int |  |
| InOutFlag | 內外盤 | int | 0:內盤<br>1:外盤 |

### GetStkClassifyPrice

- 中文名稱：分價量表查詢
- Function ID：500041
- 備註：報價類發送
- 來源：`GetStkClassifyPrice_IO_Spec.md`
- Service ID：API GetStkClassifyPrice
- Service Desc：分價量表查詢
- 呼叫簽名：`bool GetStkClassifyPrice(Account, MarketType, StkCode, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 商品代號 | string |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### StkClassifyPriceResult 分價量表查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Date | 日期 | string | yyyy/MM/dd |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |
| ClassifyPriceList | 結果清單 | List&lt;ClassifyPrice&gt; |  |

#### ClassifyPrice 分價量表物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Price | 成交價 | double |  |
| InDealVol | 內盤成交量 | int |  |
| OutDealVol | 外盤成交量 | int |  |
| TotalDealVol | 累計成交量 | int |  |

### GetUnrealizedGainLossDetail

- 中文名稱：未實現損益明細查詢
- Function ID：201031018
- 備註：帳務類發送
- 來源：`GetUnrealizedGainLossDetail_IO_Spec.md`
- Service ID：API GetUnrealizedGainLossDetail
- Service Desc：未實現損益明細查詢
- 呼叫簽名：`bool GetUnrealizedGainLossDetail(Account, MarketType, StkCode, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代號 | string |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### UnGainLossDetailResult 未實現損益明細結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| UnGainLossDetailList | 結果清單 | List&lt;UnGainLossDetail&gt; | 註2 |

#### UnGainLossDetail 未實現損益明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| TradeKind | 交易種類 | Int | 0:現股 <br>3:資買  <br>4:券賣 |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 股票代號 | string |  |
| StockQty | 股數 | Long |  |
| Price | 成交價 | double |  |
| TradeDate | 成交日 | string | yyyy/MM/dd |
| Cost | 持有成本 | double |  |
| Interest | 預估利息 | Long |  |
| ReturnAmt | 未實現損益 | double |  |
| MarketAmt | 股票市值 | double | 股數*市價 |

### GetHisRealizedGainLoss

- 中文名稱：已實現損益查詢
- Function ID：201021011
- 備註：帳務類發送
- 來源：`GetHisRealizedGainLoss_IO_Spec.md`
- Service ID：API GetHisRealizedGainLoss
- Service Desc：已實現損益查詢
- 呼叫簽名：`bool GetHisRealizedGainLoss(Account, SDate, EDate, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| SDate | 查詢起始日 | string | yyyy/MM/dd<br>註2 |
| EDate | 查詢結束日 | string | yyyy/MM/dd<br>註2 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### RealizedGainLossResult 已實現損益查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| RealizedGainLossList | 結果清單 | List&lt;RealizedGainLoss&gt; |  |

#### RealizedGainLoss 已實現損益物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StkCode | 商品代碼 | string |  |
| TradeDate | 成交日 | string | yyyy/MM/dd |
| TradeKind | 交易種類 | int | '0' 現股<br>'1' 代資<br>'2' 代券<br>'3'融資<br>'4' 融券<br>'5','6' 借券<br>7:資沖<br>8:券沖<br>17:現股當沖買<br>18:現股當沖賣 |
| Price | 成交價 | double |  |
| Qty | 成交股數 | int |  |
| ProfitLoss | 損益 | int |  |
| OrderNo | 委託單號 | string |  |
| TermSplit | 委託書號分單號 | int |  |
| TermExt | 委託書號延長碼 | string |  |
| Charge | 手續費 | int |  |
| Cost | 持有成本 | int |  |
| Tax | 交易稅 | int |  |
| TotalAMT | 成交價金 | int |  |

### GetStkHistoryReportReversal

- 中文名稱：沖銷明細查詢
- Function ID：201021025
- 備註：帳務類發送
- 來源：`GetStkHistoryReportReversal_IO_Spec.md`
- Service ID：API GetStkHistoryReportReversal
- Service Desc：沖銷明細查詢
- 呼叫簽名：`bool GetStkHistoryReportReversal(Account, ReGainLoss, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| ReGainLoss | 已實現損益 | RealizedGainLoss | 註2 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### ReversalReportResult 沖銷明細查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ReversalReportList | 結果清單 | List&lt;ReversalReport&gt; |  |

#### ReversalReport 沖銷明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| ReversalDate | 被沖抵成交日 | string | yyyy/MM/dd |
| ReversalPrice | 被沖抵成交價 | double |  |
| ReversalQty | 被沖抵股數 | long |  |
| GlAmt | 沖抵損益 | double |  |

### GetStkTransactionOutlay

- 中文名稱：現貨交割款查詢(台幣)
- Function ID：201041010
- 備註：帳務類發送
- 來源：`GetStkTransactionOutlay_IO_Spec.md`
- Service ID：API GetStkTransactionOutlay
- Service Desc：交割款查詢(台幣)
- 呼叫簽名：`bool GetStkTransactionOutlay(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### ReversalReportResult 交割款查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| TransactionOutlayList | 結果清單 | List&lt;TransactionOutlay&gt; | 註2 |

#### TransactionOutlay 交割款物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| SettlementDay | 交割日期 | string | yyyy/MM/dd |
| SettlementAmt | 交割金額 | double |  |

### GetBankBalance

- 中文名稱：銀行餘額查詢
- Function ID：201041014
- 備註：帳務類發送
- 來源：`GetBankBalance_IO_Spec.md`
- Service ID：API GetBankBalance
- Service Desc：銀行餘額查詢
- 呼叫簽名：`bool GetBankBalance(Account, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### BankBalanceResult 銀行餘額查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| BankBalanceList | 結果清單 | List&lt;BankBalance&gt; |  |

#### BankBalance 銀行餘額物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| ResponseTime | 系統回覆時間 | string | HH:mm:ss |
| BankAccount | 銀行帳號 | string |  |
| AvailableBalance | 可用餘額 | double |  |
| Message | 說明 | string | 異常訊息 |

### SendAlgoCOOdrStrategy

- 中文名稱：新增條件單
- Function ID：100002
- 備註：交易類發送
- 來源：`SendAlgoCOOdrStrategy.md`
- Service ID：API SendAlgoCOOdrStrategy
- Service Desc：新增條件單
- 呼叫簽名：`bool SendAlgoCOOdrStrategy(Account, lstStrategy, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註：僅可使用證券帳號 |
| lstStrategy | 條件單物件清單 | List&lt;STOStrategy&gt;,<br>List&lt;MLPStrategy&gt;,<br>List&lt;OCOStrategy&gt;,<br>List&lt;SpiderStrategy&gt;,<br>List&lt;MS_SpiderStrategy&gt;,<br>List&lt;MS_DayTradeSpiderStrategy&gt; | STOStrategy 停損利<br>MLPStrategy 移動鎖利<br>OCOStrategy 二擇一<br>SpiderStrategy 多條件<br>MS_SpiderStrategy 母子單<br>MS_DayTradeSpiderStrategy 當沖母子單<br>註：單次僅能同策略 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### STOStrategy 停損利單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| ExpTime | 策略終止日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| Order | 下單方式 | StrategyOrder1 | 請參考API說明文件-列舉物件 |
| StrategySettings | 條件設定 | StrategySettings |  |
| OrderSettings | 下單設定 | OrderSettings1&lt;OrderType1,OrderPriceType1&gt; | 僅提供庫存賣出 |

#### MLPStrategy 移動鎖利單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| ExpTime | 策略終止日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| Order | 下單方式 | StrategyOrder1 | 請參考API說明文件-列舉物件 |
| StrategySettings | 條件設定 | MLPStrategySettings |  |
| OrderSettings | 下單設定 | OrderSettings1&lt;OrderType1,OrderPriceType2&gt; |  |

#### OCOStrategy 二擇一單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| ExpTime | 策略終止日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| Order | 下單方式 | StrategyOrder1 | 請參考API說明文件-列舉物件<br>限輸入:成交就停、觸發就停 |
| StrategySettings1 | 條件1條件設定 | StrategySettings | 條件1與條件2 商品需一致 |
| StrategySettings2 | 條件2條件設定 | StrategySettings | 條件1與條件2 商品需一致 |
| OrderSettings1 | 條件1下單設定 | OrderSettings2&lt;OrderType2, OrderPriceType1&gt; |  |
| OrderSettings2 | 條件2下單設定 | OrderSettings2&lt;OrderType2, OrderPriceType1&gt; |  |

#### SpiderStrategy 多條件單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| ExpTime | 策略終止日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| Order | 下單方式 | StrategyOrder1 | 請參考API說明文件-列舉物件 |
| Settings | 設定 | SpiderSettings |  |

#### MS_SpiderStrategy 母子單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| ExpTime | 策略終止日 | DateTime | 盤中區間限制:當日~90天內<br>盤後區間限制:下一交易日~90天內 |
| Order | 下單方式 | StrategyOrder2 | 請參考API說明文件-列舉物件<br>限選交易到設定單位全部成交 |
| DayTrade | 是否當沖 | bool | 固定false |
| M_SpiderStrategy | 母單設定 | SpiderSettings |  |
| S_SpiderStrategy | 子單設定 | SpiderSettings |  |

#### MS_DayTradeSpiderStrategy 當沖母子單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| EffTime | 策略起始日 | DateTime | 盤中限填當日(僅當日有效)<br>盤後限填下一交易日(僅下一交易日當日有效) |
| ExpTime | 策略終止日 | DateTime | 盤中限填當日(僅當日有效)<br>盤後限填下一交易日(僅下一交易日當日有效) |
| Order | 下單方式 | StrategyOrder2 | 請參考API說明文件-列舉物件<br>限選母單成交子單就立即下單 |
| DayTrade | 是否當沖 | bool | 固定true |
| M_SpiderStrategy | 母單設定 | DayTradeSpiderSettings |  |
| OrderSettings | 子單下單設定 | OrderSettings2&lt;OrderType3, OrderPriceType1&gt; | 僅提供母單反向 |
| MarketType | 市場類別 | enumMarketType | 僅支援上市、上櫃商品 |
| StkCode | 商品代號 | string |  |
| Condition | 條件種類 | StrategyCondition1 | 請參考API說明文件-列舉物件 |
| Direction | 條件方向 | int | 1:大於等於<br>2:小於等於(成交價才可使用) |
| Value | 條件數值 | double | 限制：<br>成交價(開盤參考價x0.7~1.7倍)<br>總量(單位:張)<br>當日漲跌幅(0.01~10)% |
| MarketType | 市場類別 | enumMarketType | 僅支援上市、上櫃商品 |
| StkCode | 商品代號 | string |  |
| Price | 基準價 | double | 限制：開盤參考價x0.7~1.7倍 |
| Pullback_Uint | 區間高點回檔單位 | int | 1:百分比<br>2:元 |
| Pullback_Value | 區間高點回檔數值 | double | 百分比:0.1~100%<br>元:0.01&lt;=設定值&lt;=開盤參考價 |

#### OrderSettings1<T,T1> 下單設定1
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| OrderType | 委託種類 | T | 停損利、移動鎖利:OrderType1<br>請參考API說明文件-列舉物件 |
| TimeInforce | 委託時間效期 | int | 0:ROD<br>3:IOC<br>4:FOK |
| PriceType | 委託價格種類 | T1 | 停損利:OrderPriceType1<br>移動鎖利:OrderPriceType2<br>請參考API說明文件-列舉物件 |
| OrderValue | 委託數值 | double | 非限價、成交價請填0<br>限制:<br>限價(開盤參考價x0.7~1.7倍)<br>成交價(+-0~8)tick |
| OrderQty | 委託單位 | int | 張 |

#### OrderSettings2<T,T1> 下單設定2
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| MarketType | 市場類別 | enumMarketType | 僅支援上市、上櫃商品 |
| StkCode | 商品代號 | string |  |
| OrderType | 委託種類 | T | 二擇一、多條件、母子單:OrderType2<br>當沖母子單:OrderType3<br>請參考API說明文件-列舉物件 |
| TimeInforce | 委託時間效期 | int | 0:ROD<br>3:IOC<br>4:FOK |
| PriceType | 委託價格種類 | T1 | OrderPriceType1<br>請參考API說明文件-列舉物件 |
| OrderValue | 委託數值 | double | 非限價、成交價請填0<br>限制:<br>限價(開盤參考價x0.7~1.7倍)<br>成交價(+-0~8)tick |
| OrderQty | 委託單位 | int | 張 |
| lstSettings | 條件設定 | List&lt;SpiderStrategySettings&gt; | *最多8個、不得為0個<br>*同商品同種類同方向不可重複<br>*當全部符合:同商品漲與跌不可同時設定<br>1.當日漲幅、當日跌幅不可同時設定<br>2.總漲幅、總跌幅不可同時設定<br>3.當日漲停、當日跌停不可同時設定<br>4.當日上漲、當日下跌不可同時設定 |
| OrderSettings | 下單設定 | OrderSettings2&lt;OrderType2, OrderPriceType1&gt; |  |
| Eligible | 符合條件 | int | 1:擇一符合<br>2:全部符合 |
| lstSettings | 條件設定 | List&lt;SpiderStrategySettings&gt; | *最多8個、不得為0個<br>*同商品同種類同方向不可重複<br>*當全部符合:同商品漲與跌不可同時設定<br>1.當日漲幅、當日跌幅不可同時設定<br>2.總漲幅、總跌幅不可同時設定<br>3.當日漲停、當日跌停不可同時設定<br>4.當日上漲、當日下跌不可同時設定 |
| OrderSettings | 下單設定 | OrderSettings2&lt;OrderType3, OrderPriceType1&gt; |  |
| Eligible | 符合條件 | int | 1:擇一符合<br>2:全部符合 |
| MarketType | 市場類別 | enumMarketType | 僅支援上市、上櫃商品 |
| StkCode | 商品代號 | string |  |
| StrategyConditions | 條件種類 | StrategyCondition2 | 請參考API說明文件-列舉物件 |
| Direction | 條件方向 | int | 1:大於等於<br>2:小於等於(成交價才可使用)<br>3:無(漲停或跌停) |
| Price | 基準價 | double | 條件種類非總漲幅、總跌幅填0<br>限制:開盤參考價0.7~1.7倍 |
| Value | 條件數值 | double | 當日漲停、當日跌停填0<br>限制:<br>成交價(現價0.7~1.7倍)<br>總量(單位:張)<br>當日漲跌幅(0.01~10)%<br>總漲跌幅(0.01~100)%<br>當日上漲下跌(0.01~9999) |

#### OrderStrategyResult 條件單委託結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultList | 條件單委託結果清單 | List&lt;OrderStrategyStatus&gt; |  |

#### OrderStrategyStatus 條件單委託狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| OrdStatus | 委託狀態 | SStatus | 請參考API說明文件-列舉物件 |
| OrderNo | 委託編號 | String |  |
| EffTime | 策略起始日 | DateTime |  |
| ExpTime | 策略終止日 | DateTime |  |
| Msg | 訊息中文 | string |  |

### GetConditionStrategy

- 中文名稱：有效策略查詢
- Function ID：100003
- 備註：交易類發送
- 來源：`GetConditionStrategy_IO_Spec.md`
- Service ID：API GetConditionStrategy
- Service Desc：有效策略查詢
- 呼叫簽名：`bool GetConditionStrategy(Account, StrategyType, StkCode, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| StrategyType | 策略類型 | int | 1:停損利<br>2:移動鎖利<br>3:二擇一<br>4:母子單<br>5:多條件<br>6.全部 |
| StkCode | 商品代號 | string | 預設為空字串<br>空字串則全查 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### ConditionStrategyResult 有效策略查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ConditionStrategyList | 結果清單 | List&lt;ConditionStrategy&gt; |  |

#### ConditionStrategy 有效策略結果物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| StrategyType | 策略類型 | StrategyType | 請參考API說明文件-列舉物件 |
| StrategyNo | 策略編號 | string |  |
| OrdDateTime | 設定日期 | DateTime |  |
| StrategyStatus | 條件單狀態 | SStatus | 請參考API說明文件-列舉物件 |
| OrdStatus | 委託狀態 | string |  |
| MarketType | 市場別 | string |  |
| StkCode | 委託商品代號 | string |  |
| Condition | 條件設定 | string | 母子單/多條件詳細條件，請至明細查詢 |
| OrderKind | 委託買賣種類 | string | 委託種類+買賣別+委託時效 |
| Price | 下單價格 | string |  |
| OrderQty | 設定股數 | long |  |
| DealQty | 成交股數 | long |  |
| RestQty | 剩餘股數 | long |  |
| SDate | 有效期限(起日) | string | yyyy/MM/dd |
| EDate | 有效期限(迄日) | string | yyyy/MM/dd |
| OrderTypeMsg | 下單方式 | string |  |
| HighPx | 區間高點 | double | 僅移動鎖利用，預設0 |
| TriggerPx | 觸發價格 | string | 僅停損利、移動鎖利、二擇一用<br>其他單別顯示-- |
| DetailList | 查詢明細清單 | List&lt;ConditionStrategyDetail&gt; |  |

#### ConditionStrategyDetail 查詢明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| DealTime | 成交時間 | string | yyyy/MM/dd |
| OrderPrice | 委託價格 | string |  |
| AveragePrice | 成交均價 | double |  |
| DealQty | 成交股數 | long |  |
| Memo | 備註 | string |  |
| TrigTime | 觸發時間 | string | HH:mm<br>僅母子單、多條件用<br>其他單別顯示-- |
| TrigCondition | 觸發條件 | string | 僅母子單、多條件用<br>其他單別顯示-- |

### GetHisConditionStrategy

- 中文名稱：歷史策略查詢
- Function ID：100004
- 備註：交易類發送
- 來源：`GetHisConditionStrategy_IO_Spec.md`
- Service ID：API GetHisConditionStrategy
- Service Desc：歷史策略查詢
- 呼叫簽名：`bool GetHisConditionStrategy(Account, StrategyType, StkCode, sDate, EDate, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| StrategyType | 策略類型 | int | 1:停損利<br>2:移動鎖利<br>3:二擇一<br>4:母子單<br>5:多條件<br>6.全部 |
| StkCode | 商品代號 | string | 預設為空字串<br>空字串則全查 |
| SDate | 起始日 | string | yyyy/MM/dd |
| EDate | 終止日 | string | yyyy/MM/dd |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### HisConditionStrategyResult 歷史策略查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| HisConditionStrategyList | 結果清單 | List&lt;HisConditionStrategy&gt; |  |

#### HisConditionStrategy 歷史策略結果物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string |  |
| StrategyType | 策略類型 | StrategyType | 請參考API說明文件-列舉物件 |
| StrategyNo | 策略編號 | string |  |
| OrdDateTime | 設定日期 | DateTime |  |
| TermiateDate | 結束日期 | string | yyyy/MM/dd |
| CancelDate | 刪除時間 | string | yyyy/MM/dd HH:mm |
| StrategyStatus | 條件單狀態 | SStatus | 請參考API說明文件-列舉物件 |
| OrdStatus | 委託狀態 | string |  |
| MarketType | 市場別 | string |  |
| StkCode | 委託商品代號 | string |  |
| Condition | 條件設定 | string | 母子單/多條件詳細條件，請至明細查詢 |
| OrderKind | 委託買賣種類 | string | 委託種類+買賣別+委託時效 |
| Price | 下單價格 | string |  |
| OrderQty | 設定股數 | long |  |
| DealQty | 成交股數 | long |  |
| RestQty | 剩餘股數 | long |  |
| SDate | 有效期限(起日) | string | yyyy/MM/dd |
| EDate | 有效期限(迄日) | string | yyyy/MM/dd |
| OrderTypeMsg | 下單方式 | string |  |
| HighPx | 區間高點 | double | 僅移動鎖利用，預設0 |
| TriggerPx | 觸發價格 | string | 僅停損利、移動鎖利、二擇一用<br>其他單別顯示-- |
| DetailList | 查詢明細清單 | List&lt;ConditionStrategyDetail&gt; |  |

#### ConditionStrategyDetail 查詢明細物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| DealTime | 成交時間 | string | yyyy/MM/dd |
| OrderPrice | 委託價格 | string |  |
| AveragePrice | 成交均價 | double |  |
| DealQty | 成交股數 | long |  |
| Memo | 備註 | string |  |
| TrigTime | 觸發時間 | string | HH:mm<br>僅母子單、多條件用<br>其他單別顯示-- |
| TrigCondition | 觸發條件 | string | 僅母子單、多條件用<br>其他單別顯示-- |

### DeleteAlgoCOOdrStrategy

- 中文名稱：刪除條件單
- Function ID：100005
- 備註：交易類發送
- 來源：`DeleteAlgoCOOdrStrategy.md`
- Service ID：API DeleteAlgoCOOdrStrategy
- Service Desc：刪除條件單
- 呼叫簽名：`bool DeleteAlgoCOOdrStrategy(Account, lstStrategy, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>註1 |
| lstStrategy | 刪除清單 | List&lt;DeleteStrategy&gt; |  |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### DeleteStrategy 刪除條件單物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7 |
| StrategyType | 策略類型 | StrategyType | 請參考API說明文件-列舉物件 |
| StrategyNo | 策略編號 | string |  |

#### OrderStrategyResult 條件單委託結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| ResultList | 條件單委託結果清單 | List&lt;OrderStrategyStatus&gt; |  |

#### OrderStrategyStatus 條件單委託狀態
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| OrdStatus | 委託狀態 | SStatus | 請參考API說明文件-列舉物件 |
| OrderNo | 委託編號 | String |  |
| EffTime | 策略起始日 | DateTime |  |
| ExpTime | 策略終止日 | DateTime |  |
| Msg | 訊息中文 | string |  |

### GetKLine

- 中文名稱：K線查詢
- Function ID：500017
- 備註：報價類發送
- 來源：`GetKLine_IO_Spec.md`
- Service ID：API GetKLine
- Service Desc：K線查詢
- 呼叫簽名：`bool GetKLine  (Account, KLineType, MarketType, StkCode , SDate, EDate, lng)`

#### Input Spec Table
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| Account | 帳號 | string | 證券:S+分公司代號(4)+帳號(7)<br>例如 S_BRANCH4_ACCOUNT7<br>期貨:F + 固定F021013 + 分公司BRANCH + 帳號ACCOUNT<br>例如 F_F021013_BRANCH_ACCOUNT |
| KLineType | K線周期 | KLineType | 請參考API說明文件-列舉物件 |
| MarketType | 市場類別 | enumMarketType | 請參考API說明文件-列舉物件<br>註1 |
| StkCode | 商品代號 | string |  |
| Sdate | 開始時間 | string | yyyy/MM/dd<br>註2 |
| Edate | 結束時間 | string | yyyy/MM/dd<br>註2 |
| lng | 語系 | enumLangType | 請參考API說明文件-列舉物件<br>預設為Normal<br>Normal:Big5<br>UTF8:UTF8<br>SC:簡體中文 |

#### KLineResult K線查詢結果
| Field Name | Description | Type | Memo |
| --- | --- | --- | --- |
| MarketNo | 市場代碼 | enumMarketType | 請參考API說明文件-列舉物件 |
| StockCode | 商品代碼 | string |  |
| KLineList | 結果清單 | List&lt; KLine&gt; |  |

#### Kline K線物件
| 欄位 | 說明 | 型別 | 備註 |
| --- | --- | --- | --- |
| TimeStamp | 時間戳記 | DateTime |  |
| OpenPrice | 開盤價 | double |  |
| HighPrice | 最高價 | double |  |
| LowPrice | 最低價 | double |  |
| ClosePrice | 收盤價 | double |  |
| DealVol | 成交量 | int |  |

## 附錄：即時回報情境

下表保留 FunctionList 內的情境範例；第二列原本是欄位中文說明，已合併進表格前提示。

| 欄位 | 中文說明 |
| --- | --- |
| 情境編號 |  |
| 即時回報情境說明 |  |
| bytRptType | 委託回報別 |
| abyOrderNo | 委託書號 |
| intBeforeQty | 委託前數量 |
| intOrderQty | 委託數量 |
| abyPrice | 委託價 |
| abyOrderCond | 委託條件 |
| bytTradeKind | 交易性質 |
| byOrderStatus | 即回資料狀態 |
| abyPriceType | 價格型態 |
| abyStkErrCode | 證券回報錯誤碼 |

| 情境編號 | 即時回報情境說明 | bytRptType | abyOrderNo | intBeforeQty | intOrderQty | abyPrice | abyOrderCond | bytTradeKind | byOrderStatus | abyPriceType | abyStkErrCode |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 情境1 | 限價、ROD、 委託5張、無成交 | 50 | f0001 | 0 | 5000 | 10 | 0 | 1 | 0 | 2 | 00000 |
|  | 改量1張 | 50 | f0001 | 5000 | 1000 | 10 | 0 | 3 | 4 | 2 | 00000 |
|  | 刪單 | 50 | f0001 | 4000 | 4000 | 10 | 0 | 4 | 4 | 2 | 00000 |
| 情境2 | 限價、ROD、 委託5張、部分成交1張 | 50 | f0002 | 0 | 5000 | 10 | 0 | 1 | 0 | 2 | 00000 |
|  | 成交回報1張 | 51 | f0002 | 0 | 1000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
|  | 改量1張、剩餘3張、已成交1張 | 50 | f0002 | 5000 | 1000 | 10 | 0 | 3 | 4 | 2 | 00000 |
|  | 改價 | 50 | f0002 | 4000 | 4000 | 11 | 0 | 3 | 6 | 2 | 00000 |
|  | 改量2張、剩餘1張、已成交1張 | 50 | f0002 | 4000 | 2000 | 11 | 0 | 3 | 4 | 2 | 00000 |
|  | 改價 | 50 | f0002 | 2000 | 2000 | 12 | 0 | 3 | 6 | 2 | 00000 |
|  | 刪單 | 50 | f0002 | 2000 | 1000 | 12 | 0 | 3 | 4 | 2 | 00000 |
| 情境3 | 市價、ROD、委託5張、價穩失效 | 50 | f0003 | 0 | 5000 | 10 | 0 | 1 | 25 | 1 | 上市：13052<br>上櫃：19352 |
| 情境4 | 市價、ROD、委託5張、成交1張 | 50 | f0004 | 0 | 5000 | 10 | 0 | 1 | 0 | 1 | 00000 |
|  | 成交回報1張 | 51 | f0004 | 0 | 1000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
|  | 交易所主動刪單 | 50 | f0004 | 4000 | 4000 | 10 | 0 | 9 | 25 | 1 | 上市：13000<br>上櫃：19300 |
| 情境5 | 市價、ROD、委託5張、成交1張、剩餘價穩失效 | 50 | f0005 | 0 | 1000 | 10 | 0 | 1 | 25 | 1 | 上市：13051<br>上櫃：19351 |
|  |  | 51 | f0005 | 0 | 1000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
| 情境6 | 市價、IOC、委託5張、未成交 | 50 | f0006 | 0 | 5000 | 10 | 3 | 1 | 24 | 1 | 上市：13048<br>上櫃：19348 |
| 情境7 | 市價、IOC、委託5張、未成交、價穩失效 | 50 | f0007 | 0 | 5000 | 10 | 3 | 1 | 25 | 1 | 上市：13052<br>上櫃：19352 |
| 情境8 | 市價、IOC、委託5張、成交1張，剩餘未成交 | 50 | f0008 | 0 | 5000 | 10 | 3 | 1 | 0 | 1 | 上市：13031<br>上櫃：19331 |
|  | 成交回報1張 | 51 | f0008 | 0 | 1000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
| 情境9 | 市價、IOC、委託5張、成交1張，剩餘價穩失效 | 50 | f0009 | 0 | 5000 | 10 | 3 | 1 | 25 | 1 | 上市：13051<br>上櫃：19351 |
|  | 成交回報1張 | 51 | f0009 | 0 | 1000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
| 情境10 | 市價、IOC、委託5張、完全成交 | 50 | f0010 | 0 | 5000 | 10 | 3 | 1 | 0 | 1 | 00000 |
|  | 成交回報5張 | 51 | f0010 | 0 | 5000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |
| 情境11 | 市價、FOK、委託5張、未成交 | 50 | f0011 | 0 | 5000 | 10 | 4 | 1 | 24 | 1 | 上市：13048<br>上櫃：19348 |
| 情境12 | 市價、FOK、委託5張、價穩失效 | 50 | f0012 | 0 | 5000 | 10 | 4 | 1 | 25 | 1 | 上市：13052<br>上櫃：19352 |
| 情境13 | 市價、FOK、委託5張、完全成交 | 50 | f0013 | 0 | 5000 | 10 | 4 | 1 | 0 | 1 | 00000 |
|  | 成交回報5張 | 51 | f0013 | 0 | 5000 | 10 | 成交回報未設值 | 成交回報未設值 | 8 | 成交回報未設值 | 成交回報未設值 |

## 附錄：現貨下單常用錯誤碼

此為現貨下單常用錯誤代碼對照表，若有不在此表的錯誤代碼，請開啟看盤軟體查看，或透過GetOrderTradeReport委託成交綜合回報查詢

| 錯誤代碼 | 錯誤代碼中文 |
| --- | --- |
| 00000興 | 委託成功 |
| 00001興 | 委託資料有誤,請檢查後重新委託 |
| 00002 | 委託失敗，請洽營業員 |
| 00005興 | 委託資料有誤,請檢查後重新委託 |
| 00009 | 委託失敗，請洽營業員 |
| 00010興 | 委託股數錯誤,請檢查並更正 |
| 00014興 | 無該委託單,請檢查該委託是否已成交 |
| 00015興 | 該股票外資額度已滿 |
| 00016 | 委託失敗，議價券商資料有誤 |
| 00017興 | 帳號錯誤,請檢查並更正 |
| 00018興 | 委託類別錯誤，請重新輸入 |
| 00019興 | 已超過委託時間 |
| 00020 | 委託失敗，請洽營業員 |
| 00026 | 委託失敗，請洽營業員 |
| 00027 | 委託失敗，請洽營業員 |
| 00029 | 委託失敗，請洽營業員 |
| 00030興 | 委託單價錯誤,請檢查並更正 |
| 00031興 | 買賣別錯誤,請檢查並更正 |
| 00032 | 委託失敗，請洽營業員 |
| 00033 | 委託失敗，請洽營業員 |
| 00034 | 委託失敗，議價券商資料有誤 |
| 00036 | 委託失敗，議價券商資料有誤 |
| 00044 | 此帳號只可賣出；如有問題請洽業務員 |
| 00058 | 該股票不許外資交易 |
| 00059 | 委託單價格錯誤 |
| 00059興 | 委託單價錯誤,請檢查並更正 |
| 00088 | 本日成交均價與前日價差達50%以上,櫃買已設停止交易 |
| 00095 | 委託單價格錯誤 |
| 00101 | 股票暫停交易，全日不接受委託 |
| 00103 | 委託失敗，委託價格與控管基準價差距達30%以上 |
| 01603 | 此股票已暫停交易 |
| 01839 | 此商品無借券資格 |
| 01840 | 今日該股出借張數大於昨日庫存 |
| 01841 | 該委託有還券張數尚在處理中，請確認還券是否成功後再執行 |
| 01842 | 授信額度不足 |
| 01843 | 授信額度不足 |
| 01845 | 股票代號或名稱錯誤 |
| 01848 | 此筆還券請洽分公司業務員辦理 |
| 01850 | 授信額度不足 |
| 04004 | 風控擔保金/品，查無相對應之借券資料 |
| 12022 | 委託失敗；此股票暫停交易 |
| 12244 | 查無此筆委託資料；如有問題請洽業務員 |
| 13000 | 委託成功 |
| 13001 | 已超過委託時間 |
| 13002 | 時間未到,稍待再輸入委託 |
| 13003 | 取消或改量失敗,交易正在處理中,稍待再重新進行 |
| 13004 | 取消或改量失敗,交易正在處理中,稍待再輸入委託 |
| 13005 | 無該委託單,請檢查該委託是否已成交 |
| 13011 | 委託資料有誤,請檢查後重新委託 |
| 13012 | 委託資料有誤,請檢查後重新委託 |
| 13013 | 委託資料有誤,請檢查後重新委託 |
| 13014 | 帳號錯誤,請檢查並更正 |
| 13015 | 委託資料有誤,請檢查後重新委託 |
| 13016 | 委託資料有誤,請檢查後重新委託 |
| 13018 | 委託資料有誤,請檢查後重新委託 |
| 13019 | 檢查並更正下單類別註記 |
| 13020 | 股票代號錯誤,請檢查並更正 |
| 13021 | 委託單價錯誤,請檢查並更正 |
| 13022 | 委託張數錯誤.請檢查並更正 |
| 13024 | 買賣別錯誤,請檢查並更正 |
| 13025 | 委託下單種類錯誤,請檢查並更正 |
| 13026 | 交易別錯誤,請檢查並更正 |
| 13027 | 該股票不許自營商交易 |
| 13028 | 該股票不許外資交易 |
| 13029 | 委託種類錯誤,請檢查並更正 |
| 13030 | 外資買進或借券賣出已無委託額度 |
| 13031 | 部分成交；剩餘數量被取消 |
| 13032 | 取消數量超過原有數量 |
| 13033 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 13034 | 颱風地區證券商不得交易 |
| 13035 | 委託張數錯誤,請檢查並更正 |
| 13036 | 委託張數錯誤,請檢查並更正 |
| 13038 | 該股票非借券標的，或不允許借券賣出 |
| 13040 | 委託書編號錯誤 |
| 13043 | 委託失敗，此股票已暫停交易 |
| 13045 | 委託失敗，此股票已收盤無法交易 |
| 13046 | 請選擇以限價或市價重新委託 |
| 13047 | 請選擇以ROD、IOC、FOK重新委託 |
| 13048 | 委託失效；IOC、FOK委託未能成交 |
| 13049 | 委託失敗；集合競價或瞬間價格穩定措施時段，不接受市價、IOC、FOK |
| 13050 | 此筆委託無可取消數量，請檢查是否已成交 |
| 13051 | 部分成交；超過價格穩定機制上、下限剩餘數量被取消 |
| 13052 | 委託失效；觸及價格穩定機制上、下限 |
| 13053 | 此筆不接受改價 |
| 13060 | 委託下單失敗 |
| 13061 | 委託已送出，但尚未收到交易所回報 |
| 13062 | 委託已送出，待交易所線路恢復，請稍待 |
| 13063 | 下單作業中斷，該委託單已取消 |
| 13064 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13065 | 證券交易所交易系統已停止服務 |
| 13066 | 此筆委託單，委託失敗 |
| 13069 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13089 | 交易所連線異常,請洽業務員 |
| 13099 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 13200 | 委託成功 |
| 13201 | 已超過委託時間 |
| 13202 | 時間未到,稍待再輸入委託 |
| 13203 | 取消或改量失敗,交易正在處理中,稍待再重新進行 |
| 13204 | 取消或改量失敗,交易正在處理中,稍待再輸入委託 |
| 13205 | 無該委託單,請檢查該委託是否已成交 |
| 13211 | 委託資料有誤,請檢查後重新委託 |
| 13212 | 委託資料有誤,請檢查後重新委託 |
| 13213 | 委託資料有誤,請檢查後重新委託 |
| 13214 | 帳號錯誤,請檢查並更正 |
| 13215 | 委託資料有誤,請檢查後重新委託 |
| 13216 | 委託資料有誤,請檢查後重新委託 |
| 13218 | 委託資料有誤,請檢查後重新委託 |
| 13219 | 檢查並更正下單類別註記 |
| 13220 | 股票代號錯誤,請檢查並更正 |
| 13221 | 委託單價錯誤,請檢查並更正 |
| 13222 | 委託張數錯誤.請檢查並更正 |
| 13224 | 買賣別錯誤,請檢查並更正 |
| 13225 | 委託下單種類錯誤,請檢查並更正 |
| 13226 | 交易別錯誤,請檢查並更正 |
| 13227 | 該股票不許自營商交易 |
| 13228 | 該股票不許外資交易 |
| 13229 | 委託種類錯誤,請檢查並更正 |
| 13230 | 外資買進或借券賣出已無委託額度 |
| 13231 | 部分成交；剩餘數量被取消 |
| 13232 | 取消數量超過原有數量 |
| 13233 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 13234 | 颱風地區證券商不得交易 |
| 13235 | 委託張數錯誤,請檢查並更正 |
| 13236 | 委託張數錯誤,請檢查並更正 |
| 13237 | 請確認委託單價是否正確後,重新委託並確認 |
| 13238 | 今日收盤價低於參考價，不可融券或借券賣出 |
| 13243 | 委託失敗，此股票已暫停交易 |
| 13246 | 請選擇以限價或市價重新委託 |
| 13247 | 請選擇以ROD、IOC、FOK重新委託 |
| 13250 | 此筆委託無可取消數量，請檢查是否已成交 |
| 13260 | 委託下單失敗 |
| 13261 | 委託已送出，但尚未收到交易所回報 |
| 13262 | 委託已送出，待交易所線路恢復，請稍待 |
| 13263 | 下單作業中斷，該委託單已取消 |
| 13264 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13265 | 證券交易所交易系統已停止服務 |
| 13266 | 此筆委託單，委託失敗 |
| 13269 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13289 | 交易所連線異常,請洽業務員 |
| 13299 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 13300 | 委託成功 |
| 13301 | 已超過委託時間 |
| 13302 | 時間未到,稍待再輸入委託 |
| 13305 | 無該委託單,請檢查該委託是否已成交 |
| 13305 | 無該委託單,請檢查該委託是否已成交 |
| 13311 | 委託資料有誤,請檢查後重新委託 |
| 13312 | 委託資料有誤,請檢查後重新委託 |
| 13313 | 委託資料有誤,請檢查後重新委託 |
| 13314 | 帳號錯誤,請檢查並更正 |
| 13315 | 委託資料有誤,請檢查後重新委託 |
| 13318 | 委託資料有誤,請檢查後重新委託 |
| 13319 | 檢查並更正下單類別註記 |
| 13319 | 檢查並更正下單類別註記 |
| 13320 | 股票代號錯誤,請檢查並更正 |
| 13321 | 委託單價錯誤,請檢查並更正 |
| 13322 | 委託股數錯誤,請檢查並更正 |
| 13324 | 買賣別錯誤,請檢查並更正 |
| 13325 | 委託下單種類錯誤,請檢查並更正 |
| 13326 | 交易別錯誤,請檢查並更正 |
| 13327 | 該股票不許自營商交易 |
| 13328 | 該股票不許外資交易 |
| 13330 | 該股票外資額度已滿 |
| 13331 | 外資委託數量被刪減 |
| 13332 | 取消數量超過原有數量 |
| 13333 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 13335 | 委託失敗；該股票已超過證券商可買入金額 |
| 13336 | 委託失敗；該股票已超過證券商可賣出金額 |
| 13340 | 委託書編號錯誤 |
| 13343 | 委託失敗，此股票已暫停交易 |
| 13346 | 請選擇以限價或市價重新委託 |
| 13347 | 請選擇以ROD、IOC、FOK重新委託 |
| 13350 | 此筆委託無可取消數量，請檢查是否已成交 |
| 13360 | 委託下單失敗 |
| 13361 | 委託已送出，但尚未收到交易所回報 |
| 13362 | 委託已送出，待交易所線路恢復，請稍待 |
| 13363 | 下單作業中斷，該委託單已取消 |
| 13364 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13365 | 證券交易所交易系統已停止服務 |
| 13366 | 此筆委託單，委託失敗 |
| 13369 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 13389 | 交易所連線異常,請洽業務員 |
| 13399 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 14000 | 委託成功 |
| 14001 | 已超過委託時間 |
| 14002 | 時間未到,稍待再輸入委託 |
| 14011 | 委託資料有誤,請檢查後重新委託 |
| 14012 | 委託資料有誤,請檢查後重新委託 |
| 14013 | 委託資料有誤,請檢查後重新委託 |
| 14014 | 委託股數錯誤,請檢查並更正 |
| 14015 | 委託資料有誤,請檢查後重新委託 |
| 14016 | 委託資料有誤,請檢查後重新委託 |
| 14017 | 委託資料有誤,請檢查後重新委託 |
| 14018 | 買賣別錯誤,請檢查並更正 |
| 14019 | 委託下單種類錯誤,請檢查並更正 |
| 14020 | 帳號錯誤,請檢查並更正 |
| 14021 | 股票代號錯誤,請檢查並更正 |
| 14022 | 股票代號錯誤,請檢查並更正 |
| 14023 | 委託股數錯誤,請檢查並更正 |
| 14024 | 委託資料有誤,請檢查後重新委託 |
| 14025 | 委託資料有誤,請檢查並更正 |
| 14026 | 該帳號不得買進零股,請檢查並更正 |
| 14027 | 該股票不許自營商交易 |
| 14030 | 該股票不許外資交易 |
| 14031 | 該股票外資額度已滿 |
| 14032 | 部分成交；剩餘數量被取消 |
| 14033 | 取消或改量失敗,交易正在處理中,稍待再重新進行 |
| 14035 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 14043 | 委託失敗，此股票已暫停交易 |
| 14046 | 請選擇以限價或市價重新委託 |
| 14047 | 請選擇以ROD、IOC、FOK重新委託 |
| 14050 | 此筆委託無可取消數量，請檢查是否已成交 |
| 14060 | 委託下單失敗 |
| 14061 | 委託已送出，但尚未收到交易所回報 |
| 14062 | 委託已送出，待交易所線路恢復，請稍待 |
| 14063 | 下單作業中斷，該委託單已取消 |
| 14064 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 14065 | 證券交易所交易系統已停止服務 |
| 14066 | 此筆委託單，委託失敗 |
| 14069 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 14089 | 交易所連線異常,請洽業務員 |
| 14099 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 18300 | 委託成功 |
| 18301 | 已超過委託時間 |
| 18302 | 時間未到,稍待再輸入委託 |
| 18305 | 無該委託單,請檢查該委託是否已成交 |
| 18311 | 委託資料有誤,請檢查後重新委託 |
| 18312 | 委託資料有誤,請檢查後重新委託 |
| 18313 | 委託資料有誤,請檢查後重新委託 |
| 18314 | 帳號錯誤,請檢查並更正 |
| 18315 | 委託資料有誤,請檢查後重新委託 |
| 18318 | 委託資料有誤,請檢查後重新委託 |
| 18319 | 檢查並更正下單類別註記 |
| 18319 | 檢查並更正下單類別註記 |
| 18320 | 股票代號錯誤,請檢查並更正 |
| 18321 | 委託單價錯誤,請檢查並更正 |
| 18322 | 委託股數錯誤,請檢查並更正 |
| 18324 | 買賣別錯誤,請檢查並更正 |
| 18325 | 委託下單種類錯誤,請檢查並更正 |
| 18326 | 交易別錯誤,請檢查並更正 |
| 18327 | 大陸地區人民不得買進 |
| 18328 | 該股票不許自營商交易 |
| 18329 | 該股票不許外資交易 |
| 18330 | 該股票外資額度已滿 |
| 18331 | 外資委託數量被刪減 |
| 18332 | 取消數量超過原有數量 |
| 18333 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 18335 | 外資客戶尚未開戶,不許委託 |
| 18336 | 委託失敗；該股票已超過證券商可買入金額 |
| 18337 | 委託失敗；該股票已超過證券商可賣出金額 |
| 18341 | 委託書編號錯誤 |
| 18343 | 委託資料有誤,請檢查並更正 |
| 18345 | 委託失敗，此股票已收盤無法交易 |
| 18346 | 請選擇以限價或市價重新委託 |
| 18347 | 請選擇以ROD、IOC、FOK重新委託 |
| 18350 | 此筆委託無可取消數量，請檢查是否已成交 |
| 18360 | 委託下單失敗 |
| 18361 | 委託已送出，但尚未收到交易所回報 |
| 18362 | 委託已送出，待交易所線路恢復，請稍待 |
| 18363 | 下單作業中斷，該委託單已取消 |
| 18364 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 18365 | 證券交易所交易系統已停止服務 |
| 18366 | 此筆委託單，委託失敗 |
| 18369 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 18389 | 交易所連線異常,請洽業務員 |
| 18399 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 19300 | 委託成功 |
| 19301 | 已超過委託時間 |
| 19302 | 時間未到,稍待再輸入委託 |
| 19303 | 取消或改量失敗,交易正在處理中,稍待再重新進行 |
| 19304 | 取消或改量失敗,交易正在處理中,稍待再輸入委託 |
| 19305 | 無該委託單,請檢查該委託是否已成交 |
| 19305 | 查無此筆委託單,請檢查該委託是否已成交 |
| 19311 | 委託資料有誤,請檢查後重新委託 |
| 19312 | 委託資料有誤,請檢查後重新委託 |
| 19313 | 委託資料有誤,請檢查後重新委託 |
| 19314 | 帳號錯誤,請檢查並更正 |
| 19315 | 委託資料有誤,請檢查後重新委託 |
| 19316 | 委託資料有誤,請檢查後重新委託 |
| 19318 | 委託資料有誤,請檢查後重新委託 |
| 19319 | 檢查並更正下單類別註記 |
| 19320 | 股票代號錯誤,請檢查並更正 |
| 19321 | 委託單價錯誤,請檢查並更正 |
| 19321 | 委託單價錯誤,請檢查並更正 |
| 19322 | 委託張數錯誤.請檢查並更正 |
| 19324 | 買賣別錯誤,請檢查並更正 |
| 19325 | 委託下單種類錯誤,請檢查並更正 |
| 19326 | 交易別錯誤,請檢查並更正 |
| 19327 | 大陸地區人民不得買進 |
| 19328 | 該股票不許自營商交易 |
| 19329 | 該股票不許外資交易 |
| 19330 | 外資買進或借券賣出已無委託額度 |
| 19331 | 部分成交；剩餘數量被取消 |
| 19332 | 取消數量超過原有數量 |
| 19333 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 19334 | 颱風地區證券商不得交易 |
| 19335 | 外資客戶尚未開戶,不許委託 |
| 19336 | 該股票買進金額超過交易所限制 |
| 19337 | 該股票賣出金額超過交易所限制 |
| 19338 | 此股票不可信用交易 |
| 19339 | 此股票投信不得交易 |
| 19341 | 委託書編號錯誤 |
| 19343 | 委託失敗，此股票已暫停交易 |
| 19345 | 委託失敗，此股票已收盤無法交易 |
| 19346 | 請選擇以限價或市價重新委託 |
| 19347 | 請選擇以ROD、IOC、FOK重新委託 |
| 19348 | 委託失效；IOC、FOK委託未能成交 |
| 19349 | 委託失敗；集合競價或瞬間價格穩定措施時段，不接受市價、IOC、FOK |
| 19350 | 此筆委託無可取消數量，請檢查是否已成交 |
| 19351 | 部分成交；超過價格穩定機制上、下限剩餘數量被取消 |
| 19352 | 委託失效；觸及價格穩定機制上、下限 |
| 19353 | 此筆不接受改價 |
| 19360 | 委託下單失敗 |
| 19361 | 委託已送出，但尚未收到交易所回報 |
| 19362 | 委託已送出，待交易所線路恢復，請稍待 |
| 19363 | 下單作業中斷，該委託單已取消 |
| 19364 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19365 | 證券交易所交易系統已停止服務 |
| 19366 | 此筆委託單，委託失敗 |
| 19369 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19389 | 交易所連線異常,請洽業務員 |
| 19400 | 委託成功 |
| 19401 | 已超過委託時間 |
| 19402 | 時間未到,稍待再輸入委託 |
| 19403 | 取消或改量失敗,交易正在處理中,稍待再重新進行 |
| 19403 | 尚無委託資料 |
| 19411 | 委託資料有誤,請檢查後重新委託 |
| 19412 | 委託資料有誤,請檢查後重新委託 |
| 19413 | 委託資料有誤,請檢查後重新委託 |
| 19414 | 委託股數錯誤,請檢查並更正 |
| 19415 | 委託資料有誤,請檢查後重新委託 |
| 19417 | 委託資料有誤,請檢查後重新委託 |
| 19418 | 買賣別錯誤,請檢查並更正 |
| 19419 | 只允許正常零股委託或錯帳零股委託 |
| 19420 | 帳號錯誤,請檢查並更正 |
| 19421 | 股票代號錯誤,請檢查並更正 |
| 19422 | 此股票不得零股交易 |
| 19423 | 委託股數錯誤,請檢查並更正 |
| 19425 | 外資不可買進此檔股票 |
| 19426 | 委託單價錯誤,請檢查並更正 |
| 19427 | 證券商休市 |
| 19428 | 大陸地區人民不得買進 |
| 19429 | 該股票不許自營商交易 |
| 19435 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 19443 | 委託失敗，此股票已暫停交易 |
| 19446 | 請選擇以限價或市價重新委託 |
| 19447 | 請選擇以ROD、IOC、FOK重新委託 |
| 19450 | 此筆委託無可取消數量，請檢查是否已成交 |
| 19460 | 委託下單失敗 |
| 19461 | 委託已送出，但尚未收到交易所回報 |
| 19462 | 委託已送出，待交易所線路恢復，請稍待 |
| 19463 | 下單作業中斷，該委託單已取消 |
| 19464 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19465 | 證券交易所交易系統已停止服務 |
| 19466 | 此筆委託單，委託失敗 |
| 19469 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19499 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 19800 | 委託成功 |
| 19801 | 已超過委託時間 |
| 19802 | 時間未到,稍待再輸入委託 |
| 19805 | 查無此筆委託單,請檢查該委託是否已成交 |
| 19811 | 委託資料有誤,請檢查後重新委託 |
| 19812 | 委託資料有誤,請檢查後重新委託 |
| 19813 | 委託資料有誤,請檢查後重新委託 |
| 19814 | 帳號錯誤,請檢查並更正 |
| 19815 | 委託資料有誤,請檢查後重新委託 |
| 19816 | 委託資料有誤,請檢查後重新委託 |
| 19818 | 委託資料有誤,請檢查後重新委託 |
| 19819 | 檢查並更正下單類別註記 |
| 19820 | 股票代號錯誤,請檢查並更正 |
| 19821 | 委託單價錯誤,請檢查並更正 |
| 19822 | 委託張數錯誤.請檢查並更正 |
| 19824 | 買賣別錯誤,請檢查並更正 |
| 19825 | 委託下單種類錯誤,請檢查並更正 |
| 19826 | 交易別錯誤,請檢查並更正 |
| 19827 | 大陸地區人民不得買進 |
| 19828 | 該股票不許自營商交易 |
| 19829 | 該股票不許外資交易 |
| 19830 | 外資買進或借券賣出已無委託額度 |
| 19831 | 部分成交；剩餘數量被取消 |
| 19832 | 取消數量超過原有數量 |
| 19833 | 總委託金額超過限額,只允許取消,改量及查詢 |
| 19834 | 颱風地區證券商不得交易 |
| 19835 | 外資客戶尚未開戶,不許委託 |
| 19836 | 該股票買進金額超過交易所限制 |
| 19837 | 該股票賣出金額超過交易所限制 |
| 19838 | 此股票不可信用交易 |
| 19839 | 此股票投信不得交易 |
| 19840 | 此筆委託已存在 |
| 19841 | 今日收盤價低於參考價，不可融券或借券賣出 |
| 19843 | 委託失敗，此股票已暫停交易 |
| 19846 | 請選擇以限價或市價重新委託 |
| 19847 | 請選擇以ROD、IOC、FOK重新委託 |
| 19850 | 此筆委託無可取消數量，請檢查是否已成交 |
| 19860 | 委託下單失敗 |
| 19861 | 委託已送出，但尚未收到交易所回報 |
| 19862 | 委託已送出，待交易所線路恢復，請稍待 |
| 19863 | 下單作業中斷，該委託單已取消 |
| 19864 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19865 | 證券交易所交易系統已停止服務 |
| 19866 | 此筆委託單，委託失敗 |
| 19869 | 下單作業中斷，該委託單已送出，請先查詢委託資料或洽所屬業務員 |
| 19889 | 交易所連線異常,請洽業務員 |
| 19899 | 請查詢委託是否已輸入成功,若有任何問題請洽所屬業務員或客服專線 |
| 20001 | 帳號輸入錯誤，請重新輸入 |
| 20002 | 委託類別錯誤，請重新輸入 |
| 20003 | 股票代號錯誤，請重新輸入 |
| 20004 | 委託數量錯誤，請重新輸入 |
| 20005 | 委託單價錯誤，請重新輸入 |
| 20006 | 請洽分公司，更新業務員代號 |
| 20007 | 買賣別錯誤，請重新輸入 |
| 20008 | 有效交易日期錯誤，請重新查詢 |
| 20009 | 委託序號重覆 |
| 20010 | 查無此筆委託資料；如有問題請洽業務員 |
| 20011 | 刪改單失敗；此筆委託已成交 |
| 20012 | 刪改單失敗；此筆委託已取消 |
| 20013 | 請洽業務員，更正委託單號 |
| 20014 | 委託單號錯誤，如有問題請洽業務員 |
| 20015 | 人工單不能透過電子通路改量或取消；如有問題請洽營業員 |
| 20020 | 改量時數量須大於零，請重新輸入 |
| 20021 | 改量時數量須小於等於未成交數量，請重新輸入 |
| 20023 | 市價單不接受改價 |
| 20024 | 原委託為限價單，只可接受「限價改限價」委託 |
| 20030 | 委託單價不可為零，請重新輸入 |
| 20031 | 改量委託單價錯誤，請重新輸入 |
| 20032 | 取消委託單價錯誤，請重新輸入 |
| 20043 | 委託失敗；此股票暫停交易 |
| 20044 | 委託失敗，此股票為非本日可交易股票，如有問題請洽所屬業務員 |
| 20091 | 委託失敗：不提供此功能 |
| 20092 | 委託失敗：不提供此功能 |
| 20093 | 委託失敗：不提供此功能 |
| 20101 | 未完成開立交割銀行帳號；如有問題請洽業務員 |
| 20102 | 未完成開立集保戶；如有問題請洽分公司 |
| 20103 | 未簽署最新版權證風險預告書，請使用電子憑證或分公司辦理簽署；如有問題請洽業務員 |
| 20104 | 今日才開戶，明日才可委託；如有問題請洽分公司 |
| 20105 | 未完成開立帳號；如有問題請洽分公司 |
| 20106 | 未開立信用交易，只可 買賣現股；如有問題請洽業務員 |
| 20107 | 客戶狀態異常(解約戶) |
| 20108 | 委託失敗；尚未開放權證電子下單，請洽業務員申請開放 |
| 20109 | 此帳號暫停交易，請洽業務員 |
| 20110 | 此帳號只可交易庫存部位；如有問題請洽業務員 |
| 20111 | 此帳號暫停交易；如有問題請洽業務員 |
| 20112 | 此帳號暫停交易；如有問題請洽業務員 |
| 20113 | 此帳號已註銷；如有問題請洽業務員 |
| 20114 | 信用交易只可資賣或券買；如有問題請洽業務員 |
| 20115 | 此帳號只可買進；如有問題請洽業務員 |
| 20116 | 此帳號只可賣出；如有問題請洽業務員 |
| 20117 | 此帳號限制買賣；如有問題請洽業務員 |
| 20118 | 此帳號限制融資買進；如有問題請洽業務員 |
| 20119 | 客戶狀態異常(未簽二類股風險預告書) |
| 20121 | 今日已有委買,不可再做委賣；如有問題請洽業務員 |
| 20122 | 今日已有委賣,不可再做委買；如有問題請洽業務員 |
| 20124 | 此帳號信用交易暫停資買或券賣；如有問題請洽業務員 |
| 20125 | 此帳號暫停信用交易；如有問題請洽業務員 |
| 20126 | 此帳號信用交易已註銷；如有問題請洽業務員 |
| 20127 | 此帳號暫停信用交易；如有問題請洽業務員 |
| 20128 | 此帳號暫停信用交易；如有問題請洽業務員 |
| 20132 | 未簽署外國企業來台上市櫃風險預告書，請使用電子憑證或分公司辦理簽署；如有問題請洽業務員 |
| 20134 | 委託失敗；此帳號身分別只可委託賣出；如有問題請洽業務員 |
| 20135 | 此帳號只可賣出；如有問題請洽業務員 |
| 20136 | 委託失敗；尚未完成信用開戶，如有問題請洽業務員 |
| 20137 | 未簽署外國企業來台上市櫃風險預告書，請使用電子憑證或分公司辦理簽署；如有問題請洽業務員 |
| 20139 | 委託失敗；您目前狀態為當日違約，不可買賣，如有問題請洽所屬業務員 |
| 20140 | 委託失敗，您目前狀態為當日違約，如需當沖反向交易，請洽所屬業務員 |
| 20141 | 委託失敗；此帳號身分別只可委託賣出；如有問題請洽業務員 |
| 20142 | 未簽署『日本公司來台上櫃(市)及興櫃股票』特別注意事項 |
| 20143 | 未簽署槓桿反向ETF預告書 |
| 20144 | 未簽署「一般ETF」風險預告書 |
| 20145 | 未開立或未約定「外幣綜合存款」帳戶，如有問題請洽業務員 |
| 20147 | 未簽署外幣ETF預告書 |
| 20148 | 未簽署期信槓反ETF預告書 |
| 20149 | 未簽署指數股票一般型ETF預告書 |
| 20150 | 未簽署新版權證風險預告書 |
| 20151 | 未簽署「連結特殊商品個股ETF」風險預告書 |
| 20152 | 未簽署「指數投資證券(ETN)」風險預告書 |
| 20153 | 未簽署「買賣可轉債及交換公司債風險預告書」 |
| 20154 | 未符合槓反ETN交易條件，如有問題請洽所屬業務員 |
| 20158 | 您尚未簽署「槓桿反向指數股票型期貨信託基金受益憑證交易檢核表」請前往簽署 |
| 20159 | 您尚未簽署「指數投資證券買賣及申購賣回風險預告書(ETN)」，請先前往簽署 |
| 20160 | 期貨ETF相關商品，今日只可委託賣出，不能買進 |
| 20161 | 期貨ETF相關商品，今日只可委託賣出，不能買進 |
| 20162 | 您尚未簽署「上櫃外幣ETF基金配息同意書 」請前往簽署 |
| 20163 | 委託失敗；普通交易限額之額度未設定(群組)，如有問題請洽所屬業務員 |
| 20201 | 此股票不可融資買進；如有問題請洽業務員 |
| 20202 | 此股票不可融券賣出；如有問題請洽業務員 |
| 20203 | 此股票暫停融資買進；如有問題請洽業務員 |
| 20204 | 此股票暫停融券賣出；如有問題請洽業務員 |
| 20205 | 此股票無融資配額；如有問題請洽業務員 |
| 20206 | 此股票無融券配額；如有問題請洽業務員 |
| 20207 | 警示股票只可委託買進；如有問題請洽業務員 |
| 20208 | 警示股或權證高風險股只可委託賣出，若要買進，請逕向業務員委託 |
| 20209 | 警示股票本日限制委託買賣；如有問題請洽業務員 |
| 20210 | 請洽分公司，更新股票市場別 |
| 20211 | 此股票資券配額不足；如有問題請洽業務員 |
| 20212 | 此股票暫停融資互抵買進交易；如有問題請洽業務員 |
| 20213 | 此股票暫停融券互抵賣出交易；如有問題請洽業務員 |
| 20214 | 公司員工不能買其他券商股票；如有問題請洽業務員 |
| 20215 | 此股票融券賣出價格須大於等於平盤價；請改價或洽業務員 |
| 20216 | 請洽分公司，更新股票類別 |
| 20217 | 此股票不能融資買進；如有問題請洽業務員 |
| 20218 | 此股票無漲跌幅限制，僅接受限價委託 委託失敗，此個股僅接受限價委託 |
| 20219 | 首五日及無漲跌幅股票，僅接受限價委託 |
| 20222 | 營業員本人或其未成年子女帳號不可「業代下單」自行委託輸入 |
| 20232 | 委託失敗；您已申請「預支交割款」借款，請先取消借款，再進行盤後交易 |
| 20301 | 復華融資交易,只能賣出 |
| 20302 | 復華融券交易,只能買進 |
| 20303 | 委託類別5不能做賣出 |
| 20304 | 委託類別6不能做買進 |
| 20305 | 資券配額不足 |
| 20306 | 資券配額不足 |
| 20307 | 資券配額不足 |
| 20308 | 委託已超過公司淨值；如有問題請洽業務員 |
| 20309 | 單筆互抵數,不可大於原始資配額；如有問題請洽業務員 |
| 20310 | 單筆互抵數,不可大於原始券配額；如有問題請洽業務員 |
| 20311 | OTC不能做資券互抵 |
| 20314 | [借券]委託，只能賣出 |
| 20315 | 委託失敗；策略性借券賣出單價須大於等於平盤價，如有問題請洽業務員 |
| 20316 | 委託失敗；借券賣出單價須大於等於平盤價，如有問題請洽業務員 |
| 20317 | 委託失敗；此股票不接受「現股當沖」交易 |
| 20401 | 此股票超出委託數量；如有問題請洽業務員 |
| 20402 | 此股票超出委託金額；如有問題請洽業務員 |
| 20403 | 此為全額交割股票；如有問題請洽業務員 |
| 20404 | 此為交易所警示股票；如有問題請洽業務員 |
| 20405 | 單筆委託金額，超過單股限額；如有問題請洽業務員 |
| 20406 | 價格超過下限；如有問題請洽業務員 |
| 20407 | 價格超過上限；如有問題請洽業務員 |
| 20408 | 委託張數超過99張,請改量或逕向營業員下單 |
| 20409 | 此為二類股票 |
| 20410 | 委託失敗；權證買進單價超過開盤參考價2倍，請改價或聯絡業務員 |
| 20411 | 委託失敗；權證下市前30個交易日停止電子通路買進，如有問題請洽業務員 |
| 20412 | 買進單價超過控管漲幅範圍，請改價或聯絡業務員下單 |
| 20413 | 賣出單價超過控管跌幅範圍，請改價或聯絡業務員下單 |
| 20481 | 委託失敗；此股票控管為不可買進，如有問題請洽業務員 |
| 20482 | 委託失敗；此股票控管為不可賣出，如有問題請洽業務員 |
| 20483 | 此為全額交割股票；如有問題請洽業務員 |
| 20484 | 此為全額交割股票；如有問題請洽業務員 |
| 20485 | 此為處置股票；如有問題請洽業務員 |
| 20486 | 此為處置股票；如有問題請洽業務員 |
| 20503 | 委託失敗；此股票融資配額不足，如有問題請洽業務員 |
| 20504 | 委託失敗；此股票資券配額不足，如有問題請洽業務員 |
| 20505 | 委託失敗；單筆融資買進，超過交易所數量限額，如有問題請洽業務員 |
| 20506 | 此股票已無配額可用；如有問題請洽業務員 |
| 20507 | 委託失敗；停資期間，暫停融券賣出；如有問題請洽業務員 |
| 20508 | 委託失敗；此股票已無配額可用，如有問題請洽業務員 |
| 20509 | 委託失敗；此股票已無配額可用，如有問題請洽業務員 |
| 20510 | 委託失敗；此股票已無配額可用，如有問題請洽業務員 |
| 20511 | 委託失敗；單筆融券賣出，超過交易所數量限額，如有問題請洽業務員 |
| 20512 | 委託失敗；停券期間，暫停融券賣出，如有問題請洽業務員 |
| 20601 | 與交易所線路異常 |
| 20602 | 交易線路忙碌中且委託記錄逾時，請查詢委託回報或洽業務員 |
| 20603 | 漲跌幅未轉,請稍後再委託 |
| 20604 | 漲跌幅未轉,請稍後再委託 |
| 20605 | 信用配額未轉檔,請稍後再委託 |
| 20683 | 委託失敗；此股票控管為不可買進，如有問題請洽業務員 |
| 20684 | 委託失敗；此股票暫停交易 |
| 20804 | 回覆訊息代碼錯誤,請洽客服人員 |
| 21100 | 委託失敗；電子單筆委託金額超過限額，如有問題請洽業務員 |
| 21101 | 委託下單金額累計超過額度；如有問題請洽業務員 |
| 21102 | 委託下單金額累計超過額度；如有問題請洽業務員 |
| 21103 | 委託下單金額累計超過額度；如有問題請洽業務員 |
| 21104 | 委託下單金額累計超過額度；如有問題請洽業務員 |
| 21105 | 委託下單金額累計超過額度；如有問題請洽業務員 |
| 21106 | 委託失敗；境外ETF委託買進金額累計超過限額，如有問題請洽業務員 |
| 21107 | 委託失敗；權證或境外ETF權證委託買進金額累計超過限額，如有問題請洽業務員 |
| 21108 | 委託失敗；普通限額使用超額，如有問題請洽業務員 |
| 21109 | 委託失敗；『單一權證買進累計』數量超過限額，如有問題請洽業務員 |
| 21112 | 上櫃股票融資買進單股單日累計數量超過額度；如有問題請洽業務員 |
| 21121 | 委託下單累計超過額度；如有問題請洽業務員 |
| 21123 | 95開頭帳號只可賣,不可買(投資海外可轉換公司債者) ；如有問題請洽業務員 |
| 21128 | 此為需預繳商品，買進預收款不足！立即前往線上預繳，完成預繳後，請重新下單 |
| 21129 | 此帳號只看盤不電子下單；如有問題請洽業務員 |
| 21130 | 客戶狀態異常(未開電子功能) |
| 21132 | 整戶買賣交易預收款項不足，如有問題請洽詢所屬業務員 |
| 21133 | 整戶買賣交易預收款項不足，如有問題請洽詢所屬業務員 |
| 21134 | 個股預收款項不足，如有問題請洽詢所屬業務員 |
| 21135 | 整戶買賣交易預收款項不足！立即前往線上預繳，完成預繳後，請重新下單 |
| 21136 | 整戶買賣交易預收款項不足！立即前往線上預繳，完成預繳後，請重新下單 |
| 21137 | 整戶買賣交易預收款項不足！立即前往線上預繳，完成預繳後，請重新下單 |
| 21151 | 委託下單累計超過額度；如有問題請洽業務員 |
| 21171 | 委託下單累計超過額度；如有問題請洽業務員 |
| 21202 | 委託下單數量累計超過額度；如有問題請洽業務員 |
| 21222 | 委託下單數量累計超過額度；如有問題請洽業務員 |
| 21251 | 委託失敗，買進累計數量超過控管股票限額，如有問題請洽業務員 |
| 21252 | 委託下單數量累計超過額度；如有問題請洽業務員 |
| 21265 | 委託下單累計超過電子額度；如有問題請洽業務員 |
| 21272 | 委託下單數量累計超過額度；如有問題請洽業務員 |
| 21303 | 信用交易庫存數量不足；如有問題請洽業務員 |
| 21323 | 委託失敗；信用交易庫存不足，如有問題請洽業務員 |
| 21328 | 此為需圈存商品，賣出圈存數量不足！立即前往線上圈存，完成圈存後，請重新下單 |
| 21333 | 委託失敗；外國股票現股庫存不足，如有問題請洽業務員 |
| 21334 | 整戶賣出圈存數量不足！立即前往線上圈存，完成圈存後，請重新下單 |
| 21335 | 整戶賣出圈存數量不足！立即前往線上圈存，完成圈存後，請重新下單 |
| 21336 | 整戶賣出圈存數量不足！立即前往線上圈存，完成圈存後，請重新下單 |
| 21352 | 委託失敗，單筆委託數量已超過該股票券源，請調整數量重新下單或洽您所屬業務員 |
| 21353 | 委託失敗；現股庫存不足，如有問題請洽業務員 |
| 21355 | 委託失敗；借券庫存不足，如有問題請洽業務員 |
| 21363 | 委託失敗；外國股票現股庫存不足，如有問題請洽業務員 |
| 21373 | 委託失敗；現股庫存不足，如有問題請洽業務員 |
| 21404 | 委託失敗；買進金額超過限額，如有問題請洽業務員 |
| 21424 | 委託失敗；買進總金額超過限額，如有問題請洽業務員 |
| 21454 | 委託失敗；賣出總金額超過限額，如有問題請洽業務員 |
| 21474 | 委託失敗；賣出總金額超過限額，如有問題請洽業務員 |
| 21481 | 委託失敗；買進或賣出數量累計超過個股控管數量，如有問題請洽業務員 |
| 21482 | 委託失敗；買進或賣出累計金額超過個股控管限額，如有問題請洽業務員 |
| 21483 | 委託失敗；買進或賣出數量累計超過個股控管數量，如有問題請洽業務員 |
| 21484 | 委託失敗；買進或賣出累計金額超過個股控管限額，如有問題請洽業務員 |
| 21506 | 委託失敗；融資買進單一股票超過限額；如有問題請洽業務員 |
| 21507 | 委託失敗；融資買進整戶超過額度，如有問題請洽業務員 |
| 21508 | 委託失敗；融資買進非放寬資券額度股票，整戶超過限額，如有問題請洽業務員 |
| 21511 | 委託失敗；融資買進整戶超過授信額度，如有問題請洽業務員 |
| 21526 | 委託失敗；單一股票融資買進累計超過額度，如有問題請洽業務員 |
| 21556 | 委託失敗；單一股票融券賣出累計超過額度；如有問題請洽業務員 |
| 21557 | 委託失敗；融券賣出整戶超過額度，如有問題請洽業務員 |
| 21558 | 委託失敗；融券賣出非放寬資券額度股票，整戶超過限額，如有問題請洽業務員 |
| 21576 | 委託失敗；融券賣出單一股票超過限額，如有問題請洽業務員 |
| 21577 | 委託失敗；融券賣出整戶超過額度，如有問題請洽業務員 |
| 21600 | 委託失敗；資券配額資料處理中，如有問題請洽業務員 |
| 21601 | 委託失敗；此股票無融資配額，如有問題請洽業務員 |
| 21602 | 委託失敗；此股票無融券配額，如有問題請洽業務員 |
| 21605 | 委託失敗；此股票融券配額不足，如有問題請洽業務員 |
| 21606 | 委託失敗；此股票融券配額不足，如有問題請洽業務員 |
| 21607 | 委託失敗；此股票融券配額不足，如有問題請洽業務員 |
| 21608 | 委託失敗；融資買進資餘額不足，如有問題請洽業務員 |
| 21609 | 委託失敗；資券互抵配額不足，如有問題請洽業務員 |
| 21613 | 委託失敗；融資配額不足，如有問題請洽業務員 |
| 21658 | 委託失敗；融券配額不足，如有問題請洽業務員 |
| 21853 | 委託失敗；現股庫存不足，如有問題請洽業務員 |
| 21881 | 錯帳累計張數超過 200 張 |
| 21882 | 錯帳累計金額超過 900 萬 |
| 29998 | 請重新委託或洽客服人員 |
| 29999 | 交易線路忙碌中,請由委託查詢或洽客服人員 |

## 附錄：市場表

| 市場代碼 | 市場別 | 交易所簡碼<br>(國外期貨下單用) | 市場名稱 |
| --- | --- | --- | --- |
| 1 | TWSE |  | 上市 |
| 2 | TWOTC |  | 上櫃 |
| 3 | TAIFEX |  | 期貨 |
| 4 | TWEMERGING |  | 興櫃 |
| 5 | TWSEODD |  | 盤中零股-上市 |
| 6 | TWOTCODD |  | 盤中零股-上櫃 |
| 202 | SGX | SGX | 新加坡交易所 |
| 203 | CME | CME | 芝商所CME Group |
| 204 | CBOT | CBT | 芝商所原CBOT |
| 205 | TCE | TCE | 東京商品 TOCOM |
| 207 | OSE | OSE | 日本交易所JPX |
| 208 | HKFE | HKF | 香港交易所 |
| 209 | NYBOT | NBT | 洲際-美國ICE-US交易所 |
| 210 | LIFFE | LIF | 洲際-英國ICE-UK交易所 |
| 211 | XEUREX | EUX | 歐洲交易所 |
| 212 | ASX | ASX | 澳洲交易所 |
| 215 | CBOE | CFE | CBOE期貨交易所 |

## 未納入資料

- `股名檔對照表(僅供參考,最後更新日期20260422)`：依使用者指示先忽略，未讀取、未摘要、未展開到本檔。

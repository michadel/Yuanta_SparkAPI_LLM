<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 26%" />
<col style="width: 4%" />
<col style="width: 15%" />
<col style="width: 9%" />
<col style="width: 21%" />
</colgroup>
<thead>
<tr>
<th colspan="6" style="text-align: center;"><div data-custom-style="header">
<p><strong>Service Input - Output Specification</strong></p>
</div></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>Project Name</strong></p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><strong>API GetOrderTradeReport</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>委託成交綜合回報</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>GetOrderTradeReport(NotshowCancel, Account, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">NotshowCancel</td>
<td style="text-align: center;">是否不列出取消單</td>
<td colspan="2" style="text-align: center;">bool</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OrderTradeReportResult 查詢委託成交回報結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkOrderList</td>
<td style="text-align: center;">現貨委託回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkOrder&gt;</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td style="text-align: center;">StkTradeList</td>
<td style="text-align: center;">現貨成交回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkTrade&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">FutOrderList</td>
<td style="text-align: center;">期貨委託回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutOrder&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">FutTradeList</td>
<td style="text-align: center;">期貨成交回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutTrade&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OVStkOrderList</td>
<td style="text-align: center;">國外股票委託回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVStkOrder&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OVStkTradeList</td>
<td style="text-align: center;">國外股票成交回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVStkTrade&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OVFutOrderList</td>
<td style="text-align: center;">國外期貨委託回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVFutOrder&gt;</td>
<td colspan="2" style="text-align: center;"><h1 id="section-1"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OVFutTradeList</td>
<td style="text-align: center;">國外期貨成交回報清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVFutTrade&gt;</td>
<td colspan="2" style="text-align: center;"><h1 id="section-2"></h1></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StkOrder 現貨委託回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">上市/上櫃</td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">股票名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"><p>0:現貨</p>
<p>3:融資</p>
<p>4:融券</p>
<p>5:策略借券</p>
<p>6:避險借券</p>
<p>7:資沖</p>
<p>8:券沖</p></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">價位</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">現貨小數4位,興櫃小數4位</td>
</tr>
<tr>
<td style="text-align: center;">PriceFlag</td>
<td style="text-align: center;">價格種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>H:漲停</p>
<p>L:跌停<br />
“-”:平盤</p>
<p>1-市價</p>
<p>2-限價</p></td>
</tr>
<tr>
<td style="text-align: center;">BeforeQty</td>
<td style="text-align: center;">前一次委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">For 委託狀態=取消成功</td>
</tr>
<tr>
<td style="text-align: center;">AfterQty</td>
<td style="text-align: center;">目前委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"><p>委託狀態=取消成功時,委託口數為0, 前端要改讀前一次委託量</p>
<p>委託狀態=10or24</p></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">委託狀態</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"><p>0:傳輸中</p>
<p>5:預約單</p>
<p>10:委託失敗</p>
<p>20:委託成功</p>
<p>24:委託失效</p>
<p>25:價穩失效　</p>
<p>30:取消成功</p></td>
</tr>
<tr>
<td style="text-align: center;">AcceptDate</td>
<td style="text-align: center;">委託日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>年月日</p></td>
</tr>
<tr>
<td style="text-align: center;">AcceptTime</td>
<td style="text-align: center;">委託時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>時分秒毫秒</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">“H00001”</td>
</tr>
<tr>
<td style="text-align: center;">ErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrorMessage</td>
<td style="text-align: center;">錯誤訊息</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Seller</td>
<td style="text-align: center;">營業員代碼</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Channel</td>
<td style="text-align: center;">Channel</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">APCode</td>
<td style="text-align: center;">APCode</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"><p>0:現貨</p>
<p>2:盤後零股</p>
<p>7:盤後</p>
<p>4:盤中零股</p>
<p>99:盤中零股</p></td>
</tr>
<tr>
<td style="text-align: center;">OTax</td>
<td style="text-align: center;">證交稅</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OCharge</td>
<td style="text-align: center;">手續費</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ODueAmt</td>
<td style="text-align: center;">應收付</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CancelFlag</td>
<td style="text-align: center;">可取消Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可取消</p></td>
</tr>
<tr>
<td style="text-align: center;">ReduceFlag</td>
<td style="text-align: center;">可減量Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可減量</p></td>
</tr>
<tr>
<td style="text-align: center;">TraditionFlag</td>
<td style="text-align: center;">傳統單Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘Y” :傳統單</td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">BasketNo</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">條件單識別資訊</td>
</tr>
<tr>
<td style="text-align: center;">TradeCurrency</td>
<td style="text-align: center;">報價幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>TWD</p>
<p>CNY</p>
<p>HKD</p>
<p>USD</p></td>
</tr>
<tr>
<td style="text-align: center;">Time_in_Force</td>
<td style="text-align: center;">委託效期</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>0:當日有效</p>
<p>3:IOC</p>
<p>4:FOK</p></td>
</tr>
<tr>
<td style="text-align: center;">Order_Success</td>
<td style="text-align: center;">委託成功旗標</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Reduce_Flag</td>
<td style="text-align: center;">本委託下單是否被減量</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Chg_Prz_Flag</td>
<td style="text-align: center;">本委託下單是否進行改價</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TSE_Cancel</td>
<td style="text-align: center;"><p>本委託下單是否</p>
<p>被交易所主動刪單</p></td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CancelQty</td>
<td style="text-align: center;">取消數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OR_QTY</td>
<td style="text-align: center;">原委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">UpdateDate</td>
<td style="text-align: center;">更新日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>年月日</p></td>
</tr>
<tr>
<td style="text-align: center;">UpdateTime</td>
<td style="text-align: center;">更新時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>時分秒毫秒</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StkTrade 現貨成交回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">股票名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"><p>0:現貨</p>
<p>3:融資</p>
<p>4:融券</p>
<p>5:策略借券</p>
<p>6:避險借券</p>
<p>7:資沖</p>
<p>8:券沖</p></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OPrice</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">現貨小數4位,興櫃小數4位</td>
</tr>
<tr>
<td style="text-align: center;">SPrice</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">現貨小數4位,興櫃小數4位</td>
</tr>
<tr>
<td style="text-align: center;">DateTime</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: left;">年月日時分秒毫秒</td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">“H0001”</td>
</tr>
<tr>
<td style="text-align: center;">TradeCurrency</td>
<td style="text-align: center;">報價幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>TWD</p>
<p>CNY</p>
<p>HKD</p>
<p>USD</p></td>
</tr>
<tr>
<td style="text-align: center;">Price_Flag</td>
<td style="text-align: center;">價位Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>1-市價</p>
<p>2-限價</p></td>
</tr>
<tr>
<td style="text-align: center;">Exchange_Code</td>
<td style="text-align: center;">委託別</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: left;"><p>0-一般委託</p>
<p>1-鉅額</p>
<p>2-零股</p>
<p>4-盤後定價</p>
<p>5 盤中零股</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutOrder 期貨委託回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Commodity1</td>
<td style="text-align: center;">商品代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">選擇權第7碼是C或P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">商品月份1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySellKind1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Commodity2</td>
<td style="text-align: center;">商品代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">選擇權第7碼是C或P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">商品月份2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySellKind2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OpenOffsetKind</td>
<td style="text-align: center;">新/平倉</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>0:新倉</p>
<p>1:平倉</p>
<p>2系統</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderCondition</td>
<td style="text-align: center;">委託條件</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>“ ”:ROD</p>
<p>”1”:FOK</p>
<p>”2”:IOC</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderPrice</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>M:市價</p>
<p>P:範圍市價</p></td>
</tr>
<tr>
<td style="text-align: center;">BeforeQty</td>
<td style="text-align: center;">前一次委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">For 委託狀態=取消成功</td>
</tr>
<tr>
<td style="text-align: center;">AferQty</td>
<td style="text-align: center;">目前委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">委託狀態=取消成功時,委託口數為0, 前端要改讀前一次委託量</td>
</tr>
<tr>
<td style="text-align: center;">OKQty</td>
<td style="text-align: center;">成交口數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">委託狀態</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: left;"><p>0:傳輸中</p>
<p>5:預約單</p>
<p>10:委託失敗</p>
<p>20:委託成功</p>
<p>30:取消成功</p></td>
</tr>
<tr>
<td style="text-align: center;">AcceptDate</td>
<td style="text-align: center;">委託日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">AcceptTime</td>
<td style="text-align: center;">委託時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">ErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrorMessage</td>
<td style="text-align: center;">錯誤訊息</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderNO</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ProductType</td>
<td style="text-align: center;">商品種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>O:選擇權</p>
<p>F:期貨</p></td>
</tr>
<tr>
<td style="text-align: center;">Seller</td>
<td style="text-align: center;">營業員代碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalMatFee</td>
<td style="text-align: center;">手續費總和</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalMatExchTax</td>
<td style="text-align: center;">交易稅總和</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalMatPremium</td>
<td style="text-align: center;">應收付</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Y:當沖</td>
</tr>
<tr>
<td style="text-align: center;">CancelFlag</td>
<td style="text-align: center;">可取消Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可取消</p></td>
</tr>
<tr>
<td style="text-align: center;">ReduceFlag</td>
<td style="text-align: center;">可減量Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可減量</p></td>
</tr>
<tr>
<td style="text-align: center;">StkName1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td style="text-align: center;">StkName2</td>
<td style="text-align: center;">商品名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td style="text-align: center;">TraditionFlag</td>
<td style="text-align: center;">傳統單Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘Y” :傳統單</td>
</tr>
<tr>
<td style="text-align: center;">TRID</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>FITX 200709,<br />
URO200709,</p>
<p>FIGTL7/C8,<br />
TXO09000T7,<br />
TXO08000/08100U7</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">BasketNo</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo1</td>
<td style="text-align: center;">市場代碼1</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>&lt;第1支腳&gt;</p></td>
</tr>
<tr>
<td style="text-align: center;">StkCode1</td>
<td style="text-align: center;">行情股票代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">&lt;第1支腳&gt;</td>
</tr>
<tr>
<td style="text-align: center;">MarketNo2</td>
<td style="text-align: center;">市場代碼2</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>&lt;第2支腳&gt;</p></td>
</tr>
<tr>
<td style="text-align: center;">StkCode2</td>
<td style="text-align: center;">行情股票代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">&lt;第2支腳&gt;</td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutTrade 期貨成交回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Commodity1</td>
<td style="text-align: center;">商品代號1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">選擇權第7碼是C或P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">商品月份1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySellKind1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交口數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MatchPrice1</td>
<td style="text-align: center;">成交價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MatchPrice2</td>
<td style="text-align: center;">成交價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MatchTime</td>
<td style="text-align: center;">成交時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MatchDate</td>
<td style="text-align: center;">成交日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderNO</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Commodity2</td>
<td style="text-align: center;">商品代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">選擇權第7碼是C或P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">商品月份2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySellKind2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">RecType</td>
<td style="text-align: center;">單式單/複式單</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>“1”:單式</p>
<p>“2”:複式</p></td>
</tr>
<tr>
<td style="text-align: center;">ProductType</td>
<td style="text-align: center;">商品種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderPrice</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td style="text-align: center;">StkName2</td>
<td style="text-align: center;">商品名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Ex:‘中鋼實 06 0030 C’, ‘台指01’,’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">SprMatchPrice</td>
<td style="text-align: center;">複式單成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TRID</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>2854, 05311<br />
FITX 200709,<br />
URO200709,</p>
<p>FIGTL7/C8,<br />
TXO09000T7,<br />
TXO08000/08100U7</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
<tr>
<td style="text-align: center;">SubNo</td>
<td style="text-align: center;">子成交序號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>0(單式)</p>
<p>1(複式腳1)</p>
<p>2(複式腳2)</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OVStkOrder 國外股票委託回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">證券帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>西元年</p></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>USD:美元</p>
<p>HDK:港幣</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">港股小數3位,美股小數4位</td>
</tr>
<tr>
<td style="text-align: center;">PriceType</td>
<td style="text-align: center;">價格型態</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘LMT’:限價單</td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">股數</td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">狀態碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: left;"><p>0:傳輸中</p>
<p>5:預約單</p>
<p>10:委託失敗</p>
<p>20:委託成功</p>
<p>30:取消成功</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderTime</td>
<td style="text-align: center;">委託時間</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託單型態</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">DAY:當日有效單<br />
GTD:指定日期單</td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Fee</td>
<td style="text-align: center;">手續費</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">PolarisAMT</td>
<td style="text-align: center;">應收付金額</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrorMessage</td>
<td style="text-align: center;">錯誤訊息</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>USD:美元</p>
<p>HDK:港幣</p></td>
</tr>
<tr>
<td style="text-align: center;">CancelFlag</td>
<td style="text-align: center;">可取消Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可取消</p></td>
</tr>
<tr>
<td style="text-align: center;">ReduceFlag</td>
<td style="text-align: center;">可減量Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘Y’/’N’<br />
＊美股不提供改量改價功能,由元件固定回N</td>
</tr>
<tr>
<td style="text-align: center;">TraditionFlag</td>
<td style="text-align: center;">傳統單Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘Y” :傳統單</td>
</tr>
<tr>
<td style="text-align: center;">SettleType</td>
<td style="text-align: center;">交割方式</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>0:外幣</p>
<p>1:台幣</p></td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">BasketNo</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">smart-04:長效單</td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OVStkTrade 國外股票成交回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>USD:美元</p>
<p>HDK:港幣</p></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderPrice</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">港股小數3位,美股小數4位</td>
</tr>
<tr>
<td style="text-align: center;">MatchPrice</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">港股小數3位,美股小數4位</td>
</tr>
<tr>
<td style="text-align: center;">DateTime</td>
<td style="text-align: center;">成交時間</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Fee</td>
<td style="text-align: center;">手續費</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">SettlementAMT</td>
<td style="text-align: center;">成交金額</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">含手續費</td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>USD:美元</p>
<p>HDK:港幣</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OVFutOrder 國外期貨委託回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-物件</strong></p>
<p>西元年</p></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">URO,JGL</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth</td>
<td style="text-align: center;">商品年月</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">200909</td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>“B”:買</p>
<p>“S”:賣</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託方式</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>LMT:限價單</p>
<p>MKT:市價單</p>
<p>STP:停損市價單</p>
<p>SWL:停損限價單</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">000116’21.75</td>
</tr>
<tr>
<td style="text-align: center;">TouchPrice</td>
<td style="text-align: center;">停損執行價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">000116’21.75</td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託口數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交口數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">狀態碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: left;"><p>0:傳輸中</p>
<p>5:預約單</p>
<p>10:委託失敗</p>
<p>20:委託成功</p>
<p>30:取消成功</p></td>
</tr>
<tr>
<td style="text-align: center;">AcceptDate</td>
<td style="text-align: center;">委託日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">AcceptTime</td>
<td style="text-align: center;">委託時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">ErrorNo</td>
<td style="text-align: center;">錯誤代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrorMessage</td>
<td style="text-align: center;">錯誤訊息</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">AA0484</td>
</tr>
<tr>
<td style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">Y :當沖</td>
</tr>
<tr>
<td style="text-align: center;">CancelFlag</td>
<td style="text-align: center;">可取消Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>‘Y’/’N’</p>
<p>盤中or 預約單才可取消</p></td>
</tr>
<tr>
<td style="text-align: center;">ReduceFlag</td>
<td style="text-align: center;">可減量Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>國際期貨目前無提供減量</p>
<p>‘P’:可改價</p></td>
</tr>
<tr>
<td style="text-align: center;">UtPrice</td>
<td style="text-align: center;">委託價格整數位</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>市價或市價停損單= 0</p>
<p>&lt;For 取消下單時使用&gt;</p></td>
</tr>
<tr>
<td style="text-align: center;">UtPrice2</td>
<td style="text-align: center;">委託價格分子</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">&lt;For 取消下單時使用&gt;</td>
</tr>
<tr>
<td style="text-align: center;">MinPrice2</td>
<td style="text-align: center;">委託價格分母</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">&lt;For 取消下單時使用&gt;</td>
</tr>
<tr>
<td style="text-align: center;">UtPrice4</td>
<td style="text-align: center;">停損執行價整數位</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>非停損單=0</p>
<p>&lt;For 取消下單時使用&gt;</p></td>
</tr>
<tr>
<td style="text-align: center;">UtPrice5</td>
<td style="text-align: center;">停損執行價格分子</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">&lt;For 取消下單時使用&gt;</td>
</tr>
<tr>
<td style="text-align: center;">UtPrice6</td>
<td style="text-align: center;">停損執行價格分母</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">&lt;For 取消下單時使用&gt;</td>
</tr>
<tr>
<td style="text-align: center;">TraditionFlag</td>
<td style="text-align: center;">傳統單Flag</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">‘Y” :傳統單</td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">BasketNo</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo1</td>
<td style="text-align: center;">市場代碼1</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode1</td>
<td style="text-align: center;">行情股票代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OVFutTrade 國外期貨成交回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">URO,JGL</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth</td>
<td style="text-align: center;">商品年月</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">200909</td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>“B”:買</p>
<p>“S”:賣</p></td>
</tr>
<tr>
<td style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交口數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderPrice</td>
<td style="text-align: center;">委託價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">000116’21.75</td>
</tr>
<tr>
<td style="text-align: center;">MatchPrice</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">000116’21.75</td>
</tr>
<tr>
<td style="text-align: center;">MatchDate</td>
<td style="text-align: center;">成交日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MatchTime</td>
<td style="text-align: center;">成交時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">AA0484</td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">交易幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
<tr>
<td style="text-align: center;">CurrencyType2</td>
<td style="text-align: center;">交割幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>NTD:台幣</p>
<p>USD:美元</p></td>
</tr>
</tbody>
</table>

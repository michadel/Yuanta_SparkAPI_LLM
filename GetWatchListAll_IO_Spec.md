<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 1%" />
<col style="width: 21%" />
<col style="width: 2%" />
<col style="width: 21%" />
<col style="width: 2%" />
<col style="width: 28%" />
</colgroup>
<thead>
<tr>
<th colspan="7" style="text-align: center;"><div data-custom-style="header">
<p><strong>Service Input - Output Specification</strong></p>
</div></th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
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
<td colspan="2" style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><strong>API GetWatchListAll</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>報價表查詢</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="6" style="text-align: center;"><strong>bool GetWatchListAll(Account, QuoteList, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td colspan="2" style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td colspan="2" style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">QuoteList</td>
<td colspan="2" style="text-align: center;">查詢商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;Quote&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">lng</td>
<td colspan="2" style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Quote 訂閱商品明細</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td colspan="2" style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StockCode</td>
<td colspan="2" style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>QueryWatchListResult 查詢報價表結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td colspan="2" style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">QueryWatchList</td>
<td colspan="2" style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;QueryWatchList&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>QueryWatchList 報價表物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td colspan="2" style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td colspan="2" style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td style="text-align: center;">StkName</td>
<td colspan="2" style="text-align: center;">股票名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-1"></h1></td>
</tr>
<tr>
<td style="text-align: center;">YstPrice</td>
<td colspan="2" style="text-align: center;">昨收價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-2"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OpenRefPrice</td>
<td colspan="2" style="text-align: center;">開盤參考價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-3"></h1></td>
</tr>
<tr>
<td style="text-align: center;">UpStopPrice</td>
<td colspan="2" style="text-align: center;">漲停價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-4"></h1></td>
</tr>
<tr>
<td style="text-align: center;">DownStopPrice</td>
<td colspan="2" style="text-align: center;">跌停價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-5"></h1></td>
</tr>
<tr>
<td style="text-align: center;">YstVol</td>
<td colspan="2" style="text-align: center;">昨量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-6"></h1></td>
</tr>
<tr>
<td style="text-align: center;">ExtName</td>
<td colspan="2" style="text-align: center;">擴充名</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-7"></h1></td>
</tr>
<tr>
<td style="text-align: center;">Decimal</td>
<td colspan="2" style="text-align: center;">小數位數</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><h1 id="section-8"></h1></td>
</tr>
<tr>
<td style="text-align: center;">CreditPercent</td>
<td colspan="2" style="text-align: center;">融資成數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="未提供回傳0">未提供,回傳0</h1></td>
</tr>
<tr>
<td style="text-align: center;">LenBondPercent</td>
<td colspan="2" style="text-align: center;">融券成數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="未提供回傳0-1">未提供,回傳0</h1></td>
</tr>
<tr>
<td style="text-align: center;">OpenPrice</td>
<td colspan="2" style="text-align: center;">開盤價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-9"></h1></td>
</tr>
<tr>
<td style="text-align: center;">HighPrice</td>
<td colspan="2" style="text-align: center;">最高價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-10"></h1></td>
</tr>
<tr>
<td style="text-align: center;">LowPrice</td>
<td colspan="2" style="text-align: center;">最低價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-11"></h1></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice</td>
<td colspan="2" style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="市價買999999999">市價買:999999999</h1></td>
</tr>
<tr>
<td style="text-align: center;">TotalOutVol</td>
<td colspan="2" style="text-align: center;">累計外盤量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-12"></h1></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice</td>
<td colspan="2" style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="市價賣-999999999">市價賣:-999999999</h1></td>
</tr>
<tr>
<td style="text-align: center;">TotalInVol</td>
<td colspan="2" style="text-align: center;">累計內盤量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-13"></h1></td>
</tr>
<tr>
<td style="text-align: center;">DealPrice</td>
<td colspan="2" style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-14"></h1></td>
</tr>
<tr>
<td style="text-align: center;">TotalDealAmt</td>
<td colspan="2" style="text-align: center;">總成交金額</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-15"></h1></td>
</tr>
<tr>
<td style="text-align: center;">VolFlag</td>
<td colspan="2" style="text-align: center;">單量內外盤標記</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><h1 id="內盤1外盤">0:內盤/1:外盤</h1></td>
</tr>
<tr>
<td style="text-align: center;">Vol</td>
<td colspan="2" style="text-align: center;">單量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="最高位元的bit">最高位元的Bit，</h1>
<h1 id="表示內外盤的旗標">表示內/外盤的旗標，</h1>
<h1 id="內盤1外盤-1">0:內盤/1:外盤</h1></td>
</tr>
<tr>
<td style="text-align: center;">TotalVol</td>
<td colspan="2" style="text-align: center;">總成交量</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-16"></h1></td>
</tr>
<tr>
<td style="text-align: center;">FixedPriceVol</td>
<td colspan="2" style="text-align: center;">定價量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-17"></h1></td>
</tr>
<tr>
<td style="text-align: center;">ReserveVol</td>
<td colspan="2" style="text-align: center;">未平倉量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-18"></h1></td>
</tr>
<tr>
<td style="text-align: center;">SettlementPrice</td>
<td colspan="2" style="text-align: center;">結算價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-19"></h1></td>
</tr>
<tr>
<td style="text-align: center;">HiContractPrice</td>
<td colspan="2" style="text-align: center;">合約高價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-20"></h1></td>
</tr>
<tr>
<td style="text-align: center;">LoContractPrice</td>
<td colspan="2" style="text-align: center;">合約低價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-21"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OrderBuyCount</td>
<td colspan="2" style="text-align: center;">委託買進總筆數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-22"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OrderBuyQty</td>
<td colspan="2" style="text-align: center;">委託買進總口數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-23"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OrderSellCount</td>
<td colspan="2" style="text-align: center;">委託賣出總筆數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-24"></h1></td>
</tr>
<tr>
<td style="text-align: center;">OrderSellQty</td>
<td colspan="2" style="text-align: center;">委託賣出總口數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-25"></h1></td>
</tr>
<tr>
<td style="text-align: center;">DealBuyCount</td>
<td colspan="2" style="text-align: center;">累計買進成交筆數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-26"></h1></td>
</tr>
<tr>
<td style="text-align: center;">DealSellCount</td>
<td colspan="2" style="text-align: center;">累計賣出成交筆數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-27"></h1></td>
</tr>
<tr>
<td style="text-align: center;">Volatility</td>
<td colspan="2" style="text-align: center;">波動率</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-28"></h1></td>
</tr>
<tr>
<td style="text-align: center;">Time</td>
<td colspan="2" style="text-align: center;">時間</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;">時間</td>
</tr>
<tr>
<td style="text-align: center;">TimeDiff</td>
<td colspan="2" style="text-align: center;">時差</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="台股為0晚正值早負值日本比台灣早一小時時差就是等於-1">台股為0，（晚＝正值，早＝負值）。日本比台灣早一小時，時差就是等於-1</h1></td>
</tr>
<tr>
<td style="text-align: center;">StkType2</td>
<td colspan="2" style="text-align: center;">屬性2</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><h1 id="bit-1-可轉換公司債">Bit 1: 可轉換公司債</h1>
<h1 id="bit-2-附認股權公司債">Bit 2: 附認股權公司債</h1>
<h1 id="bit-3-警示股">Bit 3: 警示股</h1>
<h1 id="bit-4-指數記號">Bit 4: 指數記號</h1>
<h1 id="bit-5-期貨">Bit 5: 期貨</h1>
<h1 id="bit-6-個股選擇權">Bit 6: 個股選擇權</h1>
<h1 id="bit-7-指數選擇權">Bit 7: 指數選擇權</h1>
<h1 id="bit-8-保留">Bit 8: 保留</h1></td>
</tr>
<tr>
<td style="text-align: center;">ReserveVolDiff</td>
<td colspan="2" style="text-align: center;">未平倉量增減</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-29"></h1></td>
</tr>
<tr>
<td style="text-align: center;">BelongCode</td>
<td colspan="2" style="text-align: center;">所屬產業分類碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="水泥工業">01: 水泥工業</h1>
<h1 id="食品工業">02: 食品工業</h1>
<h1 id="塑膠工業">03: 塑膠工業</h1></td>
</tr>
<tr>
<td style="text-align: center;">IndustryName</td>
<td colspan="2" style="text-align: center;">產業類股名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-30"></h1></td>
</tr>
<tr>
<td style="text-align: center;">PrincipalPercent</td>
<td colspan="2" style="text-align: center;">市值(%)</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="小數點兩位數單位">小數點兩位數(單位％)</h1></td>
</tr>
<tr>
<td style="text-align: center;">UpDownDay</td>
<td colspan="2" style="text-align: center;">連續漲跌(天)</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><h1 id="連續漲天數-連續跌天數">+：連續漲天數<br />
–：連續跌天數</h1></td>
</tr>
<tr>
<td style="text-align: center;">BidQty</td>
<td colspan="2" style="text-align: center;">第一買量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-31"></h1></td>
</tr>
<tr>
<td style="text-align: center;">AskQty</td>
<td colspan="2" style="text-align: center;">第一賣量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-32"></h1></td>
</tr>
<tr>
<td style="text-align: center;">PriceTrends</td>
<td colspan="2" style="text-align: center;">瞬間價格趨勢</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><h1 id="一般揭示">10: 一般揭示</h1>
<h1 id="暫緩撮合且瞬間趨跌">11: 暫緩撮合且瞬間趨跌</h1>
<h1 id="暫緩撮合且瞬間趨漲">12: 暫緩撮合且瞬間趨漲</h1>
<h1 id="試算後延後收盤">13: 試算後延後收盤</h1>
<h1 id="暫停交易">14: 暫停交易</h1>
<h1 id="恢復交易">15: 恢復交易</h1></td>
</tr>
<tr>
<td style="text-align: center;">EstDealPrice</td>
<td colspan="2" style="text-align: center;">盤前揭露價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-33"></h1></td>
</tr>
<tr>
<td style="text-align: center;">EstDealVol</td>
<td colspan="2" style="text-align: center;">盤前揭露量</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-34"></h1></td>
</tr>
<tr>
<td style="text-align: center;">EstDealVolFlag</td>
<td colspan="2" style="text-align: center;">盤前揭露量內外盤標記</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><h1 id="內盤1外盤-2">0:內盤/1:外盤</h1></td>
</tr>
</tbody>
</table>

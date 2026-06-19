<table style="width:100%;">
<colgroup>
<col style="width: 23%" />
<col style="width: 1%" />
<col style="width: 22%" />
<col style="width: 5%" />
<col style="width: 14%" />
<col style="width: 10%" />
<col style="width: 22%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>Project Name</strong></p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;"><strong>API GetStoreSummary</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>股票庫存綜合總表</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetStoreSummary(Account, lng)</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註1</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>StoreSummaryResult 查詢股票庫存總表結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkStoreList</td>
<td style="text-align: center;">現貨庫存清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkStore&gt;</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OVStkStoreList</td>
<td style="text-align: center;">國外股票庫存清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVStkStore&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>StkStore 現貨庫存物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-1"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeKind</td>
<td style="text-align: center;">交易種類</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="現股">0:現股 </h1>
<h1 id="資買">3:資買  </h1>
<h1 id="券賣">4:券賣 </h1>
<h1 id="借券">6:借券</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><h1 id="請參考api說明文件-列舉物件"><strong>請參考API說明文件-列舉物件</strong></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="上市上櫃">上市/上櫃</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-2"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName</td>
<td style="text-align: center;">股票名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-3"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StockQty</td>
<td style="text-align: center;">股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-4"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Price</td>
<td style="text-align: center;">成交均價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-5"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Cost</td>
<td style="text-align: center;">持有成本</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-6"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Interest</td>
<td style="text-align: center;">預估利息</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-7"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyNotInNos</td>
<td style="text-align: center;">買進未入帳股數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-8"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellNotInNos</td>
<td style="text-align: center;">賣出未入帳股數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-9"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradingQty</td>
<td style="text-align: center;">可交易股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-10"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Loan</td>
<td style="text-align: center;">資保證金/券擔保價品</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-11"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TaxRate</td>
<td style="text-align: center;">交易稅率</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="reits-股票">0:Reits 股票 </h1>
<h1 id="基金認股權證債券存託憑證">1:基金,認股權證,債券,存託憑證</h1>
<h1 id="一般股票-單位千分之一">3:一般股票<br />
(單位千分之一)</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LotSize</td>
<td style="text-align: center;">交易單位</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="每手股數">每手股數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice</td>
<td style="text-align: center;">市價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="盤前市價若為0則給開盤參考價">盤前市價若為0則給開盤參考價</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Decimal</td>
<td style="text-align: center;">小數位數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數">+為小數位數</h1>
<h1 id="為分數分母">-為分數分母</h1>
<h1 id="為整數">0為整數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType1</td>
<td style="text-align: center;">屬性1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="bit-1-管理商品">Bit 1: 管理商品</h1>
<h1 id="bit-2-交易記號">Bit 2: 交易記號</h1>
<h1 id="bit-3-受益憑證">Bit 3: 受益憑證</h1>
<h1 id="bit-4-etf商品">Bit 4: ETF商品</h1>
<h1 id="bit-5-權證記號">Bit 5: 權證記號</h1>
<h1 id="bit-6-特別股">Bit 6: 特別股</h1>
<h1 id="bit-7-存託憑證">Bit 7: 存託憑證</h1>
<h1 id="bit-8-外國股票">Bit 8: 外國股票</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType2</td>
<td style="text-align: center;">屬性2</td>
<td colspan="2" style="text-align: center;">Int</td>
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
<td colspan="2" style="text-align: center;">BuyPrice</td>
<td style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-12"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice</td>
<td style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-13"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">UpStopPrice</td>
<td style="text-align: center;">漲停價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-14"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DownStopPrice</td>
<td style="text-align: center;">跌停價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-15"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">PriceMultiplier</td>
<td style="text-align: center;">計價倍數</td>
<td colspan="2" style="text-align: center;">uint</td>
<td colspan="2" style="text-align: center;"><h1 id="乘1倍">1，乘1倍</h1>
<h1 id="乘10倍">10，乘10倍</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="twd">TWD</h1>
<h1 id="cny">CNY</h1>
<h1 id="hkd">HKD</h1>
<h1 id="usd">USD</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CDQTY</td>
<td style="text-align: center;">借貸股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-16"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OddTradingQty</td>
<td style="text-align: center;">零股可下單股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-17"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ReturnAmt</td>
<td style="text-align: center;">未實現損益</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-18"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketAmt</td>
<td style="text-align: center;">股票市值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-19"></h1></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>OVStkStore 國外股票庫存物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">現貨帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-20"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="usd美元">USD:美元</h1>
<h1 id="hkd港幣">HKD:港幣</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><h1 id="請參考api說明文件-列舉物件-1"><strong>請參考API說明文件-列舉物件</strong></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketName</td>
<td style="text-align: center;">市場名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-21"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-22"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName</td>
<td style="text-align: center;">股票名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-23"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkFullName</td>
<td style="text-align: center;">股票全名</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-24"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StockQty</td>
<td style="text-align: center;">庫存股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-25"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradingQty</td>
<td style="text-align: center;">可交易股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-26"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Price</td>
<td style="text-align: center;">成交均價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-27"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Cost</td>
<td style="text-align: center;">持有成本</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-28"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CloseRate</td>
<td style="text-align: center;">匯率</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-29"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">RateKind</td>
<td style="text-align: center;">匯率運算模式</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="除以匯率">1:除以匯率</h1>
<h1 id="乘以匯率">2:乘以匯率</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LotSize</td>
<td style="text-align: center;">交易單位</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="每手股數-1">每手股數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice</td>
<td style="text-align: center;">市價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="固定為0前端自行根據登入權限查詢">固定為0,前端自行根據登入權限查詢</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Decimal</td>
<td style="text-align: center;">小數位數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數-1">+為小數位數</h1>
<h1 id="為分數分母-1">-為分數分母</h1>
<h1 id="為整數-1">0為整數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyPrice</td>
<td style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-30"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice</td>
<td style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-31"></h1></td>
</tr>
</tbody>
</table>

註1：限證券使用

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 3%" />
<col style="width: 21%" />
<col style="width: 2%" />
<col style="width: 19%" />
<col style="width: 5%" />
<col style="width: 26%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p>1467140D (20.103.20.13)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;">API GetFutStoreSummary</td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;">期貨庫存總表查詢</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetFutStoreSummary(Account, lng)</strong></td>
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
<td colspan="2" style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Lng</td>
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
<td colspan="7" style="text-align: center;"><strong>FutStoreSummaryResult 查詢期貨庫存總表結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">FutStoreList</td>
<td style="text-align: center;">期貨庫存清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutStore&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>FutStore 期貨庫存物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">FutAccount</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Kind</td>
<td style="text-align: center;">期權別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">期貨(F)/選擇權(O)/期貨+選擇權(C)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Trid</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">TX109100E4/TXO09000E4</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">買(B)/賣(S)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Qty</td>
<td style="text-align: center;">未平倉口數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Amt</td>
<td style="text-align: center;">總成交點數</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Fee</td>
<td style="text-align: center;">手續費</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Tax</td>
<td style="text-align: center;">交易稅</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">NTD:台幣</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">“Y”:當沖 “ ”:空白</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Commodity1</td>
<td style="text-align: center;">商品代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">TXO</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CallPut1</td>
<td style="text-align: center;">買賣權1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">C/P</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">商品月份1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">200712</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">買(B)/賣(S)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo1</td>
<td style="text-align: center;">市場代碼1</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode1</td>
<td style="text-align: center;">行情報價代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">7799,TXO04600A9</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Commodity2</td>
<td style="text-align: center;">商品代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">TXO</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CallPut2</td>
<td style="text-align: center;">買賣權2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">C/P</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">商品月份2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">200712</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">買(B)/賣(S)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName2</td>
<td style="text-align: center;">股票名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo2</td>
<td style="text-align: center;">市場代碼2</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode2</td>
<td style="text-align: center;">行情報價代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">7799,TXO04700A9</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyPrice1</td>
<td style="text-align: center;">買入價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice1</td>
<td style="text-align: center;">賣出價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice1</td>
<td style="text-align: center;">市價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">盤前市價若為0 則給開盤參考價</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyPrice2</td>
<td style="text-align: center;">買入價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice2</td>
<td style="text-align: center;">賣出價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice2</td>
<td style="text-align: center;">市價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">盤前市價若為0 則給開盤參考價</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Decimal</td>
<td style="text-align: center;">小數位數</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數-為分數分母">+為小數位數,-為分數分母,</h1>
<h1 id="為整數">0為整數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ProductType1</td>
<td style="text-align: center;">商品類別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">“F”:期貨 “O”:選擇權</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ProductKind1</td>
<td style="text-align: center;">商品屬性1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>“I”:指數 “R”:利率 “B”:債券</p>
<p>“C”:商品 “S”:股票</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ProductType2</td>
<td style="text-align: center;">商品類別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">“F”:期貨 “O”:選擇權</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ProductKind2</td>
<td style="text-align: center;">商品屬性2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>“I”:指數 “R”:利率 “B”:債券</p>
<p>“C”:商品 “S”:股票</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">UpStopPrice1</td>
<td style="text-align: center;">漲停價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DownStopPrice1</td>
<td style="text-align: center;">跌停價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">UpStopPrice2</td>
<td style="text-align: center;">漲停價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DownStopPrice2</td>
<td style="text-align: center;">跌停價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode1opp</td>
<td style="text-align: center;">行情股票代碼1反向</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">&lt;第1支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode2opp</td>
<td style="text-align: center;">行情股票代碼2反向</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">&lt;第2支腳&gt;</td>
</tr>
</tbody>
</table>

註1：限期貨使用

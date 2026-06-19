<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 4%" />
<col style="width: 21%" />
<col style="width: 5%" />
<col style="width: 14%" />
<col style="width: 4%" />
<col style="width: 29%" />
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
<td colspan="3" style="text-align: center;"><strong>API GetOVFutStoreSummary</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>國際期貨庫存總表查詢</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetOVFutStoreSummary(Account, lng)</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Field Name</strong></td>
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
<td colspan="2" style="text-align: left;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>OVFutStoreSummaryResult 查詢國際期貨庫存總表結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OVFutStoreList</td>
<td style="text-align: center;">國際期貨庫存清單</td>
<td colspan="2" style="text-align: center;">List&lt;OVFutStore&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>OVFutStore 國際期貨庫存物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">FutAccount</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Kind</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">期貨(F)/選擇權(O)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Trid</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
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
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Amt</td>
<td style="text-align: center;">總成交點數</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Commodity1</td>
<td style="text-align: center;">商品代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">EC, URO</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CallPut1</td>
<td style="text-align: center;">買賣權1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">C/P</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">交易月份1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">201101</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">中文名稱</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Commodity2</td>
<td style="text-align: center;">商品代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">EC</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CallPut2</td>
<td style="text-align: center;">買賣權2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">C/P</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">交易月份2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: left;">201101</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName2</td>
<td style="text-align: center;">商品名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">中文名稱</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
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
<td colspan="2" style="text-align: center;">CurrencyType</td>
<td style="text-align: center;">幣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">AUD澳幣,EUR歐元,GBP英鎊,HKD港幣,JPY日幣,NTD新台幣,SGD新加坡幣,USD美金</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">“Y”:當沖 “ ”:空白</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">買(B)/賣(S)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">買(B)/賣(S)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OptProdKind1</td>
<td style="text-align: center;">選擇權商品種類1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>&lt;第1支腳&gt;<br />
"0":期貨選擇權</p>
<p>"1":現貨選擇權</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OptProdKind2</td>
<td style="text-align: center;">選擇權商品種類2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>&lt;第2支腳&gt;<br />
“0”:期貨選擇權</p>
<p>“1”:現貨選擇權</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo1</td>
<td style="text-align: center;">市場代碼1</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>&lt;第1支腳&gt;</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode1</td>
<td style="text-align: center;">行情報價代碼1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">&lt;第1支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo2</td>
<td style="text-align: center;">市場代碼2</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>&lt;第2支腳&gt;</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode2</td>
<td style="text-align: center;">行情股票代碼2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">&lt;第2支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyPrice1</td>
<td style="text-align: center;">買入價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">&lt;第1支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice1</td>
<td style="text-align: center;">賣出價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;">&lt;第1支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice1</td>
<td style="text-align: center;">市價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">&lt;第1支腳&gt;<br />
盤前市價若為0 則給開盤參考價</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BuyPrice2</td>
<td style="text-align: center;">買入價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">&lt;第2支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SellPrice2</td>
<td style="text-align: center;">賣出價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">&lt;第2支腳&gt;</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketPrice2</td>
<td style="text-align: center;">市價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">&lt;第2支腳&gt;<br />
盤前市價若為0 則給開盤參考價</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Decimal</td>
<td style="text-align: center;">小數位數</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數-為分數分母">+為小數位數,-為分數分母,</h1>
<h1 id="為整數">0為整數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Decimal2</td>
<td style="text-align: center;">小數位數2</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數-為分數分母-1">+為小數位數,-為分數分母,</h1>
<h1 id="為整數-1">0為整數</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TickDiff</td>
<td style="text-align: center;">檔差</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="檔差不是固定的就為0例如台股都為0海外股票跟海外期貨預留用的若檔差是0.05且他的小數位是3位檔差就是50">檔差不是固定的就為0，例如台股都為0；海外股票跟海外期貨預留用的；若檔差是0.05，且他的小數位是3位，檔差就是50</h1></td>
</tr>
</tbody>
</table>

註1：限期貨使用

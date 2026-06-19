<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 22%" />
<col style="width: 7%" />
<col style="width: 18%" />
<col style="width: 2%" />
<col style="width: 27%" />
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
<td colspan="2" style="text-align: center;"><strong>API GetHisRealizedGainLoss</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>已實現損益查詢</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetHisRealizedGainLoss(Account, SDate, EDate, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註1</p></td>
</tr>
<tr>
<td style="text-align: center;">SDate</td>
<td style="text-align: center;">查詢起始日</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>yyyy/MM/dd</p>
<p>註2</p></td>
</tr>
<tr>
<td style="text-align: center;">EDate</td>
<td style="text-align: center;">查詢結束日</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>yyyy/MM/dd</p>
<p>註2</p></td>
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
<td colspan="6" style="text-align: center;"><strong>RealizedGainLossResult 已實現損益查詢結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">RealizedGainLossList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;RealizedGainLoss&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>RealizedGainLoss 已實現損益物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Account</p>
</div></td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>TradeDate</p>
</div></td>
<td style="text-align: center;">成交日</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>TradeKind</p>
</div></td>
<td style="text-align: center;">交易種類</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"><p>'0' 現股</p>
<p>'1' 代資</p>
<p>'2' 代券</p>
<p>'3'融資</p>
<p>'4' 融券</p>
<p>'5','6' 借券</p>
<p>7:資沖</p>
<p>8:券沖</p>
<p>17:現股當沖買</p>
<p>18:現股當沖賣</p></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Price</p>
</div></td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>double</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Qty</p>
</div></td>
<td style="text-align: center;">成交股數</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>ProfitLoss</p>
</div></td>
<td style="text-align: center;">損益</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>OrderNo</p>
</div></td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>TermSplit</p>
</div></td>
<td style="text-align: center;">委託書號分單號</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>TermExt</p>
</div></td>
<td style="text-align: center;">委託書號延長碼</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Charge</p>
</div></td>
<td style="text-align: center;">手續費</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Cost</p>
</div></td>
<td style="text-align: center;">持有成本</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Tax</p>
</div></td>
<td style="text-align: center;">交易稅</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>TotalAMT</p>
</div></td>
<td style="text-align: center;">成交價金</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限證券使用

註2：限提供近2年資料，查詢起訖日區間不得超過1年

<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 22%" />
<col style="width: 20%" />
<col style="width: 4%" />
<col style="width: 30%" />
</colgroup>
<thead>
<tr>
<th colspan="5" style="text-align: center;"><div data-custom-style="header">
<p><strong>Service Input - Output Specification</strong></p>
</div></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>Project Name</strong></p>
</div></td>
<td style="text-align: center;"></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td style="text-align: center;"></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td style="text-align: center;">API GetQuoteList</td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;">取得己訂閱即時報價商品清單</td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="4" style="text-align: center;"><strong>bool GetQuoteList(Account)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">訂閱帳號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>SubQuoteListResult 訂閱商品清單回傳結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">QuoteList</td>
<td style="text-align: center;">訂閱商品清單</td>
<td style="text-align: center;">List&lt;Quote&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Quote 訂閱商品明細</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: left;"><div data-custom-style="Default">
<p><strong>請參考API說明文件-列舉物件</strong></p>
</div></td>
</tr>
<tr>
<td style="text-align: center;">StockCode</td>
<td style="text-align: center;">商品代碼</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

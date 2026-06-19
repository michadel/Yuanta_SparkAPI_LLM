<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 19%" />
<col style="width: 8%" />
<col style="width: 20%" />
<col style="width: 1%" />
<col style="width: 26%" />
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
<td colspan="2" style="text-align: center;"><strong>API GetStockInformation</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>標的資訊查詢</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetStockInformation(Account, StkList, lng)</strong></td>
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
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">StkList</td>
<td style="text-align: center;">查詢商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkInfo&gt;</td>
<td colspan="2" style="text-align: center;"></td>
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
<td colspan="6" style="text-align: center;"><strong>StkInfo 標的資訊</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StockCode</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StkInformationResult 標的資訊查詢結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">StockInformationList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkInformation&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StkInformation 標的資訊物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StockCode</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td style="text-align: center;">Dayoffmark</td>
<td style="text-align: center;">可否當沖</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"X"：現股當沖</p>
<p>"Y"：現股當沖(暫停先賣後買)</p>
<p>其他：不可現股當沖</p></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Creditpercent</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>融資成數</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Lendpercent</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>融券成數</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Creditremnants</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>融資餘額</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"><p>999999：無限制</p>
<p>-1：停資</p>
<p>-2：有限制</p></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Lendremnants</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>融券餘額</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"><p>999999：無限制</p>
<p>-1：停券</p>
<p>0：無券</p></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>LendSellMark</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>平盤下可放空</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;"><p>"N"：不可放空</p>
<p>"Y"：可放空</p></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>RecallDate</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>融券回補日期</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;">yyyyMMdd民國年</td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>LendQty</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>借賣配額</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>long</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>StockWarning</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>股票警示狀態</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>List&lt;enumStkWarningType&gt;</p>
</div></td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>UpdateDate</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>更新日期</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;">yyyyMMdd民國年</td>
</tr>
</tbody>
</table>

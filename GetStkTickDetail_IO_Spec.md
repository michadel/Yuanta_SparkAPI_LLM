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
<td colspan="2" style="text-align: center;"><strong>API GetStkTickDetail</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>當日分時明細查詢</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>bool GetStkTickDetail</strong></p>
<p><strong>(Account, MarketType, StkCode</strong>, <strong>SelectType, Stime, Etime, LastCount, lng)</strong></p></td>
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
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SelectType</td>
<td style="text-align: center;">查詢種類</td>
<td colspan="2" style="text-align: center;">enumStkTickSelectType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Stime</td>
<td style="text-align: center;">開始時間</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><strong>預設為00:00:00</strong></td>
</tr>
<tr>
<td style="text-align: center;">Etime</td>
<td style="text-align: center;">結束時間</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><strong>預設為23:59:59</strong></td>
</tr>
<tr>
<td style="text-align: center;">LastCount</td>
<td style="text-align: center;">最後筆數</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><strong>預設為20</strong></td>
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
<td colspan="6" style="text-align: center;"><strong>StickDetailResult 當日分時明細查詢結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
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
<td style="text-align: center;">StickDetailList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;StickDetail&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StickDetail 當日分時明細物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">TimeStamp</td>
<td style="text-align: center;">時間</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>DealPrice</p>
</div></td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>double</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>DealVol</p>
</div></td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>BuyPrice</p>
</div></td>
<td style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>SellPrice</p>
</div></td>
<td style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>SeqNo</p>
</div></td>
<td style="text-align: center;">序號</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>InOutFlag</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>內外盤</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>int</p>
</div></td>
<td colspan="2" style="text-align: center;"><p>0:內盤</p>
<p>1:外盤</p></td>
</tr>
</tbody>
</table>

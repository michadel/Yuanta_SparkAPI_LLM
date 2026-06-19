<table>
<colgroup>
<col style="width: 17%" />
<col style="width: 20%" />
<col style="width: 13%" />
<col style="width: 16%" />
<col style="width: 8%" />
<col style="width: 23%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Name</strong></p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p>D20A4610 (210.10.70.16)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><p>API SubscribeStockInformation</p>
<p>API UnSubscribeStockInformation</p></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>個股其他資訊訂閱</p>
<p>個股其他資訊解訂閱</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>bool SubscribeStockInformation(LoginAcno, LstStockInfo, Lng)</strong></p>
<p><strong>bool UnSubscribeStockInformation(LoginAcno, LstStockInfo, Lng)</strong></p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">訂閱帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">LstStockInfo</td>
<td style="text-align: center;">訂閱商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;StockOtherInformation&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StockOtherInformation 個股其他資訊物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><mark>StockCode</mark></td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StockOtherInfoResult 個股其他資訊回傳結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Key</td>
<td style="text-align: center;">鍵值</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">MarketNo+StkCode (不足補0)</td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag</td>
<td style="text-align: center;">索引值</td>
<td colspan="2" style="text-align: center;">enumQuoteStkInfoIndexType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>僅提供<strong>試搓成交時間</strong></p></td>
</tr>
<tr>
<td style="text-align: center;">TradeTime</td>
<td style="text-align: center;">試搓成交時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
</tbody>
</table>

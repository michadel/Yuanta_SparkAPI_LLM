<table style="width:100%;">
<colgroup>
<col style="width: 18%" />
<col style="width: 4%" />
<col style="width: 20%" />
<col style="width: 13%" />
<col style="width: 12%" />
<col style="width: 6%" />
<col style="width: 24%" />
</colgroup>
<thead>
<tr>
<th colspan="7" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p><strong>Service Input - Output Specification</strong></p>
</blockquote>
</div></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>Project Name</strong></p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p>TCBus(.Net)</p>
</blockquote>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p><strong>製作者</strong></p>
</blockquote>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p>D20A460F (210.10.70.15)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p><strong>製作日期</strong></p>
</blockquote>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p>API SubscribeMarketInformation</p>
</blockquote>
</div>
<div data-custom-style="header">
<blockquote>
<p>API UnSubscribeMarketInformation</p>
</blockquote>
</div></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>個股盤前資訊訂閱</p>
<p>個股盤前資訊解訂閱</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>bool SubscribeMarketInformation(LoginAcno, LstMarketInfo, Lng)</strong></p>
<p><strong>bool UnSubscribeMarketInformation(LoginAcno, LstMarketInfo, Lng)</strong></p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">訂閱帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LstMarketInfo</td>
<td style="text-align: center;">訂閱商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;MarketInformation&gt;</td>
<td colspan="2" style="text-align: center;"></td>
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
<td colspan="7" style="text-align: center;"><strong>MarketInformation 個股盤前資訊物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><mark>StockCode</mark></td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>MarketInfoResult 個股盤前資訊回傳結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Key</td>
<td style="text-align: center;">鍵值</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">MarketNo+StkCode (不足補0)</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DealPrice</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TickVol</td>
<td style="text-align: center;"><ol>
<li><p>單量</p></li>
</ol></td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><p>最高位元的Bit，表示內/外盤的旗標</p>
<p>0:內盤/1:外盤</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Time</td>
<td style="text-align: center;">時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeStatus</td>
<td style="text-align: center;">交易狀態</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>0 : 初始狀態</p>
<p>1 : 收單階段</p>
<p>2 : 不可刪單階段</p>
<p>3 : 集合競價階段</p></td>
</tr>
</tbody>
</table>

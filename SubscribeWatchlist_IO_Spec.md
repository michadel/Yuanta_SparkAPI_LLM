<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 26%" />
<col style="width: 23%" />
<col style="width: 30%" />
</colgroup>
<thead>
<tr>
<th colspan="4" style="text-align: center;"><div data-custom-style="header">
<p><strong>Service Input - Output Specification</strong></p>
</div></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>Project Name</strong></p>
</div></td>
<td style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td style="text-align: center;"><div data-custom-style="header">
<p>D20A460B (210.10.70.11)</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td style="text-align: center;"><p>API SubscribeWatchlist</p>
<p>API UnSubscribeWatchlist</p></td>
<td style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>行情報價表訂閱(指定欄位)</p>
<p>行情報價表解訂閱(指定欄位)</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="3" style="text-align: center;"><p><strong>bool SubscribeWatchlist(LoginAcno, LstWatchlist,</strong> <strong>Lng)</strong></p>
<p><strong>bool UnSubscribeWatchlist(LoginAcno, LstWatchlist,</strong> <strong>Lng)</strong></p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">訂閱帳號</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">LstWatchlist</td>
<td style="text-align: center;">訂閱商品清單</td>
<td style="text-align: center;">List&lt;Watchlist&gt;</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Lng</td>
<td style="text-align: center;">語系</td>
<td style="text-align: center;">enumLangType</td>
<td style="text-align: center;"><p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>Watchlist 行情報價表(指定欄位)物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag</td>
<td style="text-align: center;">訂閱報價欄位</td>
<td style="text-align: center;">enumQuoteIndexType</td>
<td style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td style="text-align: center;">enumMarketType</td>
<td style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><mark>StockCode</mark></td>
<td style="text-align: center;">商品代碼</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>WatchListResult 行情報價表訂閱(指定欄位)回傳結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Key</td>
<td style="text-align: center;">鍵值</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>IndexFlag+MarketNo</p>
<p>+StkCode (不足補0)</p></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td style="text-align: center;">enumMarketType</td>
<td style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代碼</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag</td>
<td style="text-align: center;">索引值</td>
<td style="text-align: center;">enumQuoteIndexType</td>
<td style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Value</td>
<td style="text-align: center;">資料值</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"><p><strong>此值定義請參考IndexFlag</strong></p>
<p>IndexFlag=買價</p>
<p>市價買:999999999</p>
<p>IndexFlag=賣價</p>
<p>市價賣:-999999999</p>
<p>IndexFlag=單量</p>
<p>最高位元的Bit,表示內/外盤的旗標,0-內盤/1-外盤</p>
<p>IndexFlag=delay一秒的成交價</p>
<p>海外股無此資料,請使用索引值=7的成交價</p>
<p>IndexFlag=瞬間價格趨勢</p>
<p>10:一般揭示</p>
<p>11:暫緩撮合且瞬間趨跌</p>
<p>12:暫緩撮合且瞬間趨漲</p>
<p>13:試算後延後收盤</p>
<p>14:暫停交易</p>
<p>15:恢復交易</p>
<p>16:試算後延後開盤</p>
<p>IndexFlag=交易狀態</p>
<p>0x00:初始狀態</p>
<p>0x01:收單階段</p>
<p>0x02:不可刪單階段</p>
<p>0x03:集合競價階段</p>
<p>IndexFlag=試撮量</p>
<p>最高位元的Bit,表示內/外盤的旗標,</p>
<p>0:內盤/1:外盤</p></td>
</tr>
</tbody>
</table>

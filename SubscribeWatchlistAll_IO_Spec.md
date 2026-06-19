<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 1%" />
<col style="width: 21%" />
<col style="width: 11%" />
<col style="width: 12%" />
<col style="width: 8%" />
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="2" style="text-align: center;">620A460A (98.10.70.10)</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><p>API SubscribeWatchlistAll</p>
<p>API UnSubscribeWatchlistAll</p></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>行情報價表訂閱</p>
<p>行情報價表解訂閱</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="6" style="text-align: center;"><p><strong>bool SubscribeWatchlistAll(LoginAcno, LstWatchlistAll, Lng)</strong></p>
<p><strong>bool UnSubscribeWatchlistAll(LoginAcno, LstWatchlistAll, Lng)</strong></p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td colspan="2" style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td colspan="2" style="text-align: center;">訂閱帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">LstWatchlistAll</td>
<td colspan="2" style="text-align: center;">訂閱商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;WatchlistAll&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Lng</td>
<td colspan="2" style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>WatchlistAll 行情報價表物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td colspan="2" style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><h1 id="請參考api說明文件-列舉物件"><strong>請參考API說明文件-列舉物件</strong></h1></td>
</tr>
<tr>
<td style="text-align: center;"><mark>StockCode</mark></td>
<td colspan="2" style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>WatchListAllResult 行情報價表訂閱回傳結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td colspan="2" style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Key</td>
<td colspan="2" style="text-align: center;">鍵值</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">MarketNo+StkCode (不足補0)</td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td colspan="2" style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td colspan="2" style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SeqNo</td>
<td colspan="2" style="text-align: center;">序號</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><p>090000000000</p>
<p>後八碼代表序號，前四碼代表時間</p></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag</td>
<td colspan="2" style="text-align: center;">索引值</td>
<td colspan="2" style="text-align: center;">enumQuoteIndexType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Value</td>
<td colspan="2" style="text-align: center;">資料值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><p><strong>此值定義請參考IndexFlag<br />
</strong>若IndexFlag=IndexFlag22、IndexFlag28、IndexFlag29則無值</p>
<p>IndexFlag=瞬間價格趨勢</p>
<p>10: 一般揭示</p>
<p>11: 暫緩撮合且瞬間趨跌</p>
<p>12: 暫緩撮合且瞬間趨漲</p>
<p>13: 試算後延後收盤</p>
<p>14: 暫停交易</p>
<p>15: 恢復交易</p>
<p>16: 試算後延後開盤</p>
<p>IndexFlag=交易狀態</p>
<p>0x00: 初始狀態</p>
<p>0x01: 收單階段</p>
<p>0x02: 不可刪單階段</p>
<p>0x03: 集合競價階段</p>
<p>IndexFlag=試撮量</p>
<p>最高位元的Bit,表示內/外盤的旗標,</p>
<p>0:內盤/1:外盤</p></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_22</td>
<td colspan="2" style="text-align: center;">訂閱報價表Flag22</td>
<td colspan="2" style="text-align: center;">WatchListAll_Flag22</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag22才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_28</td>
<td colspan="2" style="text-align: center;">訂閱報價表Flag28</td>
<td colspan="2" style="text-align: center;">WatchListAll_Flag28</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag28才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_29</td>
<td colspan="2" style="text-align: center;">訂閱報價表Flag29</td>
<td colspan="2" style="text-align: center;">WatchListAll_Flag29</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag29才有值</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>WatchListAll_Flag22 訂閱報價表IndexFlag22物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol</td>
<td colspan="2" style="text-align: center;">第一買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol</td>
<td colspan="2" style="text-align: center;">第一賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>WatchListAll_Flag28 訂閱報價表IndexFlag28物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice</td>
<td colspan="2" style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">市價買:999999999</td>
</tr>
<tr>
<td style="text-align: center;">SellPrice</td>
<td colspan="2" style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">市價賣:-999999999</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>WatchListAll_Flag29 訂閱報價表IndexFlag29物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Time</td>
<td colspan="2" style="text-align: center;">時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalOutVol</td>
<td colspan="2" style="text-align: center;">累計外盤量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalInVol</td>
<td colspan="2" style="text-align: center;">累計內盤量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Deal</td>
<td colspan="2" style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol</td>
<td colspan="2" style="text-align: center;">單量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><p>最高位元的Bit，表示內/外盤的旗標，</p>
<p>0:內盤/1:外盤</p></td>
</tr>
<tr>
<td style="text-align: center;">TotalVol</td>
<td colspan="2" style="text-align: center;">總成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">海外期貨之現貨單位是千股</td>
</tr>
<tr>
<td style="text-align: center;">TotalAmt</td>
<td colspan="2" style="text-align: center;">總成交金額</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">單位萬元</td>
</tr>
</tbody>
</table>

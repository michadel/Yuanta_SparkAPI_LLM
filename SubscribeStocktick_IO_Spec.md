<table style="width:100%;">
<colgroup>
<col style="width: 19%" />
<col style="width: 20%" />
<col style="width: 13%" />
<col style="width: 6%" />
<col style="width: 12%" />
<col style="width: 26%" />
</colgroup>
<thead>
<tr>
<th colspan="6" style="text-align: center;"><div data-custom-style="header">
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p>TCBus(.Net)</p>
</blockquote>
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p>D20A280A (210.10.40.10)</p>
</blockquote>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<blockquote>
<p>API SubscribeStockTick<br />
API UnSubscribeStockTick</p>
</blockquote>
</div></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>分時明細訂閱</p>
<p>分時明細解訂閱</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>bool SubscribeStockTick(LoginAcno, LstStocktick, Lng)</strong></p>
<p><strong>bool UnSubscribeStockTick(LoginAcno, LstStocktick, Lng)</strong></p></td>
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
<td style="text-align: center;">LstStocktick</td>
<td style="text-align: center;">訂閱商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;Stocktick&gt;</td>
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
<td colspan="6" style="text-align: center;"><strong>Stocktick 分時明細物件</strong></td>
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
<td colspan="6" style="text-align: center;"><strong>StockTickResult 分時明細回傳結果</strong></td>
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
<td style="text-align: center;">SerialNo</td>
<td style="text-align: center;">序號</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><p>以股票代碼個別編序號,從1開始</p>
<p>-1代表商品清盤</p></td>
</tr>
<tr>
<td style="text-align: center;">Time</td>
<td style="text-align: center;">時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice</td>
<td style="text-align: center;">買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><p>當SerialNo=-1時,此欄位代表漲停價</p>
<p>市價買:999999999</p></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice</td>
<td style="text-align: center;">賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><p>當SerialNo=-1時,此欄位代表跌停價</p>
<p>市價賣:-999999999</p></td>
</tr>
<tr>
<td style="text-align: center;">DealPrice</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">當SerialNo=-1時,此欄位代表開盤參考價</td>
</tr>
<tr>
<td style="text-align: center;">DealVol</td>
<td style="text-align: center;">成交量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">海外期貨之現貨單位是千股</td>
</tr>
<tr>
<td style="text-align: center;">InOutFlag</td>
<td style="text-align: center;">內外盤註記</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>0:內盤</p>
<p>1:外盤</p>
<p>2:定價內盤</p>
<p>3:定價外盤</p>
<p>10:一般揭示</p>
<p>11:暫緩撮合且瞬間趨跌</p>
<p>12:暫緩撮合且瞬間趨漲</p>
<p>13:試算後延後收盤</p>
<p>14:暫停交易</p>
<p>15:恢復交易</p>
<p>註1：當是10,11,12,13時,只有市場碼與股票代碼有值,其餘的欄位皆是0</p>
<p>註2：當是14,15時,只有市場碼、股票代碼與時間有值,其餘的欄位皆是0</p></td>
</tr>
<tr>
<td style="text-align: center;">Type</td>
<td style="text-align: center;">明細類別</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;">0:Normal</td>
</tr>
</tbody>
</table>

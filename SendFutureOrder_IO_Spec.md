<table style="width:100%;">
<colgroup>
<col style="width: 23%" />
<col style="width: 22%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 7%" />
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
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><strong>API SendFutureOrder</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>國內期貨下單</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool SendFutureOrder(LoginAcno, lstFutureOrder, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">下單帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)</p>
<p>例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td style="text-align: center;">lstFutureOrder</td>
<td style="text-align: center;">下單物件清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutureOrder&gt;</td>
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
<td colspan="6" style="text-align: center;"><strong>FutureOrder 國內期貨下單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Identity</td>
<td style="text-align: center;">識別碼</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">下單帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託書編號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">委託新單不需填</td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日期</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;">FunctionCode</td>
<td style="text-align: center;">功能別</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><p>00:委託單</p>
<p>04:取消</p>
<p>05:改量</p>
<p>07:改價</p>
<p>(Opt複式單沒有改價)</p></td>
</tr>
<tr>
<td style="text-align: center;">CommodityID1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>請參考 FunctionList.xlsx</p>
<p>股名檔對照表的下單代碼</p>
<p>如:台指🡪FITX</p>
<p>如:台指選🡪TXO</p></td>
</tr>
<tr>
<td style="text-align: center;">CallPut1</td>
<td style="text-align: center;">買賣權1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"C":Call</p>
<p>"P":Put<br />
(選擇權才需填值)</p></td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">商品月份1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">如:201912</td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">委託價格</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">非限價請填0</td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty1</td>
<td style="text-align: center;">委託口數1</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySell1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"B":買</p>
<p>"S":賣</p></td>
</tr>
<tr>
<td style="text-align: center;">CommodityID2</td>
<td style="text-align: center;">商品名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CallPut2</td>
<td style="text-align: center;">買賣權2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"C":Call</p>
<p>"P":Put<br />
(選擇權才需填值)</p></td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">商品月份2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">如:201912</td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty2</td>
<td style="text-align: center;">委託口數2</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySell2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"B":買</p>
<p>"S":賣</p></td>
</tr>
<tr>
<td style="text-align: center;">OpenOffsetKind</td>
<td style="text-align: center;">新平倉</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>0:新倉</p>
<p>1:平倉</p>
<p>2:自動</p></td>
</tr>
<tr>
<td style="text-align: center;">DayTradeID</td>
<td style="text-align: center;">當沖註記</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"Y":當沖</p>
<p>" ":空白</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託方式</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>1:市價</p>
<p>2:限價</p>
<p>3:範圍市價</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderCond</td>
<td style="text-align: center;">委託條件</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>" ":ROD</p>
<p>I:FOK</p>
<p>2:IOC</p></td>
</tr>
<tr>
<td style="text-align: center;">SellerNo</td>
<td style="text-align: center;">營業員代碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;">請填0</td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">BasketNo</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><strong>目前無作用</strong></td>
</tr>
<tr>
<td style="text-align: center;">Session</td>
<td style="text-align: center;">盤別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>1:預約</p>
<p>其他:盤中單</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutOrderResult 國內期貨下單結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">ResultCount</td>
<td style="text-align: center;">交易狀態</td>
<td colspan="2" style="text-align: center;">OrderStatus</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">ResultList</td>
<td style="text-align: center;">國內期貨下單結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutOrderData&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OrderStatus 交易類狀態</strong></td>
</tr>
<tr>
<td style="text-align: center;">MsgCode</td>
<td style="text-align: center;">訊息代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">0001:執行成功 其它:失敗</td>
</tr>
<tr>
<td style="text-align: center;">MsgContent</td>
<td style="text-align: center;">訊息內容</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Count</td>
<td style="text-align: center;">筆數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutOrderData 國內期貨下單結果明細</strong></td>
</tr>
<tr>
<td style="text-align: center;">Identify</td>
<td style="text-align: center;">識別碼</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">ReplyCode</td>
<td style="text-align: center;">委託結果代碼</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;">0:委託成功 others:委託失敗</td>
</tr>
<tr>
<td style="text-align: center;">OrderNO</td>
<td style="text-align: center;">委託書編號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日期</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;">日期</td>
</tr>
<tr>
<td style="text-align: center;">ErrType</td>
<td style="text-align: center;">錯誤類別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">ErrNO</td>
<td style="text-align: center;">錯誤代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Advisory</td>
<td style="text-align: center;">錯誤說明</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限期貨使用

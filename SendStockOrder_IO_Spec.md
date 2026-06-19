<table>
<colgroup>
<col style="width: 21%" />
<col style="width: 24%" />
<col style="width: 5%" />
<col style="width: 16%" />
<col style="width: 9%" />
<col style="width: 22%" />
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
<td colspan="2" style="text-align: center;"><strong>API SendStockOrder</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>國內證券下單</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool SendStockOrder(LoginAcno, lstStockOrder, lng)</strong></td>
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
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註1</p></td>
</tr>
<tr>
<td style="text-align: center;">lstStockOrder</td>
<td style="text-align: center;">下單物件清單</td>
<td colspan="2" style="text-align: center;">List&lt;StockOrder&gt;</td>
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
<td colspan="6" style="text-align: center;"><strong>StockOrder 國內現貨下單物件</strong></td>
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
<td colspan="2" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
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
<td style="text-align: center;">APCode</td>
<td style="text-align: center;">交易單市場別</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><p>0:一般</p>
<p>2:零股</p>
<p>4:盤中零股</p>
<p>7:盤後</p></td>
</tr>
<tr>
<td style="text-align: center;">TradeKind</td>
<td style="text-align: center;">交易性質</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><p>00:委託單</p>
<p>03:改量</p>
<p>04:取消</p>
<p>07:改價</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"0":現貨</p>
<p>"3":融資</p>
<p>"4":融券</p>
<p>"5":策略借券(賣出)</p>
<p>"6":避險借券(賣出)</p>
<p>"9":現股當沖委託控管</p></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySell</td>
<td style="text-align: center;">買賣記號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>"B":買</p>
<p>"S":賣</p></td>
</tr>
<tr>
<td style="text-align: center;">PriceFlag</td>
<td style="text-align: center;">價格種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>H:漲停</p>
<p>-:平盤</p>
<p>L:跌停</p>
<p>" ":限價</p>
<p>M:市價單</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">委託價格</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">非限價請填0</td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">使用者自訂欄位</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>(限32個英數字內)</p>
<p>若為條件單委託請將識別資訊帶入</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託單位</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Time_in_force</td>
<td style="text-align: center;">委託時間效期</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>0:ROD</p>
<p>3:IOC</p>
<p>4:FOK</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>StkOrderResult 國內證券下單結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
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
<td style="text-align: center;">國內證券下單結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;StkOrderData&gt;</td>
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
<td colspan="6" style="text-align: center;"><strong>StkOrderData 國內證券下單結果明細</strong></td>
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
<td colspan="2" style="text-align: center;">Tbyte5</td>
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
<td colspan="2" style="text-align: center;"><p>A003:預約單不支援改價或無此委託單</p>
<p>A004:委託已成交，無法改價</p>
<p>A005:委託已取消，無法改價</p></td>
</tr>
<tr>
<td style="text-align: center;">Advisory</td>
<td style="text-align: center;">錯誤說明</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限證券使用

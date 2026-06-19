<table style="width:100%;">
<colgroup>
<col style="width: 19%" />
<col style="width: 3%" />
<col style="width: 22%" />
<col style="width: 1%" />
<col style="width: 22%" />
<col style="width: 30%" />
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
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;"><strong>API SendFutureApart</strong></td>
<td style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>期貨複式單拆解</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="4" style="text-align: center;"><strong>bool SendFutureApart(LoginAcno, futureApart, lng)</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)</p>
<p>例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">lstFutSprStore</td>
<td style="text-align: center;">拆解物件</td>
<td colspan="2" style="text-align: center;">List&lt;FutSprStore&gt;</td>
<td style="text-align: center;">註2</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutureApart 複式單拆解物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><mark>FutAccount</mark></td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;">期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日期</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SeqNo</td>
<td style="text-align: center;">流水號</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><mark>Trid</mark></td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;">TX109100E4/TXO09000E4</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Qty</td>
<td style="text-align: center;">口數</td>
<td colspan="2" style="text-align: center;">Short</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutureApartResult 複式單拆解結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ResultCount</td>
<td style="text-align: center;">交易狀態</td>
<td colspan="2" style="text-align: center;">OrderStatus</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ResultList</td>
<td style="text-align: center;">複式單拆解結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutureApartData&gt;</td>
<td style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>OrderStatus 交易狀態</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MsgCode</td>
<td style="text-align: center;">訊息代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;">0001:執行成功 其它:失敗</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MsgContent</td>
<td style="text-align: center;">訊息內容</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Count</td>
<td style="text-align: center;">筆數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutureApartData 複式單拆解結果明細</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Identify</td>
<td style="text-align: center;">識別碼</td>
<td colspan="2" style="text-align: center;">Int</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ReplyCode</td>
<td style="text-align: center;">委託結果代碼</td>
<td colspan="2" style="text-align: center;">Short</td>
<td style="text-align: center;">0:委託成功 others:委託失敗</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ErrType</td>
<td style="text-align: center;">錯誤類別</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ErrNO</td>
<td style="text-align: center;">錯誤代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Advisory</td>
<td style="text-align: center;">錯誤說明</td>
<td colspan="2" style="text-align: center;">string</td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限期貨使用

註2：可由期貨複式單庫存明細查詢取得，流水號相同為同一複式單組合商品，若帶入相同流水號資料僅會處理一次

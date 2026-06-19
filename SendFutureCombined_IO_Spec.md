<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 25%" />
<col style="width: 5%" />
<col style="width: 18%" />
<col style="width: 6%" />
<col style="width: 24%" />
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
<td colspan="2" style="text-align: center;"><strong>API SendFutureCombined</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>期貨複式單組合</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool SendFutureCombined(LoginAcno, lstDepositOptimum, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">組合帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td style="text-align: center;">lstDepositOptimum</td>
<td style="text-align: center;">組合物件清單</td>
<td colspan="2" style="text-align: center;">List&lt;DepositOptimum&gt;</td>
<td colspan="2" style="text-align: center;"><strong>建議由保證金最佳化查詢結果篩選代入</strong></td>
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
<td colspan="6" style="text-align: center;"><strong>DepositOptimum 期貨保證金最佳化物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">StrategyID</td>
<td style="text-align: center;">策略ID</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;">6.買賣權混合部位(跨式,勒式))<br />
7.多頭價差<br />
8.Put空頭價差<br />
9.溫跌作莊<br />
10.溫漲作莊<br />
11.Call時間價差<br />
12.Put時間價差</td>
</tr>
<tr>
<td style="text-align: center;">FutAccountInfo</td>
<td style="text-align: center;">期貨帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Qty</td>
<td style="text-align: center;">口數</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuySell1</td>
<td style="text-align: center;">買賣別1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">B, S</td>
</tr>
<tr>
<td style="text-align: center;">BuySell2</td>
<td style="text-align: center;">買賣別2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">B, S</td>
</tr>
<tr>
<td style="text-align: center;">DealPrice1</td>
<td style="text-align: center;">成交價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="此值即為市價">此值即為市價</h1></td>
</tr>
<tr>
<td style="text-align: center;">DealPrice2</td>
<td style="text-align: center;">成交價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="此值即為市價-1">此值即為市價</h1></td>
</tr>
<tr>
<td style="text-align: center;">Decimal1</td>
<td style="text-align: center;">小數位數1</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"><h1 id="為小數位數-為分數分母0為整數">+為小數位數,-為分數分母,0為整數</h1></td>
</tr>
<tr>
<td style="text-align: center;">CurrentIM1</td>
<td style="text-align: center;">商品一保證金</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td style="text-align: center;">CurrentIM2</td>
<td style="text-align: center;">商品二保證金</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-1"></h1></td>
</tr>
<tr>
<td style="text-align: center;">SaveIM</td>
<td style="text-align: center;">可節省保證金</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-2"></h1></td>
</tr>
<tr>
<td style="text-align: center;">CommodityID1</td>
<td style="text-align: center;">商品ID1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="txo">TXO</h1></td>
</tr>
<tr>
<td style="text-align: center;">CallPut1</td>
<td style="text-align: center;">買賣權1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">C/P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth1</td>
<td style="text-align: center;">商品年月1</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">202502</td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice1</td>
<td style="text-align: center;">履約價1</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName1</td>
<td style="text-align: center;">商品名稱1</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">台指選 02 22800 P</td>
</tr>
<tr>
<td style="text-align: center;">CommodityID2</td>
<td style="text-align: center;">商品ID2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="txo-1">TXO</h1></td>
</tr>
<tr>
<td style="text-align: center;">CallPut2</td>
<td style="text-align: center;">買賣權2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">C/P</td>
</tr>
<tr>
<td style="text-align: center;">SettlementMonth2</td>
<td style="text-align: center;">商品年月2</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">202502</td>
</tr>
<tr>
<td style="text-align: center;">StrikePrice2</td>
<td style="text-align: center;">履約價2</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">StkName2</td>
<td style="text-align: center;">商品名稱2</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">台指選 02 23000 P</td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FutCombinedResult 複合式組合下單結果</strong></td>
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
<td style="text-align: center;">複合式組合下單結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;FutCombinedData&gt;</td>
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
<td colspan="6" style="text-align: center;"><strong>FutCombinedData複合式組合下單結果明細</strong></td>
</tr>
<tr>
<td style="text-align: center;">Identify</td>
<td style="text-align: center;">識別碼</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="section-3"></h1></td>
</tr>
<tr>
<td style="text-align: center;">ReplyCode</td>
<td style="text-align: center;">委託結果代碼</td>
<td colspan="2" style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"><h1 id="委託成功-others委託失敗">0:委託成功 others:委託失敗</h1></td>
</tr>
<tr>
<td style="text-align: center;">ErrType</td>
<td style="text-align: center;">錯誤類別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-4"></h1></td>
</tr>
<tr>
<td style="text-align: center;">ErrNO</td>
<td style="text-align: center;">錯誤代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-5"></h1></td>
</tr>
<tr>
<td style="text-align: center;">Advisory</td>
<td style="text-align: center;">錯誤說明</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-6"></h1></td>
</tr>
</tbody>
</table>

註1：限期貨使用

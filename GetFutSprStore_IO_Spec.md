<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 3%" />
<col style="width: 22%" />
<col style="width: 23%" />
<col style="width: 31%" />
</colgroup>
<thead>
<tr>
<th colspan="5" style="text-align: center;"><div data-custom-style="header">
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><strong>API GetFutSprStore</strong></td>
<td style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>期貨複式單庫存明細查詢</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="3" style="text-align: center;"><strong>bool GetFutSprStore(Account, lng)</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Lng</td>
<td style="text-align: center;">語系</td>
<td style="text-align: center;">enumLangType</td>
<td style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>FutSprStoreResult 查詢期貨複式單庫存明細結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">FutSprStoreList</td>
<td style="text-align: center;">結果清單</td>
<td style="text-align: center;">List&lt;FutSprStore&gt;</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>FutSprStore 期貨複式單物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">FutAccount</td>
<td style="text-align: center;">帳號</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Trid</td>
<td style="text-align: center;">商品代碼</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">TX109100E4/TXO09000E4</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SeqNo</td>
<td style="text-align: center;">流水號</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">流水號相同為同一複式單組合商品</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SprNum</td>
<td style="text-align: center;">組合編號</td>
<td style="text-align: center;">Short</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">B, S</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CommodityID</td>
<td style="text-align: center;">商品名稱</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">TXO</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CallPut</td>
<td style="text-align: center;">買賣權</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">C/P</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SettlementMonth</td>
<td style="text-align: center;">商品年月</td>
<td style="text-align: center;">Int</td>
<td style="text-align: left;">200708</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice</td>
<td style="text-align: center;">履約價</td>
<td style="text-align: center;">double</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Qty</td>
<td style="text-align: center;">口數</td>
<td style="text-align: center;">Short</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeDate</td>
<td style="text-align: center;">交易日期</td>
<td style="text-align: center;">TYuantaDate</td>
<td style="text-align: left;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MatchPrice</td>
<td style="text-align: center;">成交價</td>
<td style="text-align: center;">double</td>
<td style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkName</td>
<td style="text-align: center;">股票名稱</td>
<td style="text-align: center;">string</td>
<td style="text-align: left;">Ex: ‘中鋼實 06 0030 C’, ‘台指01’, ’ 櫃指選 03 00400 C’</td>
</tr>
</tbody>
</table>

註1：限期貨使用

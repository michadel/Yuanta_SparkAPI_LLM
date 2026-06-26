<table style="width:100%;">
<colgroup>
<col style="width: 22%" />
<col style="width: 25%" />
<col style="width: 18%" />
<col style="width: 7%" />
<col style="width: 26%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td style="text-align: center;"><strong>API Login</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>登入</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Windows 環境使用</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="4" style="text-align: center;"><strong>bool Login(Account, Pass)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">登入帳號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">Pass</td>
<td style="text-align: center;">登入密碼</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Linux 環境使用</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="4" style="text-align: center;"><strong>bool Login(PfxPath, PfxPass , Account, Pass)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">PfxPath</td>
<td style="text-align: center;">Pfx憑證路徑</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">絕對路徑</td>
</tr>
<tr>
<td style="text-align: center;">PfxPass</td>
<td style="text-align: center;">Pfx憑證密碼</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">登入帳號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+ 帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">Pass</td>
<td style="text-align: center;">登入密碼</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>LoginResult 登入結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginStatus</td>
<td style="text-align: center;">登入狀態</td>
<td style="text-align: center;">Status</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">LoginList</td>
<td style="text-align: center;">登入取得資料清單</td>
<td style="text-align: center;">List&lt;LoginData&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>Status 登入狀態</strong></td>
</tr>
<tr>
<td style="text-align: center;">MsgCode</td>
<td style="text-align: center;">訊息代碼</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>0000:執行失敗</p>
<p>0001:執行成功</p>
<p>0102: 密碼凍結或未啟用</p>
<p>0112:無此權限使用功能</p></td>
</tr>
<tr>
<td style="text-align: center;">MsgContent</td>
<td style="text-align: center;">中文訊息</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Count</td>
<td style="text-align: center;">筆數</td>
<td style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="5" style="text-align: center;"><strong>LoginData 登入取得資料</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S98875005091</p>
<p>期貨: FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">Name</td>
<td style="text-align: center;">客戶姓名</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">InvestorID</td>
<td style="text-align: center;">身分證字號</td>
<td style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellerNo</td>
<td style="text-align: center;">營業員代碼</td>
<td style="text-align: center;">Short</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

> **注意**：`Login` 呼叫頻率建議間隔 **5 秒以上**。短時間內重複呼叫登入可能造成伺服器端拒絕或帳號凍結風險，請勿在迴圈或重試邏輯中無節流地連續呼叫。

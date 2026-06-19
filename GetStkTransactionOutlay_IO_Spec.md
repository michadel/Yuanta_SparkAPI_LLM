<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 18%" />
<col style="width: 15%" />
<col style="width: 12%" />
<col style="width: 6%" />
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
<td colspan="2" style="text-align: center;"><strong>API GetStkTransactionOutlay</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>交割款查詢(台幣)</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetStkTransactionOutlay(Account, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註1</p></td>
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
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>ReversalReportResult 交割款查詢結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Field Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">TransactionOutlayList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;TransactionOutlay&gt;</td>
<td colspan="2" style="text-align: center;">註2</td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>TransactionOutlay 交割款物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>Account</p>
</div></td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>SettlementDay</p>
</div></td>
<td style="text-align: center;">交割日期</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>string</p>
</div></td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="List Paragraph">
<p>SettlementAmt</p>
</div></td>
<td style="text-align: center;">交割金額</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="List Paragraph">
<p>double</p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限證券使用

註2：近三交割日資料

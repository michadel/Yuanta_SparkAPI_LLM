<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 19%" />
<col style="width: 7%" />
<col style="width: 9%" />
<col style="width: 14%" />
<col style="width: 29%" />
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
<td colspan="2" style="text-align: center;"></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="2" style="text-align: center;"></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>event</strong></td>
<td colspan="2" style="text-align: center;">OnResponse</td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;">接收封包事件</td>
</tr>
<tr>
<td style="text-align: center;"><strong>delegate</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>事件回應</strong></p>
<p><strong>OnResponseEventHandler(intMark, dwIndex, strIndex, objHandle, objValue)</strong></p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">intMark</td>
<td style="text-align: center;">回應種類</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><p>0:系統資訊回應</p>
<p>1:查詢資訊回應</p>
<p>2:訂閱資訊回應</p></td>
</tr>
<tr>
<td style="text-align: center;">dwIndex</td>
<td style="text-align: center;">回應狀態</td>
<td colspan="2" style="text-align: center;">uint</td>
<td colspan="2" style="text-align: center;"><p>intMark為0：</p>
<p>0:其他訊息</p>
<p>1:Connect</p>
<p>2:Disconect</p>
<p>3:網路異常</p>
<p>4:需下載新版API</p>
<p>5:尚未連線</p>
<p>6:系統公告</p>
<p>intMark為1：</p>
<p>0:總帳/子帳登入</p>
<p>3:尚未登入</p>
<p>4:輸入的登入帳號錯誤</p>
<p>5:功能代碼錯誤,或權限不足</p>
<p>6:訂閱即時回報失敗</p>
<p>7:SocketRPRead失敗</p>
<p>9:加簽失敗/憑證異常</p>
<p>10:Logout!</p>
<p>11:帳號資訊異常</p>
<p>12:取得己訂閱商品清單異常</p>
<p>13:使用限制觸發</p>
<p>14:停權觸發</p>
<p>其他(FunctionID):功能回應</p>
<p>intMark為2：</p>
<p>1:訂閱/取消訂閱失敗</p>
<p>其他(FunctionID):功能回應</p>
<p>FunctionID請參考<a href="file:///Users/michael/Documents/CODE/GitHub-CODE/YSOP_Spark_CLI/doc/IO_Doc/FunctionList.xlsx"><span data-custom-style="Hyperlink">FunctionList.xlsx</span></a>功能對照表</p></td>
</tr>
<tr>
<td style="text-align: center;">strIndex</td>
<td style="text-align: center;">功能名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>intMark為0：</p>
<p>空字串<br />
<br />
intMark為1or2：</p>
<p>Function 例:SendStockOrder</p>
<p>空字串:查詢or訂閲功能有誤，請用string格式解析objValue</p>
<p>Function請參考<a href="file:///Users/michael/Documents/CODE/GitHub-CODE/YSOP_Spark_CLI/doc/IO_Doc/FunctionList.xlsx"><span data-custom-style="Hyperlink">FunctionList.xlsx</span></a>功能對照表</p></td>
</tr>
<tr>
<td style="text-align: center;">objHandle</td>
<td style="text-align: center;">Handle值</td>
<td colspan="2" style="text-align: center;">object</td>
<td colspan="2" style="text-align: center;">回傳訂閱事件時所傳入的Handle值(不處理)</td>
</tr>
<tr>
<td style="text-align: center;">objValue</td>
<td style="text-align: center;">回傳資料</td>
<td colspan="2" style="text-align: center;">object</td>
<td colspan="2" style="text-align: center;"><p>intMark為0：</p>
<p>strIndex為空字串：<br />
請用string格式解析</p>
<p>功能回應請依說明文件進行物件轉型並解析</p>
<p>非功能對照表功能請依舊元件方式解析byte[]</p>
<p>請參考<a href="file:///Users/michael/Documents/CODE/GitHub-CODE/YSOP_Spark_CLI/doc/IO_Doc/FunctionList.xlsx"><span data-custom-style="Hyperlink">FunctionList.xlsx</span></a>功能對照表</p></td>
</tr>
</tbody>
</table>

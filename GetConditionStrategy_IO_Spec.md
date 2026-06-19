<table>
<colgroup>
<col style="width: 23%" />
<col style="width: 18%" />
<col style="width: 12%" />
<col style="width: 14%" />
<col style="width: 5%" />
<col style="width: 25%" />
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
<td colspan="2" style="text-align: center;"><strong>API GetConditionStrategy</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>有效策略查詢</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetConditionStrategy(Account, StrategyType, StkCode, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">StrategyType</td>
<td style="text-align: center;">策略類型</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="2" style="text-align: center;"><p>1:停損利<br />
2:移動鎖利</p>
<p>3:二擇一</p>
<p>4:母子單<br />
5:多條件</p>
<p>6.全部</p></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p><strong>預設為空字串</strong></p>
<p>空字串則全查</p></td>
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
<td colspan="6" style="text-align: center;"><strong>ConditionStrategyResult 有效策略查詢結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">ConditionStrategyList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;ConditionStrategy&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>ConditionStrategy 有效策略結果物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">StrategyType</td>
<td style="text-align: center;">策略類型</td>
<td colspan="2" style="text-align: center;">StrategyType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StrategyNo</td>
<td style="text-align: center;">策略編號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrdDateTime</td>
<td style="text-align: center;">設定日期</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">StrategyStatus</td>
<td style="text-align: center;">條件單狀態</td>
<td colspan="2" style="text-align: center;">SStatus</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrdStatus</td>
<td style="text-align: center;">委託狀態</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">委託商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Condition</td>
<td style="text-align: center;">條件設定</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">母子單/多條件詳細條件，請至明細查詢</td>
</tr>
<tr>
<td style="text-align: center;">OrderKind</td>
<td style="text-align: center;">委託買賣種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">委託種類+買賣別+委託時效</td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">下單價格</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">設定股數</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DealQty</td>
<td style="text-align: center;">成交股數</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">RestQty</td>
<td style="text-align: center;">剩餘股數</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SDate</td>
<td style="text-align: center;">有效期限(起日)</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;">EDate</td>
<td style="text-align: center;">有效期限(迄日)</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;">OrderTypeMsg</td>
<td style="text-align: center;">下單方式</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">HighPx</td>
<td style="text-align: center;">區間高點</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">僅移動鎖利用，預設0</td>
</tr>
<tr>
<td style="text-align: center;">TriggerPx</td>
<td style="text-align: center;">觸發價格</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>僅停損利、移動鎖利、二擇一用</p>
<p>其他單別顯示--</p></td>
</tr>
<tr>
<td style="text-align: center;">DetailList</td>
<td style="text-align: center;">查詢明細清單</td>
<td colspan="2" style="text-align: center;">List&lt;ConditionStrategyDetail&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>ConditionStrategyDetail 查詢明細物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">DealTime</td>
<td style="text-align: center;">成交時間</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">yyyy/MM/dd</td>
</tr>
<tr>
<td style="text-align: center;">OrderPrice</td>
<td style="text-align: center;">委託價格</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">AveragePrice</td>
<td style="text-align: center;">成交均價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DealQty</td>
<td style="text-align: center;">成交股數</td>
<td colspan="2" style="text-align: center;">long</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Memo</td>
<td style="text-align: center;">備註</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TrigTime</td>
<td style="text-align: center;">觸發時間</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>HH:mm<br />
僅母子單、多條件用</p>
<p>其他單別顯示--</p></td>
</tr>
<tr>
<td style="text-align: center;">TrigCondition</td>
<td style="text-align: center;">觸發條件</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>僅母子單、多條件用</p>
<p>其他單別顯示--</p></td>
</tr>
</tbody>
</table>

**註1：資料上限200筆**

**註2：API不提供長效單的有效策略查詢，長效單請透過其他電子平台查詢**

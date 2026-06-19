<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 26%" />
<col style="width: 21%" />
<col style="width: 29%" />
</colgroup>
<thead>
<tr>
<th colspan="4" style="text-align: center;"><div data-custom-style="header">
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td style="text-align: center;"><strong>API GetFutInterestStore</strong></td>
<td style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>期貨權益數查詢</strong></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="3" style="text-align: center;"><strong>bool GetFutInterestStore(Account, Type, Currency, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p>
<p>註1</p></td>
</tr>
<tr>
<td style="text-align: center;">Type</td>
<td style="text-align: center;">型態</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>1:基本幣別</p>
<p>2:明細幣別</p></td>
</tr>
<tr>
<td style="text-align: center;">Currency</td>
<td style="text-align: center;">幣別</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>TWD:台幣</p>
<p>USA:美金</p>
<p>CNA:人民幣</p>
<p>JPA:日圓</p></td>
</tr>
<tr>
<td style="text-align: center;">Lng</td>
<td style="text-align: center;">語系</td>
<td style="text-align: center;">enumLangType</td>
<td style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="4" style="text-align: center;"><strong>FutInterestStoreResult 查詢期貨權益數結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td style="text-align: center;"><strong>Type</strong></td>
<td style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">ReplyCode</td>
<td style="text-align: center;">委託結果代碼</td>
<td style="text-align: center;">Short</td>
<td style="text-align: center;">0:委託成功 others:委託失敗</td>
</tr>
<tr>
<td style="text-align: center;">Advisory</td>
<td style="text-align: center;">錯誤說明</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Type</td>
<td style="text-align: center;">型態</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"><p>1:基本幣別</p>
<p>2:明細幣別</p></td>
</tr>
<tr>
<td style="text-align: center;">Currency</td>
<td style="text-align: center;">幣別</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"><p>TWD:台幣</p>
<p>USA:美金</p>
<p>CNA:人民幣</p>
<p>JPA:日圓</p></td>
</tr>
<tr>
<td style="text-align: center;">Equity</td>
<td style="text-align: center;">權益數</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">AllFullIm</td>
<td style="text-align: center;">全額原始保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CanuseMargin</td>
<td style="text-align: center;">可運用保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">RiskRate</td>
<td style="text-align: center;">權益比率</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DaytradeRisk</td>
<td style="text-align: center;">當沖風險指標</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">AllRiskRate</td>
<td style="text-align: center;">風險指標</td>
<td style="text-align: center;">String</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CashForward</td>
<td style="text-align: center;">前日餘額</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OpenGlYes</td>
<td style="text-align: center;">昨日未平倉損益</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">UpdateTime</td>
<td style="text-align: center;">風險更新時間</td>
<td style="text-align: center;">DateTime</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Accounting</td>
<td style="text-align: center;">存/提</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">FloatMargin</td>
<td style="text-align: center;">未沖銷期貨浮動損益</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">FloatPremium</td>
<td style="text-align: center;"><p>未沖銷買方選擇權市值+</p>
<p>未沖銷賣方選擇權市值</p></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CommissionAll</td>
<td style="text-align: center;">手續費</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TotalValue</td>
<td style="text-align: center;">權益總值</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">TaxRate</td>
<td style="text-align: center;">期交稅</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">AllIm</td>
<td style="text-align: center;">原始保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CallMargin</td>
<td style="text-align: center;">追繳保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Grantal</td>
<td style="text-align: center;"><p>本日期貨平倉損益淨額+</p>
<p>到期履約損益</p></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">AllMm</td>
<td style="text-align: center;">維持保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderIm</td>
<td style="text-align: center;">委託保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Premium</td>
<td style="text-align: center;">權利金收入與支出</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderPremium</td>
<td style="text-align: center;">委託權利金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Balance</td>
<td style="text-align: center;">本日餘額</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CanusePremium</td>
<td style="text-align: center;">可動用(出金)保證金(含抵委)</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CoveredOim</td>
<td style="text-align: center;">委託抵繳保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BondAmt</td>
<td style="text-align: center;">債券實物交割款</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">NobondAmt</td>
<td style="text-align: center;">債券實物不足交割款</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BondMargin</td>
<td style="text-align: center;">債券待交割保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">CoveredIm</td>
<td style="text-align: center;">有價證券抵繳總額</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">ReduceIm</td>
<td style="text-align: center;">期貨多空減收保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">IncreaseIm</td>
<td style="text-align: center;">加收保證金</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">YTotalValue</td>
<td style="text-align: center;">昨日權益總值</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Rate</td>
<td style="text-align: center;">匯率</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BestFlag</td>
<td style="text-align: center;">客戶保證金計收方式</td>
<td style="text-align: center;">string</td>
<td style="text-align: center;"><p>‘ ’: 傳統(策略)<br />
‘S’:整戶風險(SPAN)</p>
<p>‘Y’:保證金最佳化</p></td>
</tr>
<tr>
<td style="text-align: center;">GlToday</td>
<td style="text-align: center;">本日損益</td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DspEquity</td>
<td style="text-align: center;"><mark>風險權益總值</mark></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DspFloatmargin</td>
<td style="text-align: center;"><mark>未沖銷期貨風險浮動損益</mark></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DspFloatpremium</td>
<td style="text-align: center;"><mark>未沖銷買方選擇權風險市值+未沖銷賣方選擇權風險市值</mark></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DspIM</td>
<td style="text-align: center;"><mark>風險原始保證金</mark></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">DspRiskRate</td>
<td style="text-align: center;"><mark>盤後風險指標</mark></td>
<td style="text-align: center;">double</td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

註1：限期貨使用

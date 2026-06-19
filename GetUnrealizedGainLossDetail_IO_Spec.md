<table>
<colgroup>
<col style="width: 19%" />
<col style="width: 2%" />
<col style="width: 21%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 8%" />
<col style="width: 22%" />
</colgroup>
<thead>
<tr>
<th colspan="7" style="text-align: center;"><div data-custom-style="header">
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;"><strong>API GetUnrealizedGainLossDetail</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>未實現損益明細查詢</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetUnrealizedGainLossDetail(Account, MarketType, StkCode, lng)</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註1</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>UnGainLossDetailResult 未實現損益明細結果</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">UnGainLossDetailList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;UnGainLossDetail&gt;</td>
<td colspan="2" style="text-align: center;">註2</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>UnGainLossDetail 未實現損益明細物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeKind</td>
<td style="text-align: center;">交易種類</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><h1 id="現股">0:現股 </h1>
<h1 id="資買">3:資買  </h1>
<h1 id="券賣">4:券賣 </h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><h1 id="請參考api說明文件-列舉物件"><strong>請參考API說明文件-列舉物件</strong></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="section-1"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StockQty</td>
<td style="text-align: center;">股數</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-2"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Price</td>
<td style="text-align: center;">成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-3"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeDate</td>
<td style="text-align: center;">成交日</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><h1 id="yyyymmdd">yyyy/MM/dd</h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Cost</td>
<td style="text-align: center;">持有成本</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-4"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Interest</td>
<td style="text-align: center;">預估利息</td>
<td colspan="2" style="text-align: center;">Long</td>
<td colspan="2" style="text-align: center;"><h1 id="section-5"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">ReturnAmt</td>
<td style="text-align: center;">未實現損益</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="section-6"></h1></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketAmt</td>
<td style="text-align: center;">股票市值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><h1 id="股數市價">股數*市價</h1></td>
</tr>
</tbody>
</table>

註1：限證券使用

註2：不包含待沖單資訊

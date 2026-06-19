<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 1%" />
<col style="width: 19%" />
<col style="width: 8%" />
<col style="width: 11%" />
<col style="width: 12%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p>C80A0A1B(200.10.10.27)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;">RR_RealReportMerge</td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;">彙整的即時回報訂閱</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>RealReportMerge 即時回報彙總物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">RptType</td>
<td style="text-align: center;">回報標記</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: left;"><p>1:股票</p>
<p>2:期貨</p>
<p>3:選擇權</p>
<p>4:海外期貨</p>
<p>5:海外股票</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">CompanyNo</td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>2854, 05311<br />
FITX 200709,<br />
URO200709,</p>
<p>FIGTL7/C8,<br />
TXO09000T7,<br />
TXO08000/08100U7</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderTime</td>
<td style="text-align: center;">委託時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>0:普通</p>
<p>1,3:資</p>
<p>2,4:券</p>
<p>5,6:借券(賣出)<br />
期權</p>
<p>1:市價</p>
<p>2:限價</p>
<p>3:範圍市價<br />
海外期</p>
<p>LMT:限價單</p>
<p>MKT:市價單</p>
<p>STP:停損單</p>
<p>SWL:停損限價單</p>
<p>CXL:取消單</p>
<p>海外股票</p>
<p>1:Market<br />
2:Limit 限價單</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Price</td>
<td style="text-align: center;">價格</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>Ex. 23.50,1.0585</p>
<p>0000125’23.5(海外期)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TouchPrice</td>
<td style="text-align: center;">停損執行價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LastDealPrice</td>
<td style="text-align: center;">最新成交價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>Ex. 23.50,1.0585</p>
<p>0000125’23.5(海外期)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">AvgDealPrice</td>
<td style="text-align: center;">成交均價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>Ex. 23.50,1.0585</p>
<p>0000125’23.5(海外期)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BeforeQty</td>
<td style="text-align: center;">改量前數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託股數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"><p>股數/口數</p>
<p>(有效數量含成交)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OkQty</td>
<td style="text-align: center;">成交股數</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">股數/口數</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OpenOffsetKind</td>
<td style="text-align: center;">新增/沖銷別</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>期</p>
<p>0:新增</p>
<p>1:沖銷</p>
<p>2:新倉且當日沖銷單<br />
權</p>
<p>0: 新增</p>
<p>1: 沖銷</p>
<p>海外股票 (SettleType)</p>
<p>0:外幣</p>
<p>1:台幣</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DayTrade</td>
<td style="text-align: center;">當沖記號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券：' ' OR 'X'</p>
<p>期權：' ' OR 'Y'</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderCond</td>
<td style="text-align: center;">委託條件</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券</p>
<p>3:IOC</p>
<p>4:FOK</p>
<p>0:ROD</p>
<p>期權</p>
<p>F:FOK</p>
<p>I:IOC</p>
<p>R:ROD<br />
海外期</p>
<p>0:DAY</p>
<p>2:IOC</p>
<p>1:FOK</p>
<p>N:非GTC單</p>
<p>海外股票</p>
<p>0:DAY</p>
<p>3:IOC</p>
<p>4:FOK</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">P201</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">APCode</td>
<td style="text-align: center;">委託類別</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>0:現股</p>
<p>2:零股</p>
<p>4:盤中零股</p>
<p>7:盤後</p>
<p>99:興櫃</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">狀態碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: left;"><p>0：傳輸中</p>
<p>5：預約單</p>
<p>10：委託失敗</p>
<p>20：委託成功</p>
<p>24：委託失效</p>
<p>25：價穩失效</p>
<p>30：取消</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">LastOrderStatus</td>
<td style="text-align: center;">最新一筆即回資料狀態</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>0:委託成功</p>
<p>1:委託失敗</p>
<p>2:取消成功</p>
<p>3:取消失敗</p>
<p>4:減量成功</p>
<p>5:減量失敗</p>
<p>6:查詢成功</p>
<p>7:查詢失敗</p>
<p>8:已成交</p>
<p>10:組合成功</p>
<p>11:拆解成功</p>
<p>12:平轉新</p>
<p>13:新轉平</p>
<p>18:委託收到</p>
<p>19:取消收到(國外股票)</p>
<p>20:改價成功</p>
<p>21:改價失敗</p>
<p>23:取消成交 (國外股票)</p>
<p>24:委託失效</p>
<p>25:價穩失效</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkCName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">此欄位代表股票名稱;但是在期貨價差的CASE下,此欄位代表第二個商品的tradecode</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeCode</td>
<td style="text-align: center;">實體交易代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;">當期貨價差時,此欄位代表第一個商品的tradecode</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StrikePrice</td>
<td style="text-align: center;">履約價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BasketNo</td>
<td style="text-align: center;">一籃子下單編號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType1</td>
<td style="text-align: center;">屬性1</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: left;"><p>Bit 1: 管理商品</p>
<p>Bit 2: 交易記號</p>
<p>Bit 3: 受益憑證</p>
<p>Bit 4: ETF商品</p>
<p>Bit 5: 權證記號</p>
<p>Bit 6: 特別股</p>
<p>Bit 7: 存託憑證</p>
<p>Bit 8: 外國股票</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType2</td>
<td style="text-align: center;">屬性2</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: left;"><p>Bit 1: 可轉換公司債</p>
<p>Bit 2: 附認股權公司債</p>
<p>Bit 3: 警示股</p>
<p>Bit 4: 指數記號</p>
<p>Bit 5: 期貨</p>
<p>Bit 6: 個股選擇權</p>
<p>Bit 7: 指數選擇權</p>
<p>Bit 8: 保留</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BelongMarketNo</td>
<td style="text-align: center;">所屬市場代碼</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BelongStkCode</td>
<td style="text-align: center;">所屬股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType</td>
<td style="text-align: center;">價格型態</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p><strong>證券使用</strong></p>
<p>1:市價</p>
<p>2:限價</p>
<p>H:漲停</p>
<p>L:跌停</p>
<p>-:平盤</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkErrorNo</td>
<td style="text-align: center;">證券回報錯誤碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">證券回報錯誤碼</td>
</tr>
</tbody>
</table>

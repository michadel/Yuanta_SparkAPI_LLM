<table>
<colgroup>
<col style="width: 23%" />
<col style="width: 19%" />
<col style="width: 4%" />
<col style="width: 15%" />
<col style="width: 8%" />
<col style="width: 28%" />
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
<td colspan="2" style="text-align: center;"><strong>API GetRealReport</strong></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>即時回報查詢</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><strong>bool GetRealReport(Account, lng)</strong></td>
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
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
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
<td colspan="6" style="text-align: center;"><strong>RealReportResult 即時回報結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">RealReportList</td>
<td style="text-align: center;">結果清單</td>
<td colspan="2" style="text-align: center;">List&lt;RealReport&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>RealReport 即時回報物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">RptType</td>
<td style="text-align: center;">回報類別</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>50:股票委託</p>
<p>51:股票成交<br />
2:期貨委託</p>
<p>3:期貨成交<br />
4:期貨價差成交回報<br />
5:期貨委託減量取消</p>
<p>07:期貨改價回報<br />
10:選擇權委託回報<br />
11:單式成交回報<br />
12:複式成交回報<br />
13:選擇權減量取消回報<br />
17:選擇權改價回報</p>
<p>21:組合拆解回報<br />
22:改變新/平倉回報<br />
30:海外期貨委託<br />
31:海外期貨成交</p>
<p>32:海外期貨風控委託失敗單</p>
<p>40:海外股票委託,</p>
<p>41:海外股票委託取消</p>
<p>42:海外股票委託回覆,</p>
<p>43:海外股票委託取消回覆</p>
<p>44:海外股票成交</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託單號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">MarketNo</td>
<td style="text-align: center;">市場代碼</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">CompanyNo</td>
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
<td style="text-align: center;">StkCName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderTime</td>
<td style="text-align: center;">交易時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-物件</strong></p>
<p>委託時間/成交時間</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>0:普通</p>
<p>1,3:資</p>
<p>2,4:券</p>
<p>5:策略借券</p>
<p>6:避險借券</p>
<p>7:資沖</p>
<p>8:券沖<br />
期權</p>
<p>M:市價</p>
<p>L:限價</p>
<p>P:範圍市價<br />
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
<td style="text-align: center;">BS</td>
<td style="text-align: center;">買賣別</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: left;"><p>S:賣</p>
<p>B:買</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">價格</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"><p>委託價 / 成交價</p>
<p>Ex. 23.50,1.0585</p>
<p>0000125’23.5(海外期)</p></td>
</tr>
<tr>
<td style="text-align: center;">TouchPrice</td>
<td style="text-align: center;">停損執行價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;">000116'21.75</td>
</tr>
<tr>
<td style="text-align: center;">BeforeQty</td>
<td style="text-align: center;">改量前數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">委託股數 / 成交股數</td>
</tr>
<tr>
<td style="text-align: center;">OpenOffsetKind</td>
<td style="text-align: center;">新增/沖銷別</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>期</p>
<p>0:新增</p>
<p>1:沖銷</p>
<p>2:新倉且當日沖銷單<br />
權</p>
<p>0: 新增</p>
<p>1: 沖銷</p>
<p>海外股票(SettleType)</p>
<p>0:外幣</p>
<p>1:台幣</p></td>
</tr>
<tr>
<td style="text-align: center;">DayTrade</td>
<td style="text-align: center;">當沖記號</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>證券：' ' OR 'X'</p>
<p>期權：' ' OR 'Y'</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderCond</td>
<td style="text-align: center;">委託條件</td>
<td colspan="2" style="text-align: center;">String</td>
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
<td style="text-align: center;">OrderErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>P201</p>
<p>證券以外的錯誤碼</p></td>
</tr>
<tr>
<td style="text-align: center;">TradeKind</td>
<td style="text-align: center;">交易性質</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>1:B</p>
<p>2:S</p>
<p>3:改量</p>
<p>4:取消</p>
<p>5:查詢</p>
<p>6:改價</p>
<p>9:交易所主動刪單<br />
期權</p>
<p>1:新增</p>
<p>2:減量</p>
<p>3:取消</p>
<p>5:查詢</p>
<p>6:改價</p></td>
</tr>
<tr>
<td style="text-align: center;">APCode</td>
<td style="text-align: center;">委託類別</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>0:現股</p>
<p>2:零股</p>
<p>4:盤中零股</p>
<p>7:盤後<br />
組合拆解回報</p>
<p>83:拆解</p>
<p>67:組合<br />
改變新/平倉回報</p>
<p>83:新轉平</p>
<p>79:平轉新</p></td>
</tr>
<tr>
<td style="text-align: center;">BasketNo</td>
<td style="text-align: center;">一籃子下單編號</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;">條件單識別資訊</td>
</tr>
<tr>
<td style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">狀態碼</td>
<td colspan="2" style="text-align: center;">short</td>
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
<td style="text-align: center;">StkType1</td>
<td style="text-align: center;">屬性1</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>Bit 1: 管理商品</p>
<p>Bit 2: 交易記號</p>
<p>Bit 3: 受益憑證</p>
<p>Bit 4: ETF商品</p>
<p>Bit 5: 權證記號</p>
<p>Bit 6: 特別股</p>
<p>Bit 7: 存託憑證</p>
<p>Bit 8: 外國股票</p></td>
</tr>
<tr>
<td style="text-align: center;">StkType2</td>
<td style="text-align: center;">屬性2</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>Bit 1: 可轉換公司債</p>
<p>Bit 2: 附認股權公司債</p>
<p>Bit 3: 警示股</p>
<p>Bit 4: 指數記號</p>
<p>Bit 5: 期貨</p>
<p>Bit 6: 個股選擇權</p>
<p>Bit 7: 指數選擇權</p>
<p>Bit 8: TSE/OTC創新板/興櫃戰略新板</p></td>
</tr>
<tr>
<td style="text-align: center;">BelongMarketNo</td>
<td style="text-align: center;">所屬市場代碼</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BelongStkCode</td>
<td style="text-align: center;">所屬股票代碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SeqNo</td>
<td style="text-align: center;">成交序號</td>
<td colspan="2" style="text-align: center;">Uint</td>
<td colspan="2" style="text-align: center;"><p>For 股票,期貨成交單<br />
(複委託,國際期 -&gt;０)</p>
<p>若OrderStatus =25且StkErrCode =13051、19351，此欄位會帶入成交數量</p></td>
</tr>
<tr>
<td style="text-align: center;">PriceType</td>
<td style="text-align: center;">價格型態</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p><strong>只有證券使用</strong></p>
<p>1:市價</p>
<p>2:限價</p>
<p>H:漲停</p>
<p>L:跌停<br />
“-”:平盤</p></td>
</tr>
<tr>
<td style="text-align: center;">StkErrorNo</td>
<td style="text-align: center;">證券回報錯誤碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;">證券回報錯誤碼</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 1%" />
<col style="width: 21%" />
<col style="width: 2%" />
<col style="width: 16%" />
<col style="width: 8%" />
<col style="width: 24%" />
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
<td colspan="3" style="text-align: center;">C80A0A1A(200.10.10.26)</td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="3" style="text-align: center;">RR_RealReport</td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;">即時回報訂閱</td>
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
<td colspan="7" style="text-align: center;"><strong>RealReport 即時回報物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">RptType</td>
<td style="text-align: center;">回報類別</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>50:股票委託</p>
<p>51:股票成交</p>
<p>2:期貨委託</p>
<p>3:期貨成交<br />
4:期貨價差成交回報<br />
5:期貨委託減量取消<br />
10:選擇權委託回報<br />
11:單式成交回報<br />
12:複式成交回報<br />
13:選擇權減量取消回報<br />
21:組合拆解回報<br />
22:改變新/平倉回報<br />
30:海外期貨委託<br />
31:海外期貨成交</p></td>
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
<td colspan="2" style="text-align: center;">StkCName</td>
<td style="text-align: center;">商品名稱</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderDate</td>
<td style="text-align: center;">交易日</td>
<td colspan="2" style="text-align: center;">TYuantaDate</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderTime</td>
<td style="text-align: center;">交易時間</td>
<td colspan="2" style="text-align: center;">TYuantaTime</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-物件</strong><br />
委託時間/成交時間</td>
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
<p>M:市價</p>
<p>L:限價</p>
<p>P:範圍市價<br />
海外期</p>
<p>LMT:限價單</p>
<p>MKT:市價單</p>
<p>STP:停損單</p>
<p>SWL:停損限價單</p>
<p>CXL:取消單</p></td>
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
<td colspan="2" style="text-align: left;"><p>委託價 / 成交價</p>
<p>Ex. 23.50,1.0585</p>
<p>0000125’23.5(海外期)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TouchPrice</td>
<td style="text-align: center;">停損執行價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BeforeQty</td>
<td style="text-align: center;">改量前數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderQty</td>
<td style="text-align: center;">數量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;">委託股數 / 成交股數</td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OpenOffsetKind</td>
<td style="text-align: center;">新增/沖銷別</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>期</p>
<p>0:新增</p>
<p>1:沖銷</p>
<p>2:新倉且當日沖銷單<br />
權</p>
<p>0: 新增</p>
<p>1: 沖銷</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">DayTrade</td>
<td style="text-align: center;">當沖記號</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>證券：' ' OR 'X'</p>
<p>期權：' ' OR 'Y'</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderCond</td>
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
<p>N:非GTC單</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderErrorNo</td>
<td style="text-align: center;">錯誤碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p>P201</p>
<p>證券錯誤碼改5碼，使用另一欄位</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">TradeKind</td>
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
<td colspan="2" style="text-align: center;">APCode</td>
<td style="text-align: center;">委託類別</td>
<td colspan="2" style="text-align: center;">byte</td>
<td colspan="2" style="text-align: center;"><p>現貨</p>
<p>0:現股</p>
<p>2:零股</p>
<p>4:盤中零股</p>
<p>7:盤後</p>
<p>99:興櫃<br />
組合拆解回報</p>
<p>83:拆解</p>
<p>67:組合<br />
改變新/平倉回報</p>
<p>83:新轉平</p>
<p>79:平轉新</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BasketNo</td>
<td style="text-align: center;">一籃子下單編號</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">OrderStatus</td>
<td style="text-align: center;">狀態碼</td>
<td colspan="2" style="text-align: center;">short</td>
<td colspan="2" style="text-align: center;"><p>0委託成功</p>
<p>1委託失敗</p>
<p>2取消成功</p>
<p>3取消失敗</p>
<p>4減量成功</p>
<p>5減量失敗</p>
<p>6查詢成功</p>
<p>7查詢失敗</p>
<p>8已成交</p>
<p>10組合成功</p>
<p>11拆解成功</p>
<p>12平轉新</p>
<p>13新轉平</p>
<p>18委託收到</p>
<p>19取消收到</p>
<p>20改價成功</p>
<p>21改價失敗</p>
<p>23取消成交</p>
<p>24委託失效</p>
<p>25價穩失效</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkType1</td>
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
<td colspan="2" style="text-align: center;">StkType2</td>
<td style="text-align: center;">屬性2</td>
<td colspan="2" style="text-align: center;">Byte</td>
<td colspan="2" style="text-align: center;"><p>Bit 1: 可轉換公司債</p>
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
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">BelongStkCode</td>
<td style="text-align: center;">所屬股票代碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">SeqNo</td>
<td style="text-align: center;">成交序號</td>
<td colspan="2" style="text-align: center;">Uint</td>
<td colspan="2" style="text-align: center;"><p>For 股票,期貨成交單<br />
(複委託,國際期 -&gt;０)</p>
<p>若OrderStatus =25且StkErrCode = 13051、19351，此欄位會帶入成交數量</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">PriceType</td>
<td style="text-align: center;">價格型態</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"><p><strong>只有證券使用</strong></p>
<p>1:市價</p>
<p>2:限價</p>
<p>H:漲停</p>
<p>L:跌停</p>
<p>-:平盤</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;">StkErrorNo</td>
<td style="text-align: center;">證券回報錯誤碼</td>
<td colspan="2" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;">證券回報錯誤碼</td>
</tr>
</tbody>
</table>

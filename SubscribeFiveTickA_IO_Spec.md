<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 21%" />
<col style="width: 11%" />
<col style="width: 18%" />
<col style="width: 4%" />
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
<td style="text-align: center;"><div data-custom-style="header">
<p><strong>COM Function ID</strong></p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p>D20A3C0A (210.10.60.10)</p>
</div></td>
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作日期</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><p>API SubscribeFiveTickA</p>
<p>API UnSubscribeFiveTickA</p></td>
<td colspan="2" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><p>最佳五檔行情訂閱</p>
<p>最佳五檔行情解訂閱</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="5" style="text-align: center;"><p><strong>bool <mark>SubscribeFiveTickA</mark>(LoginAcno, LstFiveTickA, Lng)</strong></p>
<p><strong>bool Un<mark>SubscribeFiveTickA</mark>(LoginAcno, LstFiveTickA, Lng)</strong></p></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">LoginAcno</td>
<td style="text-align: center;">訂閱帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>期貨:F+分公司代號(7+3)+帳號(7)<br />
例如 FF021000P001234567</p></td>
</tr>
<tr>
<td style="text-align: center;">LstFiveTickA</td>
<td style="text-align: center;">訂閱商品清單</td>
<td colspan="2" style="text-align: center;">List&lt;FiveTickA&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Lng</td>
<td style="text-align: center;">語系</td>
<td colspan="2" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTickA 最佳五檔行情物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;"><mark>StockCode</mark></td>
<td style="text-align: center;">商品代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTickAResult 最佳五檔行情回傳結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="2" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Key</td>
<td style="text-align: center;">鍵值</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">MarketNo+StkCode (不足補0)</td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">股票代碼</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag</td>
<td style="text-align: center;">索引值</td>
<td colspan="2" style="text-align: center;">enumQuoteFiveTickIndexType</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Value</td>
<td style="text-align: center;">資料值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"><p><strong>此值定義請參考IndexFlag</strong><br />
若IndexFlag=IndexFlag20、</p>
<p>IndexFlag21、IndexFlag42、</p>
<p>IndexFlag43、IndexFlag50、</p>
<p>IndexFlag51 <strong><u>則無值</u></strong></p></td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_20</td>
<td style="text-align: center;">五檔報價Flag20</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag20</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag20才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_21</td>
<td style="text-align: center;">五檔報價Flag21</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag21</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag21才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_42</td>
<td style="text-align: center;">五檔報價Flag42</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag42</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag42才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_43</td>
<td style="text-align: center;">五檔報價Flag43</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag43</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag43才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_50</td>
<td style="text-align: center;">五檔報價Flag50</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag50</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag50才有值</td>
</tr>
<tr>
<td style="text-align: center;">IndexFlag_51</td>
<td style="text-align: center;">五檔報價Flag51</td>
<td colspan="2" style="text-align: center;">FiveTick_Flag51</td>
<td colspan="2" style="text-align: center;">IndexFlag=IndexFlag51才有值</td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag20 五檔報價IndexFlag20物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Price1</td>
<td style="text-align: center;">第一買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price2</td>
<td style="text-align: center;">第二買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price3</td>
<td style="text-align: center;">第三買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price4</td>
<td style="text-align: center;">第四買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price5</td>
<td style="text-align: center;">第五買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol1</td>
<td style="text-align: center;">第一買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol2</td>
<td style="text-align: center;">第二買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol3</td>
<td style="text-align: center;">第三買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol4</td>
<td style="text-align: center;">第四買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol5</td>
<td style="text-align: center;">第五買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag21 五檔報價IndexFlag21物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Price1</td>
<td style="text-align: center;">第一賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price2</td>
<td style="text-align: center;">第二賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price3</td>
<td style="text-align: center;">第三賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price4</td>
<td style="text-align: center;">第四賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price5</td>
<td style="text-align: center;">第五賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol1</td>
<td style="text-align: center;">第一賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol2</td>
<td style="text-align: center;">第二賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol3</td>
<td style="text-align: center;">第三賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol4</td>
<td style="text-align: center;">第四賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol5</td>
<td style="text-align: center;">第五賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag42 五檔報價IndexFlag42物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Price1</td>
<td style="text-align: center;">第六買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price2</td>
<td style="text-align: center;">第七買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price3</td>
<td style="text-align: center;">第八買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price4</td>
<td style="text-align: center;">第九買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price5</td>
<td style="text-align: center;">第十買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol1</td>
<td style="text-align: center;">第六買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol2</td>
<td style="text-align: center;">第七買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol3</td>
<td style="text-align: center;">第八買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol4</td>
<td style="text-align: center;">第九買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol5</td>
<td style="text-align: center;">第十買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag43 五檔報價IndexFlag43物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Price1</td>
<td style="text-align: center;">第六賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price2</td>
<td style="text-align: center;">第七賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price3</td>
<td style="text-align: center;">第八賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price4</td>
<td style="text-align: center;">第九賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price5</td>
<td style="text-align: center;">第十賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol1</td>
<td style="text-align: center;">第六賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol2</td>
<td style="text-align: center;">第七賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol3</td>
<td style="text-align: center;">第八賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol4</td>
<td style="text-align: center;">第九賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Vol5</td>
<td style="text-align: center;">第十賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag50 五檔報價IndexFlag50物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice1</td>
<td style="text-align: center;">第一買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice2</td>
<td style="text-align: center;">第二買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice3</td>
<td style="text-align: center;">第三買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice4</td>
<td style="text-align: center;">第四買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice5</td>
<td style="text-align: center;">第五買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol1</td>
<td style="text-align: center;">第一買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol2</td>
<td style="text-align: center;">第二買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol3</td>
<td style="text-align: center;">第三買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol4</td>
<td style="text-align: center;">第四買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol5</td>
<td style="text-align: center;">第五買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice1</td>
<td style="text-align: center;">第一賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice2</td>
<td style="text-align: center;">第二賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice3</td>
<td style="text-align: center;">第三賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice4</td>
<td style="text-align: center;">第四賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice5</td>
<td style="text-align: center;">第五賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol1</td>
<td style="text-align: center;">第一賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol2</td>
<td style="text-align: center;">第二賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol3</td>
<td style="text-align: center;">第三賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol4</td>
<td style="text-align: center;">第四賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol5</td>
<td style="text-align: center;">第五賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="6" style="text-align: center;"><strong>FiveTick_Flag51 五檔報價IndexFlag51物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice1</td>
<td style="text-align: center;">第六買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice2</td>
<td style="text-align: center;">第七買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice3</td>
<td style="text-align: center;">第八買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice4</td>
<td style="text-align: center;">第九買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyPrice5</td>
<td style="text-align: center;">第十買價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol1</td>
<td style="text-align: center;">第六買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol2</td>
<td style="text-align: center;">第七買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol3</td>
<td style="text-align: center;">第八買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol4</td>
<td style="text-align: center;">第九買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">BuyVol5</td>
<td style="text-align: center;">第十買量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice1</td>
<td style="text-align: center;">第六賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice2</td>
<td style="text-align: center;">第七賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice3</td>
<td style="text-align: center;">第八賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice4</td>
<td style="text-align: center;">第九賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellPrice5</td>
<td style="text-align: center;">第十賣價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol1</td>
<td style="text-align: center;">第六賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol2</td>
<td style="text-align: center;">第七賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol3</td>
<td style="text-align: center;">第八賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol4</td>
<td style="text-align: center;">第九賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">SellVol5</td>
<td style="text-align: center;">第十賣量</td>
<td colspan="2" style="text-align: center;">Int</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

註：買價市價買999999999，賣價市價賣-999999999

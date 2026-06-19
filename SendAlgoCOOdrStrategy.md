<table>
<colgroup>
<col style="width: 21%" />
<col style="width: 18%" />
<col style="width: 15%" />
<col style="width: 15%" />
<col style="width: 0%" />
<col style="width: 8%" />
<col style="width: 20%" />
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
<td colspan="2" style="text-align: center;"><div data-custom-style="header">
<p>TCBus(.Net)</p>
</div></td>
<td colspan="3" style="text-align: center;"><div data-custom-style="header">
<p><strong>製作者</strong></p>
</div></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Service ID</strong></td>
<td colspan="2" style="text-align: center;"><strong>API SendAlgoCOOdrStrategy</strong></td>
<td colspan="3" style="text-align: center;"><strong>Service Desc</strong></td>
<td style="text-align: center;"><strong>新增條件單</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Input Spec Table</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Function</strong></td>
<td colspan="6" style="text-align: center;"><strong>bool SendAlgoCOOdrStrategy(Account,</strong> <strong>lstStrategy, lng)</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="3" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="3" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"><p>證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</p>
<p>註：僅可使用證券帳號</p></td>
</tr>
<tr>
<td style="text-align: center;">lstStrategy</td>
<td style="text-align: center;">條件單物件清單</td>
<td colspan="3" style="text-align: center;"><p>List&lt;<a href="#STOStrategy"><span data-custom-style="Hyperlink">STOStrategy</span></a>&gt;,</p>
<p>List&lt;<a href="#MLPStrategy"><span data-custom-style="Hyperlink">MLPStrategy</span></a>&gt;,</p>
<p>List&lt;<a href="#OCOStrategy"><span data-custom-style="Hyperlink">OCOStrategy</span></a>&gt;,</p>
<p>List&lt;<a href="#SpiderStrategy"><span data-custom-style="Hyperlink">SpiderStrategy</span></a>&gt;,</p>
<p>List&lt;<a href="#MS_SpiderStrategy"><span data-custom-style="Hyperlink">MS_SpiderStrategy</span></a>&gt;,</p>
<p>List&lt;<a href="#MS_DayTradeSpiderStrategy"><span data-custom-style="Hyperlink">MS_DayTradeSpiderStrategy</span></a>&gt;</p></td>
<td colspan="2" style="text-align: center;"><p>STOStrategy 停損利</p>
<p>MLPStrategy 移動鎖利</p>
<p>OCOStrategy 二擇一</p>
<p>SpiderStrategy 多條件</p>
<p>MS_SpiderStrategy 母子單</p>
<p>MS_DayTradeSpiderStrategy 當沖母子單</p>
<p>註：單次僅能同策略</p></td>
</tr>
<tr>
<td style="text-align: center;">lng</td>
<td style="text-align: center;">語系</td>
<td colspan="3" style="text-align: center;">enumLangType</td>
<td colspan="2" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p><strong>預設為Normal</strong><br />
Normal:Big5</p>
<p>UTF8:UTF8</p>
<p>SC:簡體中文</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="STOStrategy" class="anchor"></span><strong>STOStrategy 停損利單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="3" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="3" style="text-align: center;">StrategyOrder1</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StrategySettings</td>
<td style="text-align: center;">條件設定</td>
<td colspan="3" style="text-align: center;"><a href="#StrategySettings"><span data-custom-style="Hyperlink">StrategySettings</span></a></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings</td>
<td style="text-align: center;">下單設定</td>
<td colspan="3" style="text-align: center;"><a href="#OrderSettings1"><span data-custom-style="Hyperlink">OrderSettings1</span></a>&lt;OrderType1,OrderPriceType1&gt;</td>
<td colspan="2" style="text-align: center;">僅提供庫存賣出</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="MLPStrategy" class="anchor"></span><strong>MLPStrategy 移動鎖利單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="3" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="3" style="text-align: center;">StrategyOrder1</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">StrategySettings</td>
<td style="text-align: center;">條件設定</td>
<td colspan="3" style="text-align: center;"><a href="#MLPStrategySettings"><span data-custom-style="Hyperlink">MLPStrategySettings</span></a></td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings</td>
<td style="text-align: center;">下單設定</td>
<td colspan="3" style="text-align: center;"><a href="#OrderSettings1"><span data-custom-style="Hyperlink">OrderSettings1</span></a>&lt;OrderType1,OrderPriceType2&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="OCOStrategy" class="anchor"></span><strong>OCOStrategy 二擇一單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="2" style="text-align: center;">StrategyOrder1</td>
<td colspan="3" style="text-align: center;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>限輸入:成交就停、觸發就停</p></td>
</tr>
<tr>
<td style="text-align: center;">StrategySettings1</td>
<td style="text-align: center;">條件1條件設定</td>
<td colspan="2" style="text-align: center;"><a href="#StrategySettings"><span data-custom-style="Hyperlink">StrategySettings</span></a></td>
<td colspan="3" style="text-align: left;">條件1與條件2 商品需一致</td>
</tr>
<tr>
<td style="text-align: center;">StrategySettings2</td>
<td style="text-align: center;">條件2條件設定</td>
<td colspan="2" style="text-align: center;"><a href="#StrategySettings"><span data-custom-style="Hyperlink">StrategySettings</span></a></td>
<td colspan="3" style="text-align: left;">條件1與條件2 商品需一致</td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings1</td>
<td style="text-align: center;">條件1下單設定</td>
<td colspan="2" style="text-align: center;"><a href="#OrderSettings2"><span data-custom-style="Hyperlink">OrderSettings2</span></a>&lt;OrderType2, OrderPriceType1&gt;</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings2</td>
<td style="text-align: center;">條件2下單設定</td>
<td colspan="2" style="text-align: center;"><a href="#OrderSettings2"><span data-custom-style="Hyperlink">OrderSettings2</span></a>&lt;OrderType2, OrderPriceType1&gt;</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="SpiderStrategy" class="anchor"></span><strong>SpiderStrategy 多條件單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="2" style="text-align: center;">StrategyOrder1</td>
<td colspan="3" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Settings</td>
<td style="text-align: center;">設定</td>
<td colspan="2" style="text-align: center;"><a href="#SpiderSettings"><span data-custom-style="Hyperlink">SpiderSettings</span></a></td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="MS_SpiderStrategy" class="anchor"></span><strong>MS_SpiderStrategy 母子單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中區間限制:當日~90天內</p>
<p>盤後區間限制:下一交易日~90天內</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="2" style="text-align: center;">StrategyOrder2</td>
<td colspan="3" style="text-align: left;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>限選交易到設定單位全部成交</p></td>
</tr>
<tr>
<td style="text-align: center;">DayTrade</td>
<td style="text-align: center;">是否當沖</td>
<td colspan="2" style="text-align: center;">bool</td>
<td colspan="3" style="text-align: left;">固定false</td>
</tr>
<tr>
<td style="text-align: center;">M_SpiderStrategy</td>
<td style="text-align: center;">母單設定</td>
<td colspan="2" style="text-align: center;"><a href="#SpiderSettings"><span data-custom-style="Hyperlink">SpiderSettings</span></a></td>
<td colspan="3" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">S_SpiderStrategy</td>
<td style="text-align: center;">子單設定</td>
<td colspan="2" style="text-align: center;"><a href="#SpiderSettings"><span data-custom-style="Hyperlink">SpiderSettings</span></a></td>
<td colspan="3" style="text-align: left;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="MS_DayTradeSpiderStrategy" class="anchor"></span><strong>MS_DayTradeSpiderStrategy 當沖母子單物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Account</td>
<td style="text-align: center;">帳號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;">證券:S+分公司代號(4)+帳號(7)<br />
例如 S98875005091</td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中限填當日(僅當日有效)</p>
<p>盤後限填下一交易日(僅下一交易日當日有效)</p></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="2" style="text-align: center;">DateTime</td>
<td colspan="3" style="text-align: center;"><p>盤中限填當日(僅當日有效)</p>
<p>盤後限填下一交易日(僅下一交易日當日有效)</p></td>
</tr>
<tr>
<td style="text-align: center;">Order</td>
<td style="text-align: center;">下單方式</td>
<td colspan="2" style="text-align: center;">StrategyOrder2</td>
<td colspan="3" style="text-align: left;"><p><strong>請參考API說明文件-列舉物件</strong></p>
<p>限選母單成交子單就立即下單</p></td>
</tr>
<tr>
<td style="text-align: center;">DayTrade</td>
<td style="text-align: center;">是否當沖</td>
<td colspan="2" style="text-align: center;">bool</td>
<td colspan="3" style="text-align: left;">固定true</td>
</tr>
<tr>
<td style="text-align: center;">M_SpiderStrategy</td>
<td style="text-align: center;">母單設定</td>
<td colspan="2" style="text-align: center;"><a href="#DayTradeSpiderSettings"><span data-custom-style="Hyperlink">DayTradeSpiderSettings</span></a></td>
<td colspan="3" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings</td>
<td style="text-align: center;">子單下單設定</td>
<td colspan="2" style="text-align: center;"><a href="#OrderSettings2"><span data-custom-style="Hyperlink">OrderSettings2</span></a>&lt;OrderType3, OrderPriceType1&gt;</td>
<td colspan="3" style="text-align: left;">僅提供母單反向</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="StrategySettings" class="anchor"></span><strong>StrategySettings 條件設定</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="3" style="text-align: center;">僅支援上市、上櫃商品</td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Condition</td>
<td style="text-align: center;">條件種類</td>
<td colspan="2" style="text-align: center;">StrategyCondition1</td>
<td colspan="3" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Direction</td>
<td style="text-align: center;">條件方向</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>1:大於等於</p>
<p>2:小於等於(成交價才可使用)</p></td>
</tr>
<tr>
<td style="text-align: center;">Value</td>
<td style="text-align: center;">條件數值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;"><p>限制：</p>
<p>成交價(開盤參考價x0.7~1.7倍)</p>
<p>總量(單位:張)</p>
<p>當日漲跌幅(0.01~10)%</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="MLPStrategySettings" class="anchor"></span><strong>MLPStrategySettings 移動鎖利條件設定</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="3" style="text-align: center;">僅支援上市、上櫃商品</td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">基準價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;">限制：開盤參考價x0.7~1.7倍</td>
</tr>
<tr>
<td style="text-align: center;">Pullback_Uint</td>
<td style="text-align: center;">區間高點回檔單位</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: left;"><p>1:百分比</p>
<p>2:元</p></td>
</tr>
<tr>
<td style="text-align: center;">Pullback_Value</td>
<td style="text-align: center;">區間高點回檔數值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;"><p>百分比:0.1~100%</p>
<p>元:0.01&lt;=設定值&lt;=開盤參考價</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="OrderSettings1" class="anchor"></span><strong>OrderSettings1&lt;T,T1&gt; 下單設定1</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;"><strong>T</strong></td>
<td colspan="3" style="text-align: center;">停損利、移動鎖利:OrderType1<br />
<strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">TimeInforce</td>
<td style="text-align: center;">委託時間效期</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>0:ROD</p>
<p>3:IOC</p>
<p>4:FOK</p></td>
</tr>
<tr>
<td style="text-align: center;">PriceType</td>
<td style="text-align: center;">委託價格種類</td>
<td colspan="2" style="text-align: center;"><strong>T1</strong></td>
<td colspan="3" style="text-align: center;"><p>停損利:OrderPriceType1</p>
<p>移動鎖利:OrderPriceType2</p>
<p><strong>請參考API說明文件-列舉物件</strong></p></td>
</tr>
<tr>
<td style="text-align: center;">OrderValue</td>
<td style="text-align: center;">委託數值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;"><p>非限價、成交價請填0</p>
<p>限制:<br />
限價(開盤參考價x0.7~1.7倍)</p>
<p>成交價(+-0~8)tick</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託單位</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;">張</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="OrderSettings2" class="anchor"></span><strong>OrderSettings2&lt;T,T1&gt; 下單設定2</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="3" style="text-align: center;">僅支援上市、上櫃商品</td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">OrderType</td>
<td style="text-align: center;">委託種類</td>
<td colspan="2" style="text-align: center;">T</td>
<td colspan="3" style="text-align: left;"><p>二擇一、多條件、母子單:OrderType2</p>
<p>當沖母子單:OrderType3</p>
<p><strong>請參考API說明文件-列舉物件</strong></p></td>
</tr>
<tr>
<td style="text-align: center;">TimeInforce</td>
<td style="text-align: center;">委託時間效期</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>0:ROD</p>
<p>3:IOC</p>
<p>4:FOK</p></td>
</tr>
<tr>
<td style="text-align: center;">PriceType</td>
<td style="text-align: center;">委託價格種類</td>
<td colspan="2" style="text-align: center;">T1</td>
<td colspan="3" style="text-align: center;">OrderPriceType1<strong><br />
請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderValue</td>
<td style="text-align: center;">委託數值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;"><p>非限價、成交價請填0</p>
<p>限制:</p>
<p>限價(開盤參考價x0.7~1.7倍)</p>
<p>成交價(+-0~8)tick</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderQty</td>
<td style="text-align: center;">委託單位</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;">張</td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="SpiderSettings" class="anchor"></span><strong>SpiderSettings 多條件設定</strong></td>
</tr>
<tr>
<td style="text-align: center;">lstSettings</td>
<td style="text-align: center;">條件設定</td>
<td colspan="2" style="text-align: center;">List&lt;<a href="#SpiderStrategySettings"><span data-custom-style="Hyperlink">SpiderStrategySettings</span></a>&gt;</td>
<td colspan="3" style="text-align: center;"><p>*最多8個、不得為0個<br />
*同商品同種類同方向不可重複</p>
<p>*當全部符合:同商品漲與跌不可同時設定<br />
1.當日漲幅、當日跌幅不可同時設定</p>
<p>2.總漲幅、總跌幅不可同時設定</p>
<p>3.當日漲停、當日跌停不可同時設定<br />
4.當日上漲、當日下跌不可同時設定</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings</td>
<td style="text-align: center;">下單設定</td>
<td colspan="2" style="text-align: center;"><a href="#OrderSettings2"><span data-custom-style="Hyperlink">OrderSettings2</span></a>&lt;OrderType2, OrderPriceType1&gt;</td>
<td colspan="3" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Eligible</td>
<td style="text-align: center;">符合條件</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>1:擇一符合</p>
<p>2:全部符合</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="DayTradeSpiderSettings" class="anchor"></span><strong>DayTradeSpiderSettings 當沖條件設定</strong></td>
</tr>
<tr>
<td style="text-align: center;">lstSettings</td>
<td style="text-align: center;">條件設定</td>
<td colspan="2" style="text-align: center;">List&lt;<a href="#SpiderStrategySettings"><span data-custom-style="Hyperlink">SpiderStrategySettings</span></a>&gt;</td>
<td colspan="3" style="text-align: center;"><p>*最多8個、不得為0個<br />
*同商品同種類同方向不可重複</p>
<p>*當全部符合:同商品漲與跌不可同時設定<br />
1.當日漲幅、當日跌幅不可同時設定</p>
<p>2.總漲幅、總跌幅不可同時設定</p>
<p>3.當日漲停、當日跌停不可同時設定<br />
4.當日上漲、當日下跌不可同時設定</p></td>
</tr>
<tr>
<td style="text-align: center;">OrderSettings</td>
<td style="text-align: center;">下單設定</td>
<td colspan="2" style="text-align: center;"><a href="#OrderSettings2"><span data-custom-style="Hyperlink">OrderSettings2</span></a>&lt;OrderType3, OrderPriceType1&gt;</td>
<td colspan="3" style="text-align: left;"></td>
</tr>
<tr>
<td style="text-align: center;">Eligible</td>
<td style="text-align: center;">符合條件</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>1:擇一符合</p>
<p>2:全部符合</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="SpiderStrategySettings" class="anchor"></span><strong>SpiderStrategySettings 多條件條件設定</strong></td>
</tr>
<tr>
<td style="text-align: center;">MarketType</td>
<td style="text-align: center;">市場類別</td>
<td colspan="2" style="text-align: center;">enumMarketType</td>
<td colspan="3" style="text-align: center;">僅支援上市、上櫃商品</td>
</tr>
<tr>
<td style="text-align: center;">StkCode</td>
<td style="text-align: center;">商品代號</td>
<td colspan="2" style="text-align: center;">string</td>
<td colspan="3" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">StrategyConditions</td>
<td style="text-align: center;">條件種類</td>
<td colspan="2" style="text-align: center;">StrategyCondition2</td>
<td colspan="3" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">Direction</td>
<td style="text-align: center;">條件方向</td>
<td colspan="2" style="text-align: center;">int</td>
<td colspan="3" style="text-align: center;"><p>1:大於等於</p>
<p>2:小於等於(成交價才可使用)</p>
<p>3:無(漲停或跌停)</p></td>
</tr>
<tr>
<td style="text-align: center;">Price</td>
<td style="text-align: center;">基準價</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;">條件種類非總漲幅、總跌幅填0<br />
限制:開盤參考價0.7~1.7倍</td>
</tr>
<tr>
<td style="text-align: center;">Value</td>
<td style="text-align: center;">條件數值</td>
<td colspan="2" style="text-align: center;">double</td>
<td colspan="3" style="text-align: center;"><p>當日漲停、當日跌停填0</p>
<p>限制:</p>
<p>成交價(現價0.7~1.7倍)</p>
<p>總量(單位:張)</p>
<p>當日漲跌幅(0.01~10)%</p>
<p>總漲跌幅(0.01~100)%</p>
<p>當日上漲下跌(0.01~9999)</p></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>Output Spec Table</strong></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><strong>OrderStrategyResult 條件單委託結果</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Fileld Name</strong></td>
<td style="text-align: center;"><strong>Description</strong></td>
<td colspan="3" style="text-align: center;"><strong>Type</strong></td>
<td colspan="2" style="text-align: center;"><strong>Memo</strong></td>
</tr>
<tr>
<td style="text-align: center;">ResultList</td>
<td style="text-align: center;">條件單委託結果清單</td>
<td colspan="3" style="text-align: center;">List&lt;<a href="#OrderStrategyStatus"><span data-custom-style="Hyperlink">OrderStrategyStatus</span></a>&gt;</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td colspan="7" style="text-align: center;"><span id="OrderStrategyStatus" class="anchor"></span><strong>OrderStrategyStatus 條件單委託狀態</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrdStatus</td>
<td style="text-align: center;">委託狀態</td>
<td colspan="3" style="text-align: center;">SStatus</td>
<td colspan="2" style="text-align: center;"><strong>請參考API說明文件-列舉物件</strong></td>
</tr>
<tr>
<td style="text-align: center;">OrderNo</td>
<td style="text-align: center;">委託編號</td>
<td colspan="3" style="text-align: center;">String</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">EffTime</td>
<td style="text-align: center;">策略起始日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">ExpTime</td>
<td style="text-align: center;">策略終止日</td>
<td colspan="3" style="text-align: center;">DateTime</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;">Msg</td>
<td style="text-align: center;">訊息中文</td>
<td colspan="3" style="text-align: center;">string</td>
<td colspan="2" style="text-align: center;"></td>
</tr>
</tbody>
</table>

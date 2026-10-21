# TnSovereignOptionStructureRouterV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1021.1830` · Causal Audit: `2026-10-21 18:30 CST`

## 策略定位

**主權化選擇權結構路由器**：以四證據**波動率體制引擎**（ATR 百分位、BB 寬度
百分位、ADX 趨勢強度、區間位置）仲裁當前市況應佈建哪一種**選擇權結構**
（跨式 Long Straddle / 跨式價差 Long Strangle / 牛CALL價差 Bull Call / 熊PUT
價差 Bear Put / 鐵鷹 Iron Condor），再依所選結構建構**多腳訂單負載**並路由
至事件券商 Webhook。同一負載可切換為**標準 JSON Webhook**格式，直接對接通用
券商 REST／Webhook 橋接層。

本策略同時於策略測試器內以**受限風險的方向性代理部位**還原所選結構的損益
幾何，供因果驗證；選擇權多腳之實際成交由券商端依 payload 執行。

## 與現有庫之差異

全庫 `grep -ril "straddle|strangle|iron condor" *.pine` **零命中** —— 本策略為
**庫內首例選擇權結構能力**。既有 `TnSovereignIndiaCcfNiftyV6` 雖含「選擇權
OI 確認」與「CE/PE 模擬對沖」，其本質仍是**期貨趨勢策略**；`TnSovereignDcaWebhookV6`
為 **DCA 網格 + Webhook** 橋接，**不涉及選擇權**。

差異摘要：

1. **原策略無策略邏輯**：`StocksDeveloperAlerts.pine` 是純粹的**訊息組裝器**
   （收到什麼訊號就組什麼負載）。本策略補上**結構判定引擎** —— 「什麼市況
   該佈哪種結構」是原專案完全未處理的決策層。
2. **風險限制區塊原生支援**：`maxloss` / `forceexit` / `entrywindow` /
   `blockonexpiryday` 四項限制作為 `riskLimits` 區塊附加於任一訂單。
3. **自訂多腳（multiLeg）**：支援 1~10 腳自組負載，單腳描述子格式
   `optiontype strike tradetype [x multiplier]`。
4. **JSON 雙通道**：原始 `key=value` 行式負載（事件券商原生格式）＋ 標準 JSON
   Webhook（通用橋接格式）雙輸出。

## 核心邏輯

### 1. 波動率體制引擎（四證據）
```
atrRank = ta.percentrank(ta.atr(atrLen), volLook)          // 已是 0~100 百分位
bbRank  = ta.percentrank(bbWidth, volLook)                   // 已是 0~100 百分位
adxV    = ta.dx(adxLen, adxLen)                              // 趨勢強度
rangePos = (close - loR) / (hiR - loR)                       // 區間位置 0..1
```
- `expVol` = `atrRank ≥ 80 且 bbRank ≥ 80` → **波動擴張**（趨勢即將加速或反轉）。
- `cmpVol` = `atrRank ≤ 25 且 bbRank ≤ 25` → **波動壓縮**（區間成形）。
- `upTrd` / `dnTrd` = `ADX ≥ 22 且 EMA50 與 EMA200 同向` → **方向性趨勢**。
- `brkUp` / `brkDn` = 收盤突破前 N 根極值且 `rangePos` 越界 → **突破確認**。

### 2. 結構仲裁
| 優先序 | 條件 | 佈建結構 | 方向 | 風險幾何 |
|--------|------|----------|------|----------|
| 1 | `creditOnly` 且允許信用 | 鐵鷹 Iron Condor | 區間反轉 | 翼寬 |
| 2 | 波動擴張 + 突破 | 跨式 / 跨式價差 | 雙向多 gamma | 溢價 |
| 3 | 波動壓縮 + 允許信用 | 鐵鷹 Iron Condor | 區間反轉 | 翼寬 |
| 4 | `upTrd` | 牛CALL價差 Bull Call | 多 | 溢價 |
| 5 | `dnTrd` | 熊PUT價差 Bear Put | 空 | 溢價 |
| — | 以上皆不成立 | `none`（不進場） | — | — |

- **溢價估算**：`premP = ATR × premMult`（跨式價差 ×0.6、鐵鷹 ×0.8）。
- **價差寬度**：`wPts = width × strikeStep`；**翼寬**：`wingP = wing × strikeStep`。
- **區間反轉方向**（鐵鷹）：`rangePos ≥ fadeTrig` 做空、`rangePos ≤ 1 − fadeTrig`
  做多，目標為區間中軸，停損為區間外緣 + 翼寬 —— 對應「區間內獲利、越界虧損」
  的鐵鷹損益幾何。

### 3. 訂單負載建構器
移植自原作者 v6 library 的完整欄位骨架：
```
target   : account 或 group（擇一）
size     : lots 或 quantity（由「數量模式」開關擇一輸出）
product  : INTRADAY / DELIVERY / NORMAL / MTF
trade    : BUY / SELL（長寫法 BUY/B/LONG、SELL/S/SHORT 正規化）
order    : MARKET / LIMIT（附 price）
validity : DAY / IOC
option   : CE / PE（C/CALL、PE/P/PUT 正規化）
expiry   : weekly / next / monthly / 具體日期
width    : 價差寬度（檔位）
wing     : 鐵鷹翼寬（檔位）
leg      : 單腳描述子（multiLeg 最多 10 腳）
risk     : maxloss / forceexit / entrywindow / blockonexpiryday
```
- 未設定之欄位整行省略（`kv()` 於值為空時回傳空字串）。
- `ordertype = LIMIT` 而 `price ≤ 0` → 拒絕送出（進場訊號層擋下）。
- **設定健全性守門**：`cfgTargetOk`（帳戶／群組須擇一）、`cfgSizeOk`（手數／
  數量須擇一且為正）、LIMIT 需附價 —— 任一不成立即**不進場**，並於面板
  「設定」列顯示 `目標衝突` / `數量衝突` / `請修正`。此設計取代原作者的
  `runtime.error()`（原作者每根 K 棒重複觸發會使整支腳本中止）。

### 4. 代理部位回測
選擇權多腳由券商端成交；策略測試器內以**受限風險代理部位**還原損益幾何：

| 結構 | 代理方向 | 停損（相對進場價） | 停利（相對進場價） |
|------|----------|--------------------|--------------------|
| 跨式 / 跨式價差 | 多（+1） | −溢價 | +1.5 × 溢價 |
| 牛CALL價差 | 多（+1） | −溢價 | +價差寬度 |
| 熊PUT價差 | 空（−1） | +溢價 | −價差寬度 |
| 鐵鷹 | 區間反轉方向 | 區間外緣 + 翼寬 | 區間中軸 |

代理部位於進場後**每根 K 棒重掛** `strategy.exit`，確保停損／停利始終有效；
另設策略端強制平倉時（`fHour`/`fMinute`）。

### 5. 進場紀律
- 每日最多 `maxTrades` 筆、`coolBars` 冷卻、可選進場時段濾網。
- `blockExp` 開啟且當日為 `expDate`（到期日）→ 禁止進場。
- 訊號僅於 `barstate.isconfirmed` 成立，訂單於下一根 K 棒開盤成交。

## 負載格式範例

### 事件券商原生格式（`key=value` 行式）
```
account=MY_ACC
symbol=NIFTY
exchange=NFO
producttype=NORMAL
strategy=straddle
lots=1
expiry=weekly
tradetype=BUY
ordertype=MARKET
maxloss=25000
forceexit=15:15
entrywindow=09:15-15:00
blockonexpiryday=true
```
鐵鷹結構額外帶 `width=`（價差檔位）與 `wing=`（翼寬檔位）。

### 標準 JSON Webhook
```json
{
  "strategy": "TnSovereignOptionStructureRouterV6",
  "version": "v26.1021.1830",
  "structure": "straddle",
  "label": "跨式 (Long Straddle)",
  "symbol": "NIFTY",
  "exchange": "NFO",
  "expiry": "weekly",
  "atrRank": 87,
  "bbRank": 82,
  "adx": 26.4,
  "payload": "account=MY_ACC|symbol=NIFTY|..."
}
```
`payload` 內之換行以 `|` 取代，確保 JSON 單行可解析。

## 主要參數

| 群組 | 參數 | 預設 | 說明 |
|------|------|------|------|
| ① 標的與帳戶 | `iSymbol` / `iExchange` / `iProduct` | NIFTY / NFO / NORMAL | 標的與交易所 |
| ① 標的與帳戶 | `iAccount` / `iGroup` | MY_ACC / 空 | 目標（擇一） |
| ① 標的與帳戶 | `iSizeMode` / `iLots` / `iQuantity` | lots / 1 / 0 | 數量模式（lots 或 quantity 擇一輸出） |
| ① 標的與帳戶 | `iExpiry` | weekly | 到期 |
| ② 波動率體制 | `atrLen` / `volLook` | 14 / 120 | 體制量測窗口 |
| ② 波動率體制 | `volHi` / `volLo` | 80 / 25 | 擴張／壓縮門檻（百分位） |
| ② 波動率體制 | `adxLen` / `adxMin` | 14 / 22 | 趨勢強度門檻 |
| ② 波動率體制 | `premMult` / `strikeStep` | 0.6 / 50 | 溢價係數／履約價間距 |
| ③ 結構參數 | `width` / `wing` | 2 / 2 | 價差寬度／翼寬（檔位） |
| ③ 結構參數 | `useStrangle` / `allowCredit` / `creditOnly` | false / true / false | 結構偏好 |
| ④ 訂單 | `ordertype` / `price` / `validity` | MARKET / 0 / DAY | 訂單參數 |
| ⑤ 風險限制 | `maxloss` / `forceExit` / `entryWin` | 0 / 15:15 / 09:15-15:00 | 風險區塊 |
| ⑤ 風險限制 | `blockExp` / `expDate` | true / 空 | 到期日封鎖 |
| ⑥ 濾網 | `useSession` / `sessStr` / `sessTz` | false / 0930-1500 / Asia/Kolkata | 進場時段 |
| ⑥ 濾網 | `maxTrades` / `coolBars` | 2 / 10 | 每日筆數／冷卻 |

## 視覺層

- 區間上緣／下緣／中軸以獨立 pane 繪製，作為結構幾何的視覺錨點。
- 結構底色：信用結構（鐵鷹）綠、無交易灰、其餘紅。
- 進場標籤直接顯示所選結構名稱。
- 統計面板：結構、ATR 百分位、BB 寬百分位、ADX、區間位置、今日進場次數、
  交易數與勝率、淨值百分比。

## 來源與授權

- **原始來源**：[`stocks-developer/autotrader-tradingview-lib`](https://github.com/stocks-developer/autotrader-tradingview-lib)
  — `StocksDeveloperAlerts.pine`（498 行 v6 `library("StocksDeveloperAlerts")`）
  ＋ `examples/long-straddle.pine`（68 行 v6 `strategy()`），**MPL-2.0**。
- **主權化差異**：補上原專案未處理的**結構判定引擎**；將原作者每根 K 棒重複
  觸發的 `runtime.error()` 改為**嚴格且等價的守門判斷**；新增標準 JSON
  Webhook 通道；新增代理部位回測與完整視覺層；移除任何績效宣稱字串。
- **授權**：MPL-2.0 —— 保留原作者 MPL-2.0 聲明，衍生版本同以 MPL-2.0 釋出。

## 免責聲明

本文件描述之策略僅供研究與教學用途，不構成投資建議。選擇權為槓桿性商品，
可能導致超過本金之損失；實際交易前請充分理解產品條款、風險與保證金要求，
並自行評估與承擔後果。本系統不對任何策略績效作任何保證。

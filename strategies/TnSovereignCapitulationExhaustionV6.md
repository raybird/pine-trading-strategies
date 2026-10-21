# TnSovereignCapitulationExhaustionV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1022.0630` · Causal Audit: `2026-10-22 06:30 CST`

## 策略定位

**投降式耗竭反轉（Capitulation Exhaustion Reversal）**：在價格出現**結構性
深度拋售**（距 VWAP、布林下緣、前日低點、24 根低點、96 根低點皆已抵達
ATR 距離內）且同時出現**耗竭證據**（RSI 低 + 隨機指標低 + 單根報酬 Z 極負
+ 收盤復原位置 + 量能流動性 + 價量動能未過熱）時，於**體制閘門**允許下
建立多頭部位，出場採「棘輪停損（固定 ATR 停損與追蹤停損取近者）+ ATR
目標 + VWAP 復原 / RSI 高檔 / 動能見頂 / 持倉上限」多重紀律。

## 與現有庫之差異

現有庫的反轉類策略皆未以「**投降（capitulation）**」為核心命題：

- 全庫 `grep -ril "capitulation\|climax\|price.volume" strategies/*.pine`
  **零命中**。
- `TnSovereignPDHPDLFadeV6` 為前一日高低點單純回落反轉（僅一項位置
  證據）；`TnSovereignZScoreReversionV6` 為報酬 Z 分位反轉（僅一項統計
  證據）；`TnSovereignOscDivZonesV6` 為振盪器背離區間（無量能高潮、無
  VWAP / 布林結構定位）。
- 本策略是全庫**第一個將「深度位置 × 耗竭證據 × 體制閘門」三段式合成
  為單一進場命題**的策略：位置證據（結構極值）、行為證據（恐慌拋售 +
  收盤復原）、環境證據（ADX 帶 / ATR 相對值帶 / 4H 與日線方向仲裁）
  缺一不可。

## 核心邏輯

### 1. 體制閘門（Regime Gate）
```
capRegimeOk = any | daily_not_bear | h4_up | either_up     // 4H / 日線 EMA 方向仲裁
atrRelOk    = capAtrRelMin ≤ ATR / SMA(ATR,192) ≤ capAtrRelMax
adxOk       = capAdxMin ≤ ADX(14) ≤ capAdxMax
```
- HTF 序列（4H EMA 17/26、日線 EMA 12/50、前日高低）一律取**已收盤值**。
- ATR 相對值帶排除「波動已死」與「波動失控」兩種不適格環境。

### 2. 深度定位（Deep Location）——價格已抵達結構極值
```
capDeep = (close − VWAP) / ATR ≤ −3.4311                          // 距 VWAP 極遠
       or close ≤ BB_lower(40, 2.0) − 1.15522 × ATR               // 跌破布林下緣
       or close ≤ prevDayLow + 0.368443 × ATR                      // 貼近前日低點
       or low  ≤ lowest(low, 24)[1] − 1.006339 × ATR               // 跌破 24 根低點
       or low  ≤ lowest(low, 96)[1] + 1.095075 × ATR               // 貼近 96 根低點
```
五項定位條件為 **OR 關係**：任一項成立即視為「已拋售到結構極值」。

### 3. 耗竭證據（Exhaustion Evidence）——賣壓耗盡
```
capExhaustion = RSI(14) ≤ 41.148                                 // 超賣
             and Stoch K ≤ 35.712                                 // 隨機指標低位
             and retZ ≤ −0.788456                                // 單根報酬 Z 極負（恐慌拋售）
             and rangePos ≥ 0.076128                              // 收盤復原（長紅 K）
             and volume / SMA(volume,96) ≥ 0.521054               // 量能流動性（可關閉）
             and priceVolumeZ ≤ 1.064531                          // 價量動能未過熱
```
- `retZ`：`ta.change(close)/close[1]` 對 96 根視窗之 Z 分數。
- `rangePos`：`(close − low) / (high − low)`，代表收盤位於該 K 棒區間
  的位置 —— 數值偏高代表「低開後收復」，為多頭反轉的關鍵證據。
- `priceVolumeZ`：`Σ(Δclose × volume, 4)` 對 96 根視窗之 Z 分數；設上限
  可避免在價量動能已極度延伸（尚未耗竭）時接刀。

### 4. 反轉確認（選配）
```
capReversal = K 線黃金交叉 or 收紅 K or MACD 柱收斂向上
```
`capRequireReversal` 預設關閉（沿用原作者），開啟後需再多一項反轉徵兆。

### 5. 出場（多重紀律）
- **棘輪停損**：`max(進場均價 − 2.2046 × ATR, 進場後最高點 − 0.8154 × ATR)`
  —— 取較近者，因「進場後最高點」只會上移，停損結構上只朝有利方向移動。
- **ATR 目標**：`進場均價 + 5.3950 × ATR`。
- **VWAP 復原出場**：`close ≥ VWAP + 0.5788 × ATR`（最短持倉 3 根後生效）。
- **RSI 反轉出場**：`RSI ≥ 73.774`。
- **動能見頂出場**：`MACD 柱 < 前一根 且 rangePos ≤ 0.451264`。
- **時間出場**：持倉 56 根上限；可選每日強制平倉。

### 6. 風險距離定倉
```
stopDist = 2.2046 × ATR
qtyRisk  = (equity × riskPct%) / stopDist
qtyCap   = equity × maxLev / (close × syminfo.pointvalue)
qty      = int(max(1, floor(min(qtyRisk, qtyCap))))
```

## 非重繪契約

- 所有進場訊號僅於 `barstate.isconfirmed`（**已收盤 K 棒**）成立。
- `process_orders_on_close = false` → 訂單於**下一根 K 棒開盤**成交。
- HTF（4H / 日線）序列以 `lookahead_on` 取**已收盤值**，不使用未完成 K 棒。
- `calc_on_every_tick = false`。
- **原作者檔內之 SciPy 峰谷標記已全數刪除** —— 該標記由匯出資料回溯
  產生，屬未來資訊（事後標籤），與本庫非前視契約直接牴觸。

## 主權化修正（相對原作者）

1. **刪除事後標籤**：移除原作者內嵌之 SciPy peaks / valleys 標記陣列
   （由 TradingView 匯出資料回溯產生，構成未來資訊）。
2. **移除最佳化日期窗**：原作者以 `useDateRange` + 硬編碼 timestamp 將策略
   鎖定於特定最佳化區間（選擇偏誤）；本版改以「時段濾網 + 每日平倉 +
   持倉上限」表達時間紀律。
3. **HTF 取值語意明確化**：改以 `lookahead_on` 取已收盤值（與原作者
   `[1] + lookahead_off` 等價），消除盤中重繪疑慮。
4. **成交時機**：原作者 `process_orders_on_close = true`，本版改為 `false`
   並以已收盤 K 棒判定訊號，進場於下一根開盤成交。
5. **風險距離定倉 + 名目槓桿封頂**：取代原作者之固定 1 口。
6. **量能容錯**：`useVolumeCond` 可關閉，以適用無成交量標的（外匯等）。
7. **新增 JSON Webhook 與因果儀表板**；移除所有績效宣稱字串。

## 主要參數

| 群組 | 參數 | 預設 | 說明 |
|------|------|------|------|
| ① 體制 | `capRegime` | any | 方向仲裁模式（any / daily_not_bear / h4_up / either_up） |
| ① 體制 | `capAdxMin` / `capAdxMax` | 8.305 / 48.356 | ADX 帶 |
| ① 體制 | `capAtrRelMin` / `capAtrRelMax` | 0.945 / 3.034 | ATR 相對值帶 |
| ② 深度 | `capVwapDistAtr` | 3.4311 | 距 VWAP 之 ATR 距離 |
| ② 深度 | `capBbAtr` | −1.15522 | 布林下緣偏移（×ATR） |
| ② 深度 | `capPrevLowAtr` | 0.368443 | 距前日低點之 ATR 距離 |
| ② 深度 | `capLowBreakAtr` / `capLow96Atr` | 1.006339 / 1.095075 | 24 根 / 96 根低點距離 |
| ③ 耗竭 | `capRsiMax` / `capStochMax` | 41.148 / 35.712 | 超賣門檻 |
| ③ 耗竭 | `capRetZ` / `capReclaimPos` | 0.788456 / 0.076128 | 報酬 Z 極值 / 收盤復原位置 |
| ③ 耗竭 | `capVolumeMult` / `capPvZMax` | 0.521054 / 1.064531 | 量能流動性 / 價量動能上限 |
| ③ 耗竭 | `capRequireReversal` | false | 是否要求反轉確認 |
| ④ 出場 | `capStopAtr` / `capTargetAtr` / `capTrailAtr` | 2.2046 / 5.3950 / 0.8154 | 停損 / 目標 / 追蹤（×ATR） |
| ④ 出場 | `capExitVwapAtr` / `capExitRsi` / `capExitRangePos` | 0.5788 / 73.774 / 0.451264 | VWAP 復原 / RSI / 見頂位置 |
| ④ 出場 | `capMinHold` / `capMaxHold` / `capCooldown` | 3 / 56 / 1 | 持倉與冷卻紀律 |
| ⑤ 風險 | `riskPct` / `maxLev` | 1.0 / 2.0 | 單筆風險% / 名目槓桿封頂 |
| ⑥ 濾網 | `useSession` / `useNyHours` / `useEodFlat` | false / false / false | 時段與每日平倉 |

## 告警與 Webhook

文字告警：無內建文字告警（進場標記以 `CAP` 菱形顯示於圖上）。

JSON Webhook（`useWebhook = true`）：
```json
{
  "strategy": "TnSovereignCapitulationExhaustionV6",
  "version": "v26.1022.0630",
  "symbol": "<ticker>",
  "timeframe": "<period>",
  "side": "BUY",
  "kind": "capitulation",
  "vwapDist": -3.72,
  "retZ": -2.41,
  "rsi": 33.8,
  "qty": 12
}
```

## 視覺層

- **CAP 菱形**：投降反轉進場點。
- **D / E 圓點**（選配）：深度定位與耗竭證據的原始命中標記。
- **結構位圖層**：_session VWAP、布林上下軌、前日高低點。
- **停損 / 目標線**：持倉期間繪製當前生效的棘輪停損與 ATR 目標。
- **體制底色**：4H EMA 方向（多頭綠 / 空頭紅）。
- **因果儀表板**：訊號狀態、方向體制、深度／耗竭雙證據、VWAP 距離、
  報酬 Z 與 RSI、部位與進場價、持倉根數與淨損益、交易次數。

## 來源與授權

- **原始來源**：[`jnaggud/quant-research-lab`](https://github.com/jnaggud/quant-research-lab) —
  `pine_strategies/JD_CL_15m_Capitulation_Sleeve_64k_C1.pine`（395 行，v6
  `strategy()`，MIT License，Copyright 2026 Jefferson Duggan）。原檔為
  「趨勢核心 + 一致性 sleeve + 投降反轉 sleeve」三段式工廠，本版僅萃取
  其 capitulation sleeve 之紀律並重構為獨立主權策略。
- **主權化差異**：刪除事後 SciPy 標籤、移除最佳化日期窗、HTF 取值明確化、
  成交時機改為下一根開盤、風險距離定倉與槓桿封頂、量能容錯、JSON
  Webhook、因果儀表板、移除績效宣稱字串。
- **授權**：MIT —— 保留原作者 MIT 聲明，衍生版本同以 MIT 釋出。

## 免責聲明

本文件描述之策略僅供研究與教學用途，不構成投資建議，亦不對任何標的、
未來報酬或績效指標作任何保證。原作者之參數來自其自有最佳化流程，本庫
未經獨立驗證，實際交易須自行評估風險並承擔後果。

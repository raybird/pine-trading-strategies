# TnSovereignAtrBandRatchetTrendV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1021.1830` · Causal Audit: `2026-10-21 18:30 CST`

## 策略定位

**ATR 單向棘輪帶趨勢追蹤 + 回測再進場**：以 EMA(21) 為基底、ATR(10)×2 為帶寬
建構**單向棘輪（ratchet）**支撐／阻力帶 —— 多頭趨勢中支撐帶只上移不下移、
空頭趨勢中阻力帶只下移不上移（除非收盤已越過該帶緣則重置）。價格收盤越過
帶緣即 **stop-and-reverse（停損反手）**；趨勢延續但回到 EMA 基底時，**回測
再進場（pullback re-entry）**順勢重建部位。帶緣同時是**真實盤中停損**，
停利則以 **R 倍數**定義（R = 進場當下「收盤價到帶緣的距離」），部位大小以
**風險金額 ÷ 停損距離**計算並以**槓桿上限封頂**。

## 與現有庫之差異

現有庫的 Supertrend 系（`TnSovereignSupertrendV6`、`TnSovereignSupertrendVolV6`）
與 Chandelier 系（`TnSovereignChandelierV6`）皆為**單向追蹤停損**，出場邏輯
只有「被停損」或「固定目標」兩種，**沒有「反手重入」與「趨勢中回測再進場」
的二次建倉路徑**。

本策略的獨特處：

1. **單向棘輪帶（ratchet）**：Supertrend / Chandelier 的帶緣會隨 ATR 擴張而
   **雙向**移動；本策略的支撐帶在多頭中只上移、阻力帶在空頭中只下移，
   使「趨勢持續期間不被波動噪音掃出」成為結構性保證。
2. **回測再進場（pullback re-entry）**：趨勢未變、部位已被停損出場後，
   收盤重新穿越 EMA 基底即重新順勢進場 —— 庫內無此完整紀律
   （`TnSovereignDonchianPullbackV6` 為 Donchian 通道中線回測，通道語義不同）。
3. **R 倍數停利**：R 由「進場到帶緣的實際距離」定義，停損距離與部位大小
   恆等對齊（風險定倉與停損幾何同源），庫內無以帶緣距離定義 R 者。
4. **槓桿封頂的風險距離定倉**：`qty = floor(min(riskMoney / (dist × pointvalue),
   equity × maxLev / (close × pointvalue)))` —— 全庫僅 `TnSovereignPineFlowIctFvgV6`
   與 `TnSovereignPineFlowOrbV6` 使用 `syminfo.pointvalue` 計算部位，本策略
   為**第三例**，且額外加上槓桿名目封頂。

## 核心邏輯

### 1. EMA 基底 + ATR 單向棘輪帶
```
basis = ta.ema(close, baseLen)          // 預設 21
atrV  = ta.atr(atrLen)                  // 預設 10
loNew = basis - mult * atrV             // 多頭支撐候選
hiNew = basis + mult * atrV             // 空頭阻力候選

lo := na(pLo) ? loNew : (loNew > pLo or close[1] < pLo) ? loNew : pLo
hi := na(pHi) ? hiNew : (hiNew < pHi or close[1] > pHi) ? hiNew : pHi
```
- `lo` 僅在多頭情境有效：候選值上移才更新；`close[1] < pLo` 代表收盤已跌破
  支撐帶 → 該帶失效重置（允許下移）。
- `hi` 對稱：候選值下移才更新；`close[1] > pHi` → 重置（允許上移）。
- 棘輪帶**僅由已收盤的 basis / ATR 更新**，不含任何未來函數引用。

### 2. 趨勢狀態機
```
dir == 0 → dir = close > basis ? 1 : -1     // 首次定向
dir == 1 且 close < pLo → dir = -1           // 收盤跌破支撐帶 → 翻空
dir == -1 且 close > pHi → dir = 1            // 收盤突破阻力帶 → 翻多
```
`flipBull` / `flipBear` 定義為「方向由非 X 變為 X」，即真正的**反手事件**
（而非每根 K 棒重複觸發）。

### 3. 回測再進場（Pullback）
```
pullBull = pullOn and dir == 1 and prevDir == 1
        and close > basis and close[1] <= basis[1]   // 收盤重新站上 EMA 基底
        and strategy.position_size == 0
        and longsOn and inSession and htfOk and cooldownOk and not eodReached
```
空頭對稱。條件要求「趨勢未變 + 空倉 + 收盤重新穿越基底」，屬**回測確認型**
進場，不追逐突破根。

### 4. 風險距離定倉（Risk-per-Trade + 槓桿封頂）
```
stopLine = dir == 1 ? lo : dir == -1 ? hi : na
dist      = abs(close - stopLine)                       // R 的定義基礎
riskMoney = strategy.equity * riskPct / 100
qRisk     = riskMoney / (dist * syminfo.pointvalue)     // 風險距離定量
qCap      = strategy.equity * maxLev / (close * syminfo.pointvalue)  // 槓桿封頂
qty       = floor(min(qRisk, qCap))
```
- `syminfo.pointvalue` 用於合約乘數（期貨）與每股價值（股票）的一致換算。
- `qty` 以 `int(math.floor(...))` 落地，符合 Pine qty 整數契約。
- `minQty` 為最小下單數量門檻；不足則不進場（避免碎單）。

### 5. 出場
- **盤中停損**：每根 K 棒以當前帶緣重掛 `strategy.exit(stop = lo / hi)`，
  帶緣隨棘輪單向移動 → 停損只會朝有利方向放寬。停損以「**持倉方向**」而非
  「趨勢方向」選擇（多頭部位一律用支撐帶 `lo`、空頭部位一律用阻力帶 `hi`），
  避免反手當根（方向已翻、部位尚未平倉的一根）保護失效。
- **R 倍數停利**：`limit = refPx ± tpR × entryDist`（`refPx` = 實際成交均價）。
- **時間類出場**：`maxHoldBars` 持倉 K 棒上限、`eodReached` 每日強制平倉。

### 6. HTF 趨勢偏見閘門（預設關閉）
```
htfEma   = request.security(syminfo.tickerid, htfTf, ta.ema(close, htfLen)[1],
              lookahead = barmerge.lookahead_on)
htfClose = request.security(syminfo.tickerid, htfTf, close[1],
              lookahead = barmerge.lookahead_on)
```
取**已收盤之 HTF 序列**（`[1]` 滯後 + `lookahead_on`）＝ 等同於「以 HTF 收盤
後的已知值判斷」，零前視偏差。預設關閉以保真原始行為。

## 非重繪契約

- 所有進場訊號僅於 `barstate.isconfirmed`（**已收盤 K 棒**）成立。
- `process_orders_on_close = false` → 訂單於**下一根 K 棒開盤**成交。
- 棘輪帶僅由已收盤之 `basis` / `atrV` 更新。
- HTF 序列一律 `[1]` 滯後 + `lookahead_on`，不引用未完成的 HTF K 線。
- `calc_on_every_tick = false`。

## 主要參數

| 群組 | 參數 | 預設 | 說明 |
|------|------|------|------|
| ① 趨勢引擎 | `baseLen` | 21 | EMA 基底週期 |
| ① 趨勢引擎 | `atrLen` | 10 | ATR 週期 |
| ① 趨勢引擎 | `mult` | 2.0 | 帶寬（× ATR）；越小＝帶緣越貼近＝反手與交易頻率越高 |
| ① 趨勢引擎 | `longsOn` / `shortsOn` | true | 多空開關 |
| ② 進出場 | `pullOn` | true | 啟用回測再進場 |
| ② 進出場 | `tpOn` / `tpR` | true / 2.0 | R 倍數停利 |
| ② 進出場 | `maxHoldBars` | 0 | 持倉 K 棒上限（0 = 不限） |
| ② 進出場 | `flipCooldown` | 0 | 反手冷卻 K 棒 |
| ③ 濾網 | `useHtfBias` / `htfTf` / `htfLen` | false / 60 / 200 | HTF 偏見閘門 |
| ③ 濾網 | `useSession` / `sessionStr` | false / 0930-1600 | 進場時段濾網 |
| ③ 濾網 | `useEodFlat` / `eodHour` / `eodMinute` | false / 15 / 55 | 每日強制平倉 |
| ④ 風險 | `riskPct` | 1.0 | 單筆風險（% 權益） |
| ④ 風險 | `maxLev` | 3.0 | 最大槓桿（名目 / 權益） |
| ④ 風險 | `minQty` | 1 | 最小下單數量 |

## 告警與 Webhook

文字告警：`Tn ATR Band Ratchet: BUY|SELL <symbol> <tf> (flip|pullback) · 帶緣 <px>`

JSON Webhook（`useWebhook = true`）：
```json
{
  "strategy": "TnSovereignAtrBandRatchetTrendV6",
  "version": "v26.1021.1830",
  "symbol": "<ticker>",
  "timeframe": "<period>",
  "side": "BUY",
  "kind": "flip",
  "band": 12345.6,
  "dist": 87.4
}
```
- `kind`：`flip`（反手）／`pullback`（回測再進場）。
- `band` 為當下帶緣價位（= 停損參考價）；`dist` 為進場點到帶緣的距離（即 1R）。

## 視覺層

- **帶緣光暈**：兩層寬帶描繪（外層透明度隨「壓力值」= 價格距帶緣的接近度
  動態收斂），內層為高透明填充。
- **EMA→帶緣綢帶**：`fill()` 繪製基底與帶緣之間的色帶，方向翻轉時自動換色。
- **反手菱形 / 回測圓點 / BUY·SELL 標籤**：區分兩種進場路徑。
- **統計面板**：趨勢方向、持倉方向與即時 R 值、進場距離、交易數與勝率、淨值
  百分比、HTF 偏見狀態。

## 來源與授權

- **原始來源**：[`loctai/pinescript`](https://github.com/loctai/pinescript) —
  `src/scripts/trend_following.pine`（182 行，v6 `strategy()`，MIT License）。
- **主權化差異**：HTF 偏見閘門、時段與每日平倉紀律、持倉上限與反手冷卻、
  整數落地之倉位數、R 倍數統計面板、JSON Webhook、去除任何績效宣稱字串。
- **授權**：MIT —— 保留原作者 MIT 聲明，衍生版本同以 MIT 釋出。

## 免責聲明

本文件描述之策略僅供研究與教學用途，不構成投資建議，亦不對任何標的、未來
報酬或績效指標作任何保證。實際交易須自行評估風險並承擔後果。

# TnSovereignCrowdSentimentConsensusV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1022.0630` · Causal Audit: `2026-10-22 06:30 CST`

## 策略定位

**9 因子加權共識投票 + CNN 風格群眾情緒量表（Fear & Greed）**：以九個獨立
技術因子（EMA 方向 / Supertrend / ADX 體制 / EMA 斜率 / WaveTrend /
StochRSI / WaveTrend 背離 / 相對強度 / ATR 品質）各投一票並以整數權重
加總為「共識分數」，再以**自製的 7 組分 Fear & Greed 量表**（CNN 公開方法論
之圖表資料重建版）作為**群眾擁擠濾網** —— 極度貪婪區不追多、極度恐慌區
不追空（除非訊號達「強訊號」標準），並以 **VIX 平靜濾網**（VIX < 自身 SMA）
限制多頭。部位以**風險距離定倉**（風險金額 ÷ ATR 停損距離）並以名目槓桿
封頂，出場為 **ATR 停損 + 反向訊號出場**（可選 R 停利 / ATR 追蹤停損）。

## 與現有庫之差異

現有庫的宏觀／多智能體類策略（`sentiment_macro_sovereign_v6`、
`macro_modeling_sovereign_v6`、`federated_consensus_sovereign_v6`、
`momentum_swarm_sovereign_v6`）**無任何「Fear & Greed 群眾情緒量表」**：

- 全庫 `grep -ril "fear" strategies/*.pine` **零命中**；`greed` 僅命中
  `TnSovereignNeuraRLV6` 之中性文字，無情緒量表實作。
- `sentiment_macro_sovereign_v6` 使用 **`request.seed()`（Pine Seeds 付費
  功能）** 取得外部情緒資料，無法在免費環境運行；本策略 **100% 依賴
  內建圖表與跨標的日頻序列**，零付費依賴、零 HTTP。
- 本策略為全庫**第一個「情緒量表直接作為進場閘門」**（而非僅作為顯示圖層）
  的策略：FG 量表以 7 組分加權正規化成 0-100，並直接決定「是否允許追多 /
  追空」。

## 核心邏輯

### 1. 9 因子加權共識投票
```
score = Σ (vote_i × weight_i)          // 總權重 = 12（預設）
vote_i ∈ {+w_i, −w_i, 0}
```
| 因子 | 判定 | 預設權重 |
|------|------|---------|
| EMA 方向 | `emaFast > emaSlow` | 2 |
| Supertrend | `stDir < 0`（多頭） | 2 |
| ADX 體制 | `close > emaLong` 且 `ADX ≥ 門檻` 且 DI 對齊 | 2 |
| EMA 斜率 | `slope% ≥ minSlopePct` | 1 |
| WaveTrend | `wt1 > wt2` | 1 |
| StochRSI | `K > D` | 1 |
| WaveTrend 背離 | 樞軸確認後的多頭／隱藏背離 | 1 |
| 相對強度 | 標的報酬 − 基準報酬（雙基準） | 1 |
| ATR 品質 | 波動率位於正常區間且方向與快線一致 | 1 |

多頭門檻 `score ≥ 10`、空頭門檻 `score ≤ −10`；`score ≥ 12`（門檻 + 偏移 2）
為**強訊號**（可單獨放行情緒阻擋）。

### 2. 門禁矩陣（Gate Matrix）
```
longGate = bullReg and not rangeReg and volOK and rsLongOK and betaLongOK
         and volatilityOK and notChasing and srBull and k < stochLongMax
```
- **量能確認**：`RVOL = volume / SMA(volume, 20) ≥ 1.20`。
- **波動區間**：`ATR / SMA(ATR, 50) ∈ [0.80, 3.00]`，排除失真壓縮與失控爆發。
- **追價距離**：`|close − emaFast| / ATR ≤ 1.5`，不追離均線過遠的訊號。
- **StochRSI 上緣**：`K < 80` 方可追多、`K > 20` 方可追空。
- **RS / Beta**：`useRSFilter` 與 `useBetaFilter` 預設**關閉**（原作者實測
  無穩健價值，保留可開啟以供研究）。

### 3. 群眾情緒量表（Fear & Greed, CNN 風格 7 組分）
```
z  = (raw − SMA(raw, N)) / stdev(raw, N)      // 「偏離均值的程度 / 通常偏離的程度」
score = 100 × Φ(z)                             // Φ 由 erf 近似（A&S 7.1.26）
```
| # | 組分 | 原始值 | 方向 |
|---|------|--------|------|
| ① | 市場動能 | `100 × (SPY / SMA(SPY,125) − 1)` | 高＝貪婪 |
| ② | 價格強度 | 252 日區間位置（0-100） | 高＝貪婪 |
| ③ | 市場寬度 | 上漲日量能占比（20 日） | 高＝貪婪 |
| ④ | 避險／恐慌代理 | `(20 日高 − close) / ATR` | **反號**（高＝恐慌） |
| ⑤ | 垃圾債風險偏好 | `HYG 20 日報酬 − IEF 20 日報酬` | 高＝貪婪 |
| ⑥ | 波動率 | `VIX / SMA(VIX, 50)` | **反號**（高＝恐慌） |
| ⑦ | 避險需求 | `SPY 20 日報酬 − IEF 20 日報酬` | 高＝貪婪 |

分區：`≤ 24` 極度恐慌、`25-44` 恐慌、`45-55` 中性、`56-75` 貪婪、`≥ 76` 極度貪婪。

### 4. 群眾擁擠阻擋 + VIX 平靜濾網
```
fgBlockLong  = useFGBlock and fgExtGreed and not strongLong     // 極度貪婪不追多
fgBlockShort = useFGBlock and fgExtFear  and not strongShort    // 極度恐慌不追空
tradeLong    = ... and (not useVIXCalm or vixCalm)               // VIX < SMA50 方可做多
```
- **反群眾但不反趨勢**：在極端情緒區**不追**新倉（而非反向開倉），避免把
  情緒量表誤當反轉訊號；強訊號可放行。
- **熊市體制空頭閘門**：`canShort` 預設要求基準（SPY）日收盤 < 自身
  SMA(200)，即**空頭僅在基準位於長期均線下方時放行**（原作者之語義，
  主權版保留並於文件明確標示）。

### 5. 風險距離定倉（雙重封頂）
```
stopDist = ATR(14) × stopMultEff       // 日線以上 2.0×；盤中 0.75×
riskCash = equity × riskPct% × 確信倍率
qtyRisk  = riskCash / stopDist
qtyCap   = equity × maxLev / (close × syminfo.pointvalue)   // 名目槓桿封頂
qty      = int(max(1, floor(min(qtyRisk, qtyCap))))
```
`syminfo.pointvalue` 用於期貨合約乘數與股票每股價值的一致換算。

### 6. 出場
- **ATR 停損**：進場當下 `close ∓ stopDist`，每筆部位獨立掛單。
- **反向訊號出場**：反向訊號先發出場單（並取消舊停損），再發進場單，
  避免「同一根 K 棒同時持多空」競態；反手於下一根 K 棒開盤乾淨成交。
- **時間類出場**：每日強制平倉（`useEodFlat`）、持倉 K 棒上限（`maxHoldBars`）。

## 非重繪契約

- 所有進場訊號僅於 `barstate.isconfirmed`（**已收盤 K 棒**）成立。
- `process_orders_on_close = false` → 訂單於**下一根 K 棒開盤**成交。
- 跨標的序列一律以 `lookahead = barmerge.lookahead_on` 取得**已收盤日頻值**
  （原生作者使用 `lookahead_off`，於日內圖表會取到「形成中」的當日收盤
  而造成盤中重繪，本版已修正）。
- 日頻統計（動能均線、VIX 均線、Z-Score 視窗）一律在**日頻上下文內**計算。
- `calc_on_every_tick = false`。

## 主權化修正（相對原作者）

1. **修復 `invalid symbol` runtime error**：原作者 README 自述此錯誤未解。
   本版所有 `request.security` 均加入 `ignore_invalid_symbol = true`，
   標的不可用時回傳 `na` 並由守門判斷接管，腳本不再拋錯中斷。
2. **消除日頻序列盤中重繪**：全面改用 `lookahead_on` 取已收盤日值。
3. **消除 Fear & Greed 之時框錯配**：組分 ①②③④⑥ 原以「圖表 K 棒」計算
   252 根 Z-Score 視窗（於日內圖表僅覆蓋數小時），本版改在日頻上下文內
   正規化；組分 ⑤⑦ 為跨資產價差，改以**日頻錨定滾動統計**（每日僅更新
   一次的環形緩衝區）計算 Z 值，視窗恆等於「日」。
4. **部位數量雙重封頂**：新增名目槓桿上限並以 `int` 落地。
5. **新增紀律**：時段濾網、每日強制平倉、持倉 K 棒上限、JSON Webhook。
6. **移除所有績效宣稱字串**（PF / expectancy / 勝率 / 樣本數），本系統
   不作任何績效陳述或保證；原作者之誠實聲明改寫為「未經本庫獨立驗證」。

## 主要參數

| 群組 | 參數 | 預設 | 說明 |
|------|------|------|------|
| ① 趨勢 | `emaFastLen` / `emaSlowLen` / `emaLongLen` | 21 / 50 / 200 | EMA 三層結構 |
| ② Supertrend | `stLen` / `stMult` | 10 / 3.0 | Supertrend ATR 週期與乘數 |
| ③ 體制 | `adxLen` / `adxThresh` / `requireDiAlign` | 14 / 20 / true | ADX 體制與 DI 對齊 |
| ④ WaveTrend | `wtN1` / `wtN2` | 10 / 21 | 通道與平均週期 |
| ⑤ StochRSI | `rsiLen` / `stochLen` / `smoothK` / `smoothD` | 14 / 14 / 3 / 3 | StochRSI 參數 |
| ⑥ 背離 | `lbL` / `lbR` / `divMinBars` / `divMaxBars` | 5 / 5 / 5 / 60 | 樞軸與背離有效窗 |
| ⑦ RS/Beta | `useRSFilter` / `useBetaFilter` | false / false | 相對強度與 Beta 濾網（預設關閉） |
| ⑧ 風險 | `atrLen` / `atrStopMult` / `riskPct` / `maxLev` | 14 / 2.0 / 1.0 / 2.0 | ATR 停損、風險%、槓桿封頂 |
| ⑨ 量能 | `volLen` / `rvolMin` | 20 / 1.20 | RVOL 確認 |
| ⑩ 訊號 | `longThresh` / `shortThresh` / `strongOffset` / `cooldownBars` | 10 / 10 / 2 / 5 | 分數門檻、強訊號偏移、冷卻 |
| ⑪ 策略 | `useBearGate` / `bearLen` / `useOppExit` / `useTarget` / `useTrailing` | true / 200 / true / false / false | 熊市閘門與出場組態 |
| ⑫ 情緒 | `fgZLen` / `fgMomLen` / `fgRetLen` / `fgFear` / `fgGreed` | 252 / 125 / 20 / 24 / 76 | 量表視窗與分區 |
| ⑫ 情緒 | `useFGBlock` / `useFGConv` / `useVIXCalm` / `useVIXPanic` | true / false / true / false | 情緒閘門與 VIX 濾網 |

## 告警與 Webhook

文字告警：`CSS LONG/SHORT <symbol> <tf> qty <n> stop <px>`

JSON Webhook（`useWebhook = true`）：
```json
{
  "strategy": "TnSovereignCrowdSentimentConsensusV6",
  "version": "v26.1022.0630",
  "symbol": "<ticker>",
  "timeframe": "<period>",
  "side": "BUY",
  "kind": "strong_long",
  "score": 11,
  "fg": 78,
  "stop": 512.34,
  "qty": 42
}
```
- `kind`：`long` / `strong_long` / `short` / `strong_short`。
- `fg` 為當下 Fear & Greed 量表值（0-100）。

## 視覺層

- **BUY / SELL 標記**：一般訊號為小三角，強訊號為大三角。
- **停損線**：持倉期間於圖上繪製當前 ATR 停損價位。
- **Fear & Greed 獨立面板**：量表折線 + 極度貪婪／恐慌門檻線 + 區間填色。
- **統計面板**：訊號與冷卻時距、共識分數、體制與 RVOL、部位、進場價、
  未實現 R、淨損益、交易次數、情緒量表與 VIX 狀態。

## 來源與授權

- **原始來源**：[`kdricha0602/kernal-cipher`](https://github.com/kdricha0602/kernal-cipher) —
  `Kernal-Cipher-Strategy.pine`（518 行，v6 `strategy()`，MIT License，
  Copyright 2026 Korben Richards）。
- **主權化差異**：`invalid symbol` 錯誤修補、日頻序列去重繪、FG 量表時框
  錯配修正、名目槓桿封頂、時段／每日平倉紀律、JSON Webhook、移除績效
  宣稱字串。
- **授權**：MIT —— 保留原作者 MIT 聲明，衍生版本同以 MIT 釋出。

## 免責聲明

本文件描述之策略僅供研究與教學用途，不構成投資建議，亦不對任何標的、
未來報酬或績效指標作任何保證。本移植未經本庫獨立回測驗證，實際交易
須自行評估風險並承擔後果。

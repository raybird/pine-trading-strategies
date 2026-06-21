# TnSovereignNqOprBreakoutV6

**版號：** v26.0622.0630  
**分類：** Volatility & Breakout / NQ NY Session OPR Breakout  
**核心概念：** NQ NY 交易時段開盤價格區間 (OPR) 突破策略 + RSI/EMA 過濾 + 擺動止損

---

## 策略哲學

NQ（納斯達克期貨）的紐約交易時段開盤區間是日內最具結構性意義的價格發現階段。大型機構在 NY 開盤時的訂單流決定了當日價格方向。本策略捕捉 NY 時段的 OPR 突破，並透過 RSI 體制閘門、EMA 趨勢對位與擺動高低點動態止損進行三重確認，確保突破交易的品質。

## 核心邏輯

### 1. 開盤區間 (OPR) 累積
- 自定義區間起始時間（預設 09:30 NY 時間）
- 可配置區間持續時間（預設 5 分鐘）
- 累積該時間窗口內的最高/最低價作為突破閾值

### 2. 時段閘門
- `Trade Open` ~ `Trade Stop`：僅在此時間窗口內允許進場
- `Trade Close`：強制平倉所有持倉
- 支援多種時區設定（預設 America/New_York）

### 3. RSI 過濾（可選）
- 三種模式：Outside（超買/超賣區）、Inside（非極端區）、Off（關閉）
- 多頭：RSI 在超買區域或非極端區域（依模式）
- 空頭：RSI 在超賣區域或非極端區域（依模式）

### 4. EMA 趨勢過濾（可選）
- 預設 50 EMA
- 多頭：價格在 EMA 之上且低點也在 EMA 之上
- 空頭：價格在 EMA 之下且高點也在 EMA 之下

### 5. 擺動止損
- 偵測最近 20 根 K 線內的擺動高/低點
- 止損設置在擺動高/低點外側（緩衝 10 tick）
- 若擺動點超出 OPR 區間，則以 OPR 區間為限

### 6. 每日一單
- 每個交易日最多執行一筆交易
- 防止過度交易與報酬遞減

## 輸入參數

| 群組 | 參數 | 預設值 | 說明 |
|------|------|--------|------|
| Time Settings | Range Start | 09:30 | 區間累積起始時間 (NY) |
| Time Settings | Range Duration | 5 min | 區間持續長度 |
| Time Settings | Trade Open | 09:35 | 進場窗口開始 |
| Time Settings | Trade Stop | 16:00 | 進場窗口結束 |
| Time Settings | Trade Close | 16:30 | 強制平倉時間 |
| Time Settings | Timezone | America/New_York | 時區 |
| RSI Filter | Enable RSI | true | 啟用 RSI 過濾 |
| RSI Filter | RSI Overbought | 70 | RSI 超買閾值 |
| RSI Filter | RSI Oversold | 30 | RSI 超賣閾值 |
| RSI Filter | RSI Condition | Outside | RSI 條件模式 |
| EMA Filter | Enable EMA | false | 啟用 EMA 過濾 |
| EMA Filter | EMA Period | 50 | EMA 週期 |
| Risk Management | Separate R:R | false | 多/空分離 R:R |
| Risk Management | Common R:R | 1.5 | 共同 R:R |
| Risk Management | R:R Long | 1.5 | 多頭 R:R |
| Risk Management | R:R Short | 1.5 | 空頭 R:R |

## 資料來源

移植自 [jcornierfra/TradingView_Strategy_JCO_OPR_Breakout](https://github.com/jcornierfra/TradingView_Strategy_JCO_OPR_Breakout)（Breizhoo 開發），經 TeleNexus Sovereign 改造加入主權規訓、因果審計與強化風險管理。

## 相依性

- Pine Script v6
- 無外部函式庫依賴

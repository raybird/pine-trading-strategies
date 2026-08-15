# TnSovereignMaRelationshipV6

**版號：** v26.0815.1830
**分類：** Trend & Momentum / MA Relationship Diagnostic
**來源：** casoon/pine-scripts (WavesUnchained) — strategies/market_average_relationship_engine v1.2.0 (2026-08-12)

---

## 策略哲學

MA 交叉是脆弱的——兩條均線短暫交錯便觸發訊號，卻缺乏對「價格與市場參考線之間關係品質」的量測。本策略直接審計**價格與單一「市場參考 MA」的六維關係**，而非追逐交叉本身：

- 把 MA 當作市場的參考基準（market reference），而非獨立交叉訊號。
- 六個維度各自給出 0..100 品質分數（Trend / Respect / Extension / Compression / Acceleration / Exhaustion）。
- 融合為「關係振盪器」（Relationship Oscillator，-100..+100），搭配 11 態狀態引擎。
- 事件引擎僅在**已確立的品質趨勢**上啟動兩種順勢入場家族：**拉回 Dip-Buy** 與**壓縮釋放（Compression Release）**，並以冷卻期防止重複觸發。

## 核心邏輯

### 1. 六維診斷（每維 0..100）

| 維度 | 方法 |
|------|------|
| **Trend** | MA 斜率強度 + 側向持續性 + 斜率持續性 + 價格效率比值 + 方向共識（0.30/0.25/0.20/0.15/0.10 權重） |
| **Respect** | 歷史 MA 互動品質統計——回測視窗內每次價格觸及 MA 帶（proximity×ATR）後 responseBars 的勝率與 outcome 品質，以樣本數調整信賴度；混合當前側向翻轉率穩定性 |
| **Extension** | ATR 常態化距離（0.70 權重）+ Z-score 統計罕見度（0.30 權重） |
| **Compression** | MA 附近聚集比例（0.50）+ 聚集緊密度（0.30）+ 波動率收縮（0.20） |
| **Acceleration** | 分離速度（0.50）+ 斜率加速度（0.20）+ 報酬加速度（0.30） |
| **Exhaustion** | 延伸前置條件 × (效率衰減 0.35 + 逆向影線壓力 0.25 + 進展失敗 0.25 + 加速度喪失 0.15) |

### 2. 關係振盪器與狀態引擎
- `relationship = signedTrend × (1 - 品質懲罰)`，品質懲罰由超過追價門檻的 Extension 與超過警戒門檻的 Exhaustion 組成（上限 0.50）。
- 11 態：MA Compression / Bull·Bear Exhaustion Risk / Bull·Bear Do-Not-Chase / Bull·Bear Acceleration / Healthy Bull·Bear Trend / Developing Relationship / Neutral。

### 3. 事件引擎（七家族，全部 bar 收線確認 + 家族冷卻）
- **Pullback（入場）**：既有品質趨勢 + Respect ≥ 門檻 + 近期先有 ≥0.7×ATR 延伸 + 在 MA 帶內出現順勢吞沒式拒絕（close 收於 MA 同側且 > 中點）+ 耗竭 ≤ 上限 → 順勢掛品質拉回。
- **Compression Release（入場）**：先前有壓縮 ≥ 門檻 + signedDistanceAtr 豁越 ±0.45×ATR + MA 斜率同向 + 加速度 ≥ 60 + 效率 ≥ 0.35 + 非耗竭 → 壓縮釋放動量突破。
- **Do-Not-Chase / Exhaustion / Break / Divergence / Turn**：診斷與風控警示，刻意不混入順勢入場（避免趨勢與反轉邏輯同訊號的 anti-pattern）。

### 4. 風險管理（生成層）
- **ATR 錨定停損**：longStop = MA − 2.5×ATR；shortStop = MA + 2.5×ATR。
- **波動尖峰出場**：ATR ≥ 1.6 × EMA(ATR,50) 時強制平倉（捕捉高潮/耗竭棒）。
- **Break-Even**：獲利 ≥ 1×ATR 後將停損移至成本價。
- **完整濾網**：Session / Date Range / Max Drawdown / Max Intraday Loss / Losing Streak / Exit Cooldown / 方向（Both/Long/Short Only）。

### 5. 主權覆蓋層
- **無未來函數**：所有事件 bar 收線確認；respect 統計僅窮舉已確認的歷史互動；divergence pivot 純診斷不閘門。
- **10 種 MA 家族可選**（EMA/SMA/WMA/HMA/VWMA/RMA/DEMA/TEMA/ALMA），單一參考線貫穿全模型。
- **12 維 Data Window 儀表板 + 7 組 alert + tooltip 診斷**。

## 參數速查

| 參數 | 預設 | 說明 |
|------|------|------|
| MA family / length | EMA / 50 | 市場參考線家族與週期 |
| extensionNormal/Extreme | 0.75× / 2.50× ATR | 延伸常態/極端閾值 |
| respect lookback / response | 80 / 4 bars | MA 互動品質取樣 |
| minimumTrend / minimumRespect | 55 / 55 | 品質趨勢/尊重門檻 |
| acceleration / compression threshold | 60 / 65 | 動能釋放門檻 |
| chaseExtension / exhaustion | 75 / 68 | 追價/耗竭警戒 |
| stopAtrMult | 2.5× | MA 錨定停損距離 |
| volExitRatio | 1.6 | 波動尖峰平倉比 |

---
*Causal Audit: 2026-08-15 18:30 CST | Calibrated: Sovereign*
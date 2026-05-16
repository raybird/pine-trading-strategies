# Tn Sovereign VWAP Regime Deviation Strategy v6

**版本號**: v26.0517.0630
**物理時間**: 2026-05-17 06:30:09 CST
**標準**: Pine Script v6

---

## 核心精神

本策略基於「機構級 VWAP 偏離偵測」與「動態標準差帶 regime 分類」。當價格對 VWAP 的偏離達到統計顯著水準（通常 2σ 以上）且市場處於區間震盪模式時，觸發均值回歸信號。

---

## 邏輯矩陣

| 層次 | 組件 | 功能 |
|------|------|------|
| 1 | **VWAP Core** |  session-anchored 公平價值基準 |
| 2 | **Deviation Engine** | 測量價格對 VWAP 的標準差偏離單位 |
| 3 | **Regime Filter** | ADX 閾值區分趨勢 vs 區間市場 |
| 4 | **Liquidity Sweep Detection** | 偵測價格掃描 VWAP 極端偏離的行為 |
| 5 | **Causal Audit** | 狀態機記錄 regime 轉換用於主權驗證 |

---

## 參數說明

| 參數 | 預設值 | 說明 |
|------|--------|------|
| VWAP Source | close | 計算 VWAP 的價格來源 |
| StdDev Lookback | 20 | 標準差計算週期 |
| Upper Band Multiple | 2.0 | 上軌標準差倍數 |
| Lower Band Multiple | -2.0 | 下軌標準差倍數 |
| ADX Trend Threshold | 25 | ADX 趨勢判定閾值 |
| SL ATR Multiple | 1.5 | 止損 ATR 倍數 |
| Target R:R Ratio | 2.5 | 目標風報比 |

---

## 進場邏輯

- **多頭進場**：偏離度由下穿越 `multDn`（如 -2.0）+ ADX 低於閾值（區間市場）+ 前一根 K 棒偏離度仍在區間內
- **空頭進場**：偏離度由上穿越 `multUp`（如 +2.0）+ ADX 低於閾值（區間市場）+ 前一根 K 棒偏離度仍在區間內

---

## 風控機制

- 動態 ATR 止損（1.5× ATR）
- 固定 R:R 出場（2.5 倍）
- 無期貨對沖模式下僅做多/做空

---

## 適用市場

- **優化市場**：ETF、股票、指數型商品（高流動性）
- **時段**：亞洲盤 / 歐洲盤初期（區間特性顯著）
- **風險提醒**：趨勢型市場（ADX > 25）應降低倉位或暫停使用

---

**⚠️ 免責聲明**：本策略僅供技術研究，不構成投資建議。
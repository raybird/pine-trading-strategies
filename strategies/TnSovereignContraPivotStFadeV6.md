# TnSovereignContraPivotStFadeV6 — TeleNexus 主權樞軸 SuperTrend 反向（Fade）策略

## 概述
移植自 `jayadevrana/pinescript-contra-pivot-supertrend-fade-strategy` 的 `contra-pivot-supertrend-v6.pine`。以「樞軸點 SuperTrend band」為觸發核心，採用**逆向交易（Fade）**邏輯：當價格強勢延伸觸及/穿越 band 時反向做單，配合 ORB 開盤區間、ADX、ATR、EMA 四層過濾與金字塔加倉管理。

## 核心邏輯

### 樞軸 SuperTrend（Pivot Point SuperTrend）
- 以 `ta.pivothigh/low` 偵測擺動點，EMA 平滑式加權更新樞軸中心 `center`
- 上/下軌 = `center ± ATR × ppFactor`，追蹤機制與標準 SuperTrend 一致
- `trend` 狀態機決定目前朝向（1 = 多 / -1 = 空），`pps` 為目前 band 值

### 反向觸發（Fade Trigger）
- **Touch**：價格自正確側觸及 band（`high >= tdown` / `low <= tup`）
- **Reversal**：SuperTrend 體制翻轉（多翻空→Fade 做多；空翻多→Fade 做空）
- **Both**（預設）：任一觸發即進場

### 過濾層
- **ORB（開盤區間）**：僅在區間外（`close > orbHigh` 做空 / `close < orbLow` 做多）進場
- **ADX**：`adxVal >= minAdx`（預設 20），確認趨勢有強度
- **ATR**：可選，`atrVal > atrThr`
- **EMA 50**：做多需 `close < ema`（逆勢），做空需 `close > ema`

## 風險管理
- **金字塔**：最多 `numPyr` 次，間距可選 Points / Percent / ATR
- **Target**：Points / Percent 兩型，可關閉
- **Stop Loss**：Points / Percent 兩型，可關閉
- **Trailing**：Points / Percent，只收緊不放大
- **Re-Entry 狀態隔離**：金字塔錨點由實際成交均價重新播種，狀態不跨交易殘留

## 診斷
右下角診斷表即時顯示：ST 體制、touch/reversal、ORB、ADX、ATR、EMA、進場訊號、倉位、金字塔數與 ORB 高低。

## 版號
- 版本：v26.0803.1922
- 審計時間：2026-08-03 19:22 CST
- 來源：jayadevrana/pinescript-contra-pivot-supertrend-fade-strategy

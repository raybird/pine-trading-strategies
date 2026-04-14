# TN Sovereign Market Structure v6

## 1. 策略概述
**TN Sovereign Market Structure v6** 是一款專注於捕捉價格結構位移（Market Structure Shift）的量化策略。其核心邏輯在於識別 **BOS (Break of Structure)** 與 **CHOC (Change of Character)** 節點，並透過一目均衡表（Ichimoku Cloud）與 EMA 雙重因果錨點過濾偽信號，確保執行行為具備高度的執政主權。

- **版本**: v6.0 (Pine Script v6)
- **實體化日期**: 2026-04-14 (台灣時間 CST)
- **核心架構**: Pivot High/Low + Ichimoku Causal Anchor + Sovereign Risk Engine

## 2. 因果審計邏輯

### 第一層：市場結構判定 (Market Structure)
- **機制**: 透過設定左/右 K 線數偵測局部樞軸點（Pivots）。
- **BOS 識別**: 當價格有效突破前一個同向樞軸點時，視為結構的延續（BOS）。
- **趨勢轉向**: 突破異向樞軸點則觸發 CHOC，重置系統的趨勢偏好。

### 第二層：因果動能對焦 (Causal Anchors)
- **EMA 50 物理地板**: 價格必須位於 EMA 50 之上方（多頭）或下方（空頭）。
- **一目雲帶濾波**: 整合 Senkou A/B 雲帶，僅在價格位於雲帶上方（多頭）或下方（空頭）時觸發執行，排除雲帶內的震盪噪聲。

## 3. 風險規訓 (Risk Management)
- **動態倉位分配**: 根據 ATR (14) 計算止損距離（1.5x ATR），確保單筆交易風險嚴格鎖定在帳戶權益的 1.0%。
- **盈虧比硬化**: 設定 3.0x ATR 的止盈目標，實現高度不對稱的期望值。

## 4. 執行說明
本策略已全面對焦 Pine Script v6 標準，並執行嚴格的物理時間對位（v26.0414.*）。建議執行於 1 小時（1H）或 15 分鐘（15m）時框，並開啟 BOS 過濾功能以獲得最高信號主權。

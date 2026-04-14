# TN Stochastic Causal Divergence v6

## 1. 策略概述
**TN Stochastic Causal Divergence v6** 是一款專注於捕捉價格與動能結構性背離的高階量化策略。其核心邏輯在於透過隨機指標（Stochastic Oscillator）的背離來識別趨勢竭盡點，並結合高時框（HTF）因果錨點與動態波動率過濾，確保執行行為具備高度的執政主權與因果確定性。

- **版本**: v6.0 (Pine Script v6)
- **實體化日期**: 2026-04-15 (台灣時間 CST)
- **核心架構**: Divergence Detection Engine + HTF Causal Filter + Sovereign Risk Management

## 2. 技術邏輯分析

### 第一層：結構性背離引擎 (Divergence Engine)
- **牛市背離 (Bullish Divergence)**: 價格創下新低（Lower Low），但隨機指標形成較高的低點（Higher Low）。這象徵著空頭物理壓力的減弱。
- **熊市背離 (Bearish Divergence)**: 價格創下新高（Higher High），但隨機指標形成較低的高點（Lower High）。這象徵著多頭慣性的喪失。
- **樞軸審計 (Pivot Audit)**: 採用左側 5 根、右側 2 根 K 線的樞軸判定，過濾短期的隨機波動。

### 第二層：因果過濾層 (Causal Filter)
- **HTF 趨勢地板**: 檢索 4 小時時框（240m）的 200 日 EMA 作為趨勢錨點。
- **目的**: 確保微觀執行與宏觀因果方向一致，避免在逆勢中觸發高風險交易。

### 第三層：超買/超賣對位 (OB/OS Alignment)
- 僅在指標處於極端區域時觸發執行（多頭 < 30，空頭 > 70），以最大化反轉後的物理空間。

## 3. 風險規訓 (Risk Management)
- **動態倉位分配**: 使用 ATR (14) 計算止損距離（2.0x ATR），並依據 1.0% 固定風險分配下單單位。
- **盈虧比硬化**: 設定 4.0x ATR 的止盈目標，實現 1:2 的核心期望值。

## 4. 執行說明
本策略已全面對焦 Pine Script v6 標準，並執行嚴格的物理時間對位規訓（v26.0415.*）。建議執行於 1 小時（1H）或 15 分鐘（15m）圖表時框，並開啟 Dashboard 實時監控因果錨點狀態。

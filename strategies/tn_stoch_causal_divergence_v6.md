# TN Stochastic Causal Divergence v6

## 1. 策略概述
**TN Stochastic Causal Divergence v6** 是一款結合了結構性背離分析與高時框因果過濾的量化策略。其核心在於識別價格與隨機指標（Stochastic Oscillator）之間的因果不一致性，並透過宏觀趨勢錨點確保執行行為具備高度的確定性。

- **版本**: v6.0 (Pine Script v6)
- **實體化日期**: 2026-04-14 (台灣時間 CST)
- **核心架構**: Divergence Engine + HTF Causal Anchor + Sovereign Risk Management

## 2. 技術邏輯分析

### 第一層：背離引擎 (Divergence Engine)
- **牛市背離 (Bullish Divergence)**: 價格創下新低（Lower Low），但隨機指標創下更高的低點（Higher Low）。這象徵著空頭物理動能的衰竭與多頭因果的潛在反轉。
- **熊市背離 (Bearish Divergence)**: 價格創下新高（Higher High），但隨機指標創下更低的高點（Lower High）。這象徵著多頭慣性的喪失。
- **樞軸檢測 (Pivot Detection)**: 採用左側 5 根、右側 2 根 K 線的樞軸邏輯，確保信號的結構穩定性。

### 第二層：因果過濾器 (Causal Filter)
- **HTF 趨勢錨點**: 強制要求執行方向必須與 4 小時時框（240m）的 50 日 EMA 一致。
- **區域限制**: 多頭信號僅在指標低於 30（超賣區邊緣）時觸發；空頭信號僅在指標高於 70（超買區邊緣）時觸發。

## 3. 風險規訓 (Risk Management)
- **動態倉位調整**: 使用 ATR (14) 計算止損距離（2.0x ATR），並根據 1.0% 的固定帳戶風險比例動態演算下單量。
- **盈虧對位**: 設定 4.0x ATR 的止盈目標，實現 1:2 的優質盈虧比。

## 4. 執行說明
本策略已對焦 Pine Script v6 標準，採用嚴格的物理時間對位規訓（v26.0414.*）。建議執行於 1 小時（1H）或 15 分鐘（15m）時框，以獲得最佳的信號對位效果。

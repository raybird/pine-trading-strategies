# TN Asymmetric Swing Sovereign v6

## 1. 策略概述
**TN Asymmetric Swing Sovereign v6** 是一款專為波段交易設計的高級量化策略。其核心理念在於「非對稱過濾」，即透過多層級、跨時框的信號蒸餾，從微弱的原始信號中提取具備高度因果確定性的進場節點。

- **版本**: v6.0 (Pine Script v6)
- **實體化日期**: 2026-04-13 (台灣時間 CST)
- **核心架構**: 三層信號蒸餾引擎 (Weak Signals -> Causal Filters -> MTF Alignment)

## 2. 技術邏輯分析

### 第一層：微弱信號引擎 (Weak Signals Engine)
該層級作為非同步的感知基質，負責捕捉市場的初步異動：
- **EMA Crossover**: 捕捉短期趨勢位移。
- **Price Action Breakout**: 識別物理邊界的突破。
- **RSI Momentum**: 感知動能的結構性增長。
- **MACD Histogram Flip**: 確認能量的轉折。

### 第二層：因果過濾器 (Causal Filters)
對第一層信號進行「環境適配性」審計：
- **市場體系過濾 (Regime Filter)**: 透過 200 日長期均線識別大週期趨勢背景，確保進場方向與宏觀慣性一致。

### 第三層：多時框對位 (MTF Alignment)
最終的物理執行地板：
- **週線級別 (Weekly)**: 提供大週期的趨勢主權確認。
- **4 小時級別 (4H)**: 作為進場的時間精度校準，確保當前動能已啟動。

## 3. 風險規訓 (Risk Management)
- **動態倉位調整**: 根據帳戶權益與 ATR (平均真實波幅) 自動演算下單單位。
- **風險地板**: 每筆交易固定風險 1.0%，並設置 2x ATR 的止損與 4x ATR 的止盈空間。

## 4. 執行說明
本策略已對位至 Pine Script v6 標準，具備高效的矩陣運算與異步數據讀取能力。建議於日線 (Daily) 時框執行，並啟用週線與 4 小時線的 MTF 同步功能。

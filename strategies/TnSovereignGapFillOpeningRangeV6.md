# Tn Sovereign Gap Fill Opening Range v6

## 策略概述
跳空填補與開盤區間突破策略，採用 Pine Script v6.0 標準構建。核心基於 **缺口分類審計**（全缺口/部分缺口）與 **開盤區間 (ORB)** 突破，整合多日缺口記憶與因果狀態審計足跡。

## 核心特性
- **主權缺口偵測 (Sovereign Gap Detection)**:
    - 自動分類全日缺口 (`isFullGap`) 與部分缺口 (`isPartialGap`)。
    - 多日缺口記憶（D-1 / D-2 / D-3）與缺口簇 (`gapCluster`) 識別。
- **開盤區間突破 (ORB Breakout)**:
    - 可調開盤區間分鐘數，偵測區間高低突破 (`breakUp` / `breakDown`)。
    - 結合缺口類型與成交量確認，過濾無效突破。
- **缺口填補邏輯 (Gap Fill / Mean Reversion)**:
    - 均值回歸模式：缺口方向 + RSI 極端值過濾，捕捉缺口回補動能。
- **因果狀態審計 (Causal State Audit)**:
    - 每筆交易記錄入場類型（GapFill / Break）、缺口百分比、入場價格與 Bar Index。
- **動態風險對位**:
    - ATR 動態止損 (1.5x) 與 1:2 以上盈虧比規訓。
- **時段感知 (Session-Aware)**:
    - 支援亞洲/倫敦/紐約三大時段獨立開關。

## 模組說明
1. **Session**: 時段偵測與開盤區間管理。
2. **Gap Detection**: 主權缺口分類與多日記憶。
3. **Signals**: 缺口填補與區間突破雙模式訊號。
4. **Audit**: 因果審計足跡與即時 HUD 儀表板。

## 使用建議
- **推薦標的**: 股指期貨、外匯主流對、高流動性個股。
- **推薦時框**: 15M (執行) 搭配 1H (環境確認)。
- **版本號**: v25.0525.1830

# ZZC Market Structure Sovereign Strategy

## 策略概述
這是一款基於波段結構 (ZigZag) 與主權隧道 (Corridors) 邏輯的高階交易策略，採用 Pine Script v6.0 標準構建。它透過非重繪的樞紐點判定市場波動方向，並利用 Keltner 隧道定義價格的主權邊界，旨在市場結構確認後的穩定波段中進場。

## 核心特性
- **因果波段核心**: 使用 `pivothigh/pivotlow` 配合物理時間確認邏輯，杜絕未來函數，確保信號的因果透明度。
- **主權隧道規訓**: 利用 Keltner Channels 定義市場的「正常波動邊界」，區分趨勢持續與過度擴張狀態。
- **自適應風險管理**: 止損與獲利目標完全基於 ATR 波動率自動調整，實現動態風險對位。
- **物理時間對位**: 版本號與代碼標註嚴格對齊系統物理時間 (CST)，確保執行軌跡的可追蹤性。

## 模組說明
1. **Module 1 (ZigZag Core)**: 負責識別市場的結構性樞紐點。
2. **Module 2 (Market Structure)**: 建立主權隧道背景，過濾無效噪音。
3. **Module 3 (Sovereign Execution)**: 執行具備主權保護的進出場邏輯。
4. **Module 4 (Visualization & Audit)**: 即時渲染執行儀表板，提供透明的運行指標。

## 使用建議
- **推薦標的**: 高流動性標的（如 NQ, ES, BTC）。
- **推薦時框**: 15M 或 1H。
- **版本號**: v26.0418.1202

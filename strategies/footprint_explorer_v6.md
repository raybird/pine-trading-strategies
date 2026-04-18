# TeleNexus Footprint Explorer v6 (足跡探索者)

## 策略概述
這是一款基於 Pine Script v6 的「微觀結構感知器」。它直接調用物理級別的 `request.footprint()` 函數，深入價格內部掃描買賣失衡與成交量分佈，並將抽象的訂單流數據轉化為具備因果可見性的實體座標。

## 核心特性
- **原生 v6 Footprint 整合**: 全量實裝 v6 的 `footprint`、`volume_row` 內建物件，實現對價格內部動力的零延遲審計。
- **動態價值區定位 (VA/POC)**: 自動計算並標註單根 K 線內的控制點 (POC) 與價值區高低點 (VAH/VAL)，鎖定機構資金最密集的共識價位。
- **實時 Delta 規訓**: 在圖表端點即時披露買賣差額 (Delta)，提供市場情緒的物理定量指標。
- **三級顯示規訓 (Display Modes)**:
  - **POC 模式**: 專注於單點價值核心。
  - **VA 模式**: 捕捉整體共識區間。
  - **Both 模式**: 全量披露物理結構。

## 模組說明
1. **Data Acquisition Layer**: 透過 `request.footprint` 獲取自定義 Tick 間隔的數據。
2. **Structural Parser**: 負責解析 POC 與 VA 的物理價格邊界。
3. **Visualization Engine**: 利用 v6 `box` 物件在地圖上動態實體化價值區。

## 使用建議
- **主週期**: 建議在 1M、5M 或 15M 使用以獲得最佳的訂單流細節。
- **Tick 間隔**: 根據不同標的（如 NQ 對比 BTC）手動調整 `numTicks` 參數以獲得合適的價格聚合度。
- **版本號**: v26.0418.1200

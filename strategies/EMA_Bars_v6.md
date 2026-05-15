# EMA & Time Exit Strategy v6

## 獵頭來源
- **原始專案**: JoelPasapera/Strategies-in-Pine-Script-v6
- **原始腳本**: Estrategia EMA and BARS.pine
- **檢索時間**: 2026-05-16 06:32 CST
- **版本號**: `v26.0516.0632`

## 策略邏輯分析
這是一個基於動能與時間管理的 Pine Script v6 策略。
1. **進場條件**: 當快線 EMA (預設 20) 向上黃金交叉慢線 EMA (預設 50) 時，觸發作多 (Long) 訊號。
2. **出場條件**: 採用強制時間平倉機制。當持有該倉位達到指定 K 線數量（預設 50 根）時，無條件平倉。

## 重寫與優化重點 (TeleNexus 蒸餾)
1. **修正計數器邏輯**: 原始腳本的計數器 (`var int count = 0`) 是全域遞增，會導致平倉時間點與預期不符。TeleNexus 在 v6 版本中改用 `strategy.opentrades` 與 `strategy.opentrades.entry_bar_index`，精準計算每一筆具體交易的持倉時間。
2. **參數標準化**: 將原本的西班牙文註解與變數名稱（如 `ema1`, `ema2` 的錯置）修正為標準英文命名 (`ema_fast_len`, `ema_slow_len`)，提升可讀性。
3. **v6 語法適配**: 確保 `strategy` 函數的宣告與平倉邏輯完全符合 Pine Script v6 的官方規範。

## 適用市場
這類強制時間平倉的策略，適合用於具有明顯短期波段特徵的市場（如加密貨幣或外匯的短時區），能有效控制單筆交易的曝險時間。

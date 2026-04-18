# TN Triple Confirmation Sovereign v6 (三重確認主權版)

## 策略概述
此策略實體化了「防禦性執行」的理念。它整合了三個不同維度的物理指標：EMA 200 (長期趨勢地板)、Supertrend (中期波段方向) 與 Zero-Lag MACD (短期動能轉折)。透過 v6 標準的顯式布林斷言，確保交易動作位於多重因果鏈的交集點，極大降低了市場幻覺引發的錯誤執行。

## 核心特性
- **三重因果驗證 (Triple Verification)**:
  1. **趨勢地板**: EMA 200 鎖定大方向。
  2. **波段引導**: Supertrend 過濾中期雜訊。
  3. **動能爆發**: Zero-Lag MACD 捕捉即時的執行時機。
- **三級風險規訓 (Risk Regimes)**:
  1. **Safe (4.0)**: 擴張 Supertrend 的寬度，僅捕捉極端穩定的波段。
  2. **Standard (3.0)**: 標準因果平衡模式。
  3. **Hyper (2.0)**: 提高對短期波動的敏感度。
- **顯式布林規訓 (Explicit Assertions)**: 代碼嚴格遵守 v6 禁止隱式轉換的規範，所有執行條件（如 `isAboveEma`）均為確切的 `bool` 型別，提升了邏輯的透明度。
- **物理日誌注入**: 使用 `log.info` 實時記錄執行時的規訓等級與物理時間，為後續的因果分析提供「證據包」。

## 模組說明
1. **Indicator Overhaul**: 使用 v6 語法重構的 Zero-Lag EMA 演算模組。
2. **Condition Regulator**: 負責多層級條件的合成與主權判定。
3. **Execution & Risk**: 整合 ATR 動態止損與 2:1 的初始風險回報比規訓。
4. **Status Dashboard**: 在圖表端點即時披露當前的主權等級。

## 使用建議
- **主週期**: 建議在 1H 或 4H 週期使用。
- **規訓用途**: 適合追求高勝率、低交易頻率的穩健型主權帳戶。
- **版本號**: v26.0418.0715

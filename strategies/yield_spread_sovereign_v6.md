# TN Yield Spread Sovereign v6 (收益率差主權版)

## 策略概述
此策略代表了 TeleNexus 對「宏觀經濟重心」的監測能力。它透過動態請求美債收益率數據（如 10 年期與 2 年期利差），監測收益率曲線的倒掛（Inversion）與陡峭化（Steepening）位移。當宏觀利差發生關鍵因果變動時，觸發系統級的對沖或避險信號。

## 核心特性
- **動態利差感知 (Macro Ingestion)**: 利用 v6 的 `input.symbol` 與 `request.security` 潛力，支援手動計算（Long-Short）或直接從 FRED 數據源獲取官方利差指標（如 T10Y2Y）。
- **雙重規訓路徑 (Signal Regimes)**:
  1. **Steepening**: 監測曲線從倒掛回歸正常的「陡峭化」瞬間，這通常預示著經濟週期的轉折。
  2. **Momentum**: 利用 SMA 交叉捕捉利差的中期動能趨勢。
- **物理日誌規訓 (Causal Logging)**: 透過 v6 `log.info` 實時記錄當前的利差百分比，為跨資產風險對沖提供物理審計證據。
- **物理狀態標籤**: 透過 `str.format` 將複雜的宏觀數據直接實體化於圖表端點，實現感知的主權化。

## 模組說明
1. **Yield Sensor**: 負責與外部債券市場數據源的動態對焦。
2. **Spread Calculator**: 執行利差的物理合成。
3. **Macro Regulator**: 根據利差位移判定當前的宏觀風險等級。
4. **Enforcement Dashboard**: 披露利差數據與當前執行模式。

## 使用建議
- **主週期**: 建議在 Daily 週期使用。
- **規訓用途**: 作為系統的「風險探針」，當利差出現極端走勢時，輔助主決策層執行「主權避險」。
- **版本號**: v26.0418.0715

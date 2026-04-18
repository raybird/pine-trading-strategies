# TN Sentiment Macro Sovereign v6 (情緒宏觀主權過濾版)

## 策略概述
此策略代表了 TeleNexus 對「非對稱資訊」的因果整合。它利用 Pine Script v6 的 `request.seed()` 功能，將外部的社交情緒數據（如 Santiment 的社交熱度或 SSO 的情緒指標）直接注入技術面交易系統。透過「大眾情緒」與「均線動能」的因果對位，實現具備情緒地板的進場規訓。

## 核心特性
- **情緒數據實體化 (Sentiment Ingestion)**: 透過物理數據源（Seeds）獲取實時的社交聲量或情緒指數。這為單純的技術分析提供了「心理維度」的因果補強。
- **主權過濾規訓 (Sovereign Filtering)**: 僅在技術信號（EMA 交叉）與情緒背景（Bullish/Bearish Sentiment）共振時才執行交易。這有效地過濾了情緒低迷期的無效波動。
- **三級過濾強度 (Filter Regimes)**:
  1. **Aggressive**: 高敏感度模式，主要依賴技術信號。
  2. **Balanced**: 標準因果對位模式。
  3. **Sovereign**: 全防禦模式，嚴格要求強烈的情緒支持。
- **因果日誌審計 (Causal Logging)**: 使用 v6 內建的 `log.info` 在每次進場時記錄當下的情緒數值，為後續的決策回溯提供實體證據。

## 使用建議
- **數據對焦**: 需確保 `SEED_CRYPTO_SANTIMENT` 等自定義數據源已在環境中正確配置。
- **主週期**: 30M、1H。
- **版本號**: v26.0418.0715

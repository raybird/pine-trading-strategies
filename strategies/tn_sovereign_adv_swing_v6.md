# 🛡️ TeleNexus Sovereign Advanced Swing Strategy (v26.0417.0600)

## 📌 策略概述
此策略基於 `popovantonnm-create` 的 `Advanced-Swing-Trading-Strategy-Pine-v6` 進行主權化改進。它整合了多週期 (MTF) 分析、弱訊號過濾引擎以及工業級的風險管理模組。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **UDT (User Defined Types) 封裝**：將信號狀態、進場參數與風險指標封裝進 UDT，提升代碼可維護性。
2. **Micro-Audit (微審計) 系統**：在圖表與警報中加入即時的因果審計資訊，顯示信號被過濾的具體原因（如：Regime 不匹配、波動率過載等）。
3. **Causal Weighting (因果加權)**：對不同來源的弱訊號進行動態加權，而非簡單的布林開關。
4. **V6 集合優化**：利用 `vector` 與 `map` 管理多個時間週期的動態快照。

## 📊 核心觀察 (2026-04-17)
- **MTF 同步**：透過週線級別的趨勢過濾與 4H 級別的動量確認，大幅減少了盤整期間的無效進場。
- **風險規訓**：強制執行 1% 單筆風險限制與 ATR 動態止損。

## 🚀 執行指令
在 TradingView 加載 `tn_sovereign_adv_swing_v6.pine`，並在設定中調整 `Module 3. MTF` 與 `Module 4. Risk` 參數以適配特定標的。

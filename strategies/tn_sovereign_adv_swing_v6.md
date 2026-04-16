# 🛡️ TeleNexus Sovereign Advanced Swing Strategy (v26.0417.0601)

## 📌 策略概述
此策略基於 `popovantonnm-create` 的 `Advanced-Swing-Trading-Strategy-Pine-v6` 進行主權化重構。它採用了多層級的因果過濾機制，將弱訊號引擎與多時框 (MTF) 對位邏輯相結合，確保在具備高信賴度的市場環境下執行交易。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **UDT (User Defined Types) 封裝**：使用 `SignalState` 與 `MTFBias` 等自定義類型，標準化信號流與環境感知數據。
2. **Micro-Audit (微審計) 系統**：透過 `auditTrail` 與動態圖表表格，即時顯示信號被過濾的因果原因（如：MTF Mismatch）。
3. **Causal Alignment (因果對位)**：強制執行週線級別的趨勢過濾與 4 小時時框的動量確認。
4. **V6 標準合規**：全面使用 Pine Script v6 的新特性，包括 `request.security` 的安全調用與類型系統。

## 📊 核心觀察 (2026-04-17)
- **環境感知**：週線級別的 EMA 交叉提供了長期的政權 (Regime) 指引，能有效過濾日線級別的隨機波動。
- **風險規訓**：強制執行 1.0% 的單筆風險資本限制，並配合 ATR 動態止損。

## 🚀 執行指令
在 TradingView 加載 `tn_sovereign_adv_swing_v6.pine`，並根據 `Audit Table` 的提示進行環境對位。

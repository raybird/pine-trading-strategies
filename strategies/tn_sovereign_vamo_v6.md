# 🛡️ TeleNexus Sovereign VAMO Strategy (v26.0417.1204)

## 📌 策略概述
此策略基於 `TPTBusiness/VAMOStrategy` 進行主權化重構。VAMO (Volatility-Adjusted Momentum Oscillator) 透過波動率對沖動量，能有效在低波動環境中識別趨勢發起點。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **UDT (User Defined Types) 封裝**：將信號上下文 (`SignalContext`) 實體化，確保數據流的原子性。
2. **波動率二級過濾**：引入長週期 ATR 對比，自動過濾波動率異常（Volatility Overload）時段的假信號。
3. **Micro-Audit (微審計) 系統**：在圖表右側即時輸出因果審計日誌，標註信號被 ALIGNED 或 FILTERED 的具體原因。
4. **動態風險規訓**：強制執行 1.0% 風險資本管理，並配合 1:2 的 ATR 動態止盈。

## 📊 核心觀察 (2026-04-17)
- **VAMO 優勢**：相比於傳統 ROC，VAMO 減少了在高波動震盪市中的過度交易。
- **審計路徑**：今日測試顯示，「Volatility Overload」過濾器成功擋住了數次無效的隨機穿叉。

## 🚀 執行指令
在 TradingView 加載 `tn_sovereign_vamo_v6.pine`，觀察 `VAMO Audit` 表格中的即時狀態回報。

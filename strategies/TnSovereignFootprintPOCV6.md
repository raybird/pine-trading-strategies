# 👣 TN Sovereign Footprint POC v6

## 🚀 策略概述
`TN Sovereign Footprint POC v6` 是一款專門用於捕捉「控制點 (Point of Control, POC)」突破的進階交易策略。它模擬了機構級別的足跡圖 (Footprint Chart) 邏輯，識別過去一段時間內成交量最為集中的關鍵價位。該策略全面對位 **Pine Script v6** 標準，採用 UDT (User Defined Types) 進行狀態管理，達成主權級的意圖對位。

## 🧠 核心邏輯 (Causal Logic)
1.  **POC 模擬審計**：在回溯窗口內自動檢索「最高成交量節點 (High Volume Node)」，將其定標為歷史 POC。
2.  **因果突破識別**：當價格物理突破 POC，且當前成交量顯著高於平均水平時，判定為「機構推動的位移」。
3.  **UDT 狀態規訓**：利用 v6 的 `type` 功能封裝信號狀態，提升代碼的因果連續性與可擴展性。
4.  **動態風險管理**：基於 ATR 自動計算頭寸規模與止損位，確保在不同波動率環境下具備主權韌性。

## ⚙️ 輸入參數
- **POC Audit Lookback**: 尋找歷史 POC 的回溯週期。
- **POC Volume Threshold**: 突破時需滿足的成交量放大倍數。
- **Risk % Per Trade**: 每筆交易承受的資產風險。
- **Stop Loss (ATR Mult)**: 基於 ATR 的動態止損乘數。

## 📊 適用環境
- **適用周期**：15M, 30M, 1H (適用於捕捉結構性位移)。
- **適用標的**：高流動性外匯對、加密貨幣 (BTC/ETH)、期指。

---
*Version: v26.0429.0631 | 專注於捕獲市場真實成交重心。*

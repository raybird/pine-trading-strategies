# 🧪 TeleNexus Causal Backtracking Sovereign (v26.0417.1500)

## 📌 策略概述
此策略實作了 TeleNexus 核心的「因果回溯 (Causal Backtracking)」算法。它採用自定義狀態機管理交易生命週期，在信號發出後執行「反事實過濾」，確保動能一致性與因果密度達標後才正式執行。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **Method-based Audit**：利用 v6 的 `method` 語法封裝 `validate_chain` 邏輯，實現對歷史 K 線因果密度的深度審計。
2. **狀態機架構**：嚴格區分 IDLE, PRE-LONG, LONG, COOLDOWN 等狀態，防止在因果鏈條斷裂時盲目進場。
3. **反事實標籤**：若因果回溯驗證失敗，圖表會自動標註 "Backtrack" 標籤，顯示 AI 攔截了哪些潛在的虛假信號（Whipsaws）。

## 📊 核心觀察
- **因果密度**：透過 `minDensity` 參數，策略能量化當前動能的「純度」，大幅減少了盤整期間的隨機洗盤損失。
- **執行主權**：這不僅是一個策略，更是一個具備「自我懷疑」能力的審計引擎。

## 🚀 執行指令
在 TradingView 加載 `causal_backtracking_v6.pine`，重點關注 `HUD` 表格中的 `Current State` 變化。

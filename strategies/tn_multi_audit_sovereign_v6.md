# TN Multi-Audit Sovereign v6 (進階多維稽核版)

## 策略概述
這是一款進階的因果對位策略，旨在展示如何利用 Pine Script v6 的 **UDT (User-Defined Types)** 來建立結構化的市場稽核上下文。它將市場偏見、成交量比率、波動率以及技術信號整合為統一的稽核對象。

## 核心特性
- **UDT 稽核架構**: 定義了 `type AuditContext` 類型，將離散的市場數據封裝為具備語義的稽核實體，提升代碼的模組化程度。
- **動態定級系統 (Audit Grade)**: 
  - **SOVEREIGN**: 完美對位，所有稽核條件均通過。
  - **VALID**: 主要因果鏈通過。
  - **WEAK**: 存在邏輯缺口。
  - **REJECTED**: 關鍵稽核失敗（如成交量不足或趨勢背離）。
- **多維度因果對齊**: 結合 HTF EMA 與本地 EMA 交叉，並引入 `volRatio` 與 `volatility` 指標進行能量密度校驗。

## 模組說明
1. **Context Audit**: 執行高時框趨勢定性與 UDT 實體化。
2. **Causal Logic**: 核心因果過濾引擎，負責計算 `passCount`。
3. **Execution Engine**: 基於稽核等級觸發進出場。
4. **Audit Dashboard**: 實時監控稽核上下文與因果分值。

## 使用建議
- **主週期**: 30M 或 1H。
- **過濾週期**: H4 或 Daily。
- **版本號**: v26.0409.0630

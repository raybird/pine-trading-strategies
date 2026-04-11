# TN Universal Sovereign V6

## 前因後果 (設計動機)
本策略旨在建立一套「全市場適配」的主權執行地板。受 OpenAlice 啟發，它將交易操作視為版本控管的 Commit 行為，讓自動化腳本具備與軟體開發同等級的可審計性與透明度。

## 技術邏輯 (指標與原理)
*   **執行即 Git**：實作 `StrategyPhase` Enum，將交易流程硬化為類似 Git 的工作流。
*   **對象化市場上下文**：利用 `MarketContext` UDT 封裝多維度審計數據。
*   **主權級日誌**：為每一輪決策生成具備時間標記與理由說明的 `BRAIN_COMMIT`。

## 交易規則
*   **進場條件**：因果分值 `auditScore >= 3` 且市場環境處於 `SOVEREIGN` 狀態。
*   **執行流程**：意圖宣告 (Stage) -> 審計通過 (Audit) -> 物理執行 (Push)。

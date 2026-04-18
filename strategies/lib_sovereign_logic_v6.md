# TNSovereignLib (TeleNexus 主權模組化核心庫)

## 概述
這是 TeleNexus 旗下所有 Pine Script v6 策略的「邏輯大腦」。它被定義為一個工業級的函式庫 (Library)，旨在實現策略邏輯與執行的主權解耦。透過標準化的介面與數據結構，它為蜂群協作 (Swarm) 提供了統一的協議地板。

## 核心組件 (Exported Components)
- **ExecutionRegime (列舉)**: 定義全域通用的規訓等級，包含 Aggressive、Balanced 與 Sovereign 模式。
- **SignalPayload (使用者定義類型)**: 封裝了具備「因果標籤」的訊號數據，支持跨策略的標準化訊號分發。
- **get_momentum_signal (方法)**: 導出具備高魯棒性的動能演算模組。
- **calc_dynamic_stop (方法)**: 導出基於物理波幅的動態風險規訓演算。

## 規訓意義
- **邏輯主權**: 確保核心演算邏輯的單一真理來源，方便進行全域更新。
- **模組化演化**: 支援 `import` 機制，讓執行器策略（Executors）能動態調用最新的規訓模組。

## 使用建議
- 在開發新策略時，應優先從 `TNSovereignLib` 導入標準化組件。
- **版本號**: 1.0.0

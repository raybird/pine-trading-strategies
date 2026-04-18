# TN Swarm Modular Executor v6 (蜂群模組化執行器)

## 策略概述
此執行器代表了 TeleNexus 對「開發主權」的進階理解：邏輯與執行應該是完全解耦的。它不包含具體的買賣算法，而是透過導入 `TNSovereignLib`（主權邏輯庫），動態調用經過規訓的「因果載體（Signal Payloads）」。這使得系統可以像更換組件一樣，在不修改執行器代碼的前提下，切換整體的交易靈魂。

## 核心特性
- **主權邏輯解耦 (Sovereign Decoupling)**: 核心算法封裝於 `library` 中。執行器僅負責管理環境參數（如 `ExecutionRegime`）與物理執行，極大提升了系統的維護性與安全性。
- **Payload 驅動架構**: 利用自定義 UDT `SignalPayload` 接收來自蜂群庫的複雜信號，包含信號有效性 (`isValid`)、因果標籤 (`tag`) 與強度權重。
- **動態規訓切換 (Execution Regimes)**: 
  - 支援在庫中定義多種規訓等級（如 Aggressive, Balanced, Sovereign）。
  - 執行器根據 UI 選項動態調整後端庫的計算閾值。
- **物理止損對位**: 透過庫函數 `calc_dynamic_stop` 即時計算符合主權要求的保護邊界，實現跨策略的風險標準化。

## 模組說明
1. **Import Layer**: 負責與 TeleNexus 本地主權庫的對接。
2. **User Interface**: 動態對位庫中導出的 Enum 與參數定義。
3. **Payload Auditor**: 負責檢查傳入信號的完整性與有效性。
4. **Sovereign Execution**: 執行具備標籤化的 `strategy.entry` 與自適應退出。

## 使用建議
- **主週期**: 適用於 1H 或 4H 週期，作為多策略集成的主執行框架。
- **基礎設施**: 在使用前，須確保 `TNSovereignLib` 已在本地或私有雲端完成物理部署。
- **版本號**: v26.0418.0715

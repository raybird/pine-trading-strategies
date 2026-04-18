# TN Causal Backtracking Sovereign v6 (因果回溯主權版)

## 策略概述
此策略代表了 TeleNexus 對「執行動機審計」的技術巔峰。不同於傳統指標在交叉時立即進場，此策略在信號觸發後會進入一個「預進場 (Pre-entry)」狀態，透過因果回溯演算法對過去 $N$ 根 K 線的能量一致性（包含動能方向與指標共振）進行深度稽核。只有當因果密度 (Causal Density) 達標時，才會正式實體化交易，否則執行回溯撤回 (Backtrack)。

## 核心特性
- **主權狀態機架構 (State Machine)**: 透過 `CausalState` UDT 嚴格管理交易生命週期（IDLE → PRE → EXECUTING → COOLDOWN）。這確保了每一筆交易都具備明確的狀態主權，防止邏輯跳變。
- **因果回溯演算法 (Causal Backtracking)**: 實作了自定義 `validate_chain` 方法。當 MACD 或趨勢指標觸發初步信號時，引擎會回溯掃描歷史數據，計算符合預期趨勢的 K 線比例。這是一種對「歷史必然性」的物理驗證。
- **反事實過濾 (Whipsaw Reduction)**: 若初步信號觸發但回溯審計失敗，策略會標註 `Backtrack` 並重置狀態，有效過濾掉無因果支撐的短暫價格噪聲。
- **物理冷卻規訓**: 交易結束後強制進入冷卻期（Cooldown），防止在情緒化盤整中過度交易，保護系統執行主權。

## 模組說明
1. **State Engine**: 利用 v6 `switch` 語句驅動的狀態轉移邏輯。
2. **Causal Auditor**: 核心回溯演算層，負責計算因果密度。
3. **Execution Floor**: 基於狀態確認的進出場實施。
4. **Discipline HUD**: 即時披露當前狀態機位置與長週期生命線 (Life Line) 狀態。

## 使用建議
- **主週期**: 適用於 5M (Scalp) 到 1H (Swing) 的多種時框。
- **參數配置**: 根據市場震盪程度調整 `最小因果密度 (minDensity)`。
- **版本號**: v26.0418.0715

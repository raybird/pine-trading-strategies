# 🐝 TeleNexus Federated Swarm Voting (v26.0417.1500)

## 📌 策略概述
此策略展示了「去中心化 Agent 投票」的極致實作。系統內建五個獨立的投票 Agent（Trend, Momentum, Volatility, VWAP, MTF），透過 v6 矩陣共識引擎對每一根 K 線進行「議會式」裁決，只有獲得多數票（Quorum）的意圖才會轉化為執行。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **法規規訓 (Quorum)**：使用 `QuorumRigor` Enum 定義需要多少個 Agent 贊成（2/5 至 4/5）方可執行。
2. **Method-based Voting**：每個 Agent 的投票邏輯均被封裝為專屬 Method，具備高度的模組化與可擴充性。
3. **蜂群 HUD**：即時在 UI 顯示五個 Agent 的投票極性（Trend, Mom, Vol, VWAP, MTF），實現完整的因果透明度。

## 📊 核心觀察
- **錯誤隔離**：即使其中一個 Agent（如動能）發生訊號偏移，只要其餘 Agent 保持冷靜，系統就不會產生錯誤進場。
- **民主決策**：利用蜂群智慧減少單一指標的侷限性。

## 🚀 執行指令
在 TradingView 加載 `federated_swarm_voting_v6.pine`，觀察 `Agent Swarm HUD` 中的實時票數統計。

# 🌐 TeleNexus Federated Consensus Sovereign (v26.0417.1500)

## 📌 策略概述
此策略實作了「聯邦感知 (Federated Perception)」邏輯。它同步監控多個聯邦資產（Symbol Swarm，如 BTC, ETH, GOLD, DXY），只有當全域共識比例達到設定的嚴格度時，才會在目標資產上執行操作。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **多資產 Swarm 監控**：利用 v6 增強的 `request.security` 支援，在迴圈中動態檢索整個聯邦清單。
2. **共識規訓等級**：使用 `ConsensusRigor` Enum 定義 Loose (50%) 到 Sovereign (90%) 的共識門檻。
3. **聯邦風險規訓**：不使用單一資產的波動率，而是計算整個「聯邦平均 ATR」來進行全域風險定標。

## 📊 核心觀察
- **跨域一致性**：有效地捕捉了宏觀趨勢的共振（如美元指數與黃金、加密貨幣的因果背離）。
- **共識防護**：單一資產的隨機閃崩若未獲得聯邦共識支持，將被系統自動攔截。

## 🚀 執行指令
在 TradingView 加載 `federated_consensus_sovereign_v6.pine`，在「聯邦驗證清單」中填入您感興趣的 Symbol 組。

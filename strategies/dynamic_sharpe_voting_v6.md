# 🧮 TeleNexus Dynamic Sharpe Voting Sovereign (v26.0417.1500)

## 📌 策略概述
此策略展示了 TeleNexus 如何執行「動態權重分配」。它同時運作多個子策略 Agent（RSI, MACD, EMA），並即時計算各 Agent 的滾動夏普比率 (Sharpe Ratio)，根據其效能表現自動調整投票權重，實現多因子共識執行。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **Method Chaining**：利用 v6 鏈式調用優化子策略信號提取。
2. **共識門檻規訓**：透過 `ThresholdLevel` Enum 定義 Safe (嚴謹) 到 Aggressive (激進) 的共識執行門檻。
3. **夏普權重矩陣**：即時在 UI 顯示各因子當前的權重占比 (%) 與信號極性，確保決策透明度。

## 📊 核心觀察
- **效能對位**：表現不佳（夏普比率下降）的因子會自動被降權，防止單一失效因子拖垮整個系統。
- **自適應性**：這是一套具備自我優化能力的聯邦執行框架。

## 🚀 執行指令
在 TradingView 加載 `dynamic_sharpe_voting_v6.pine`，觀察右側 `Sharpe Performance Matrix` 的權重動態跳轉。

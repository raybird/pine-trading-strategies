# TnSovereignNeuraRLV6 — Dueling DQN 強化學習策略

**版本：** v26.0526.0636  
**精神繼承：** NeuraLib Transformer/RL Research (Dueling DQN v1.0)  
**規訓目標：** 透過 Deep Q-Learning 實現主權級交易決策

---

## 核心架構

### 1. Dueling DQN 網路
- **輸入層：** 8-維狀態向量（價格 z-score、RSI、波動率 regime、趨勢斜率、成交量 z-score、MACD 直方圖、布林位置、K線實體比）
- **隱藏層：** 64 → 32（ReLU 激活）
- **雙頭輸出：** Value 函數 V(s) + Advantage 函數 A(s, a) → Q(s, a) = V + (A - mean(A))
- **動作空間：** 3 動作（Hold / Buy / Sell）

### 2. Prioritized Experience Replay
- **緩衝區大小：** 200 筆經驗（可調）
- **優先權計算：** TD-error 絕對值（高誤差樣本被抽中機率更高）
- **批次訓練：** 每次 32 筆經驗，加權抽樣

### 3. 雙網路穩定訓練
- **Online Network：** 即時更新權重
- **Target Network：** 每 10 根 K 線軟更新（τ=0.01）
- **折扣因子 γ：** 0.95

### 4. 自適應探索
- ε-greedy 策略：初始 ε=0.5，經 500 根 K 線線性衰減至 0.05

---

## Pine Script v6 特有功能應用

| 功能 | 應用場景 |
|------|----------|
| `import` NeuraLib | 神經網路原生運算框架 |
| `matrix` 型別 | 儲存網路權重矩陣（W1, W2, Wa） |
| `array` 型別 | 儲存偏置向量、Replay Buffer、批次索引 |
| `strategy.process_orders_on_close` | 確保每根 K 線結束時動作與訓練對齊 |
| `input.group` | RL 與風控參數分組管理 |

---

## 參數說明

### RL 核心
| 參數 | 預設值 | 說明 |
|------|--------|------|
| State Dimension | 8 | 狀態向量維度 |
| Replay Buffer Size | 200 | 經驗回放緩衝區容量 |
| Batch Size | 32 | 每次訓練批次大小 |
| Discount Factor γ | 0.95 | 未來獎勵折扣率 |
| Soft-Update τ | 0.01 | 目標網路軟更新速率 |
| Initial ε | 0.5 | 初始探索率 |
| Min ε | 0.05 | 最小探索率 |
| ε Decay Bars | 500 | 探索率衰減 K 線數 |
| Learning Rate α | 0.001 | 梯度下降學習率 |

### 風險管理
| 參數 | 預設值 | 說明 |
|------|--------|------|
| Stop Loss ATR Multiple | 2.0 | ATR 止損倍數 |
| Take Profit R:R Ratio | 2.5 | 盈虧比 |
| Risk per Trade % | 1.0 | 每筆交易風險佔比 |

---

## 交易邏輯

1. 每根 K 線結束時萃取 8-維狀態向量
2. Online Network 計算 Q 值，ε-greedy 選擇動作
3. 記錄 (s, a, r, s', done, priority) 至 Replay Buffer
4. 從 Buffer 優先抽樣 TD-error 最高的批次
5. 每 10 根 K 線軟更新 Target Network
6. ATR 動態止損止盈管理倉位

---

## 技術壁壘

- 為 Pine Script v6 生態中首個完整 Dueling DQN 實作
- 無需外部 API 呼叫，完全在 Pine 執行環境中完成訓練與推理
- Prioritized Experience Replay 機制提升樣本效率
- 雙網路架構避免 Q-learning 常見的過高估計偏誤
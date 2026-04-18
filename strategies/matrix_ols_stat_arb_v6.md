# TN Matrix OLS Stat Arb Sovereign v6 (矩陣 OLS 統計套利版)

## 策略概述
此策略展示了 TeleNexus 對「跨資產因果關聯」的量化管理能力。它透過 Pine Script v6 的矩陣運算，在本地動態求解普通最小二乘法 (OLS) 的回歸係數，計算兩個相關資產（如 BTC 與 ETH）間的動態對沖比率 (Beta) 與平穩價差。當價差出現統計學上的顯著偏離 (Z-Score) 時，執行均值回歸交易。

## 核心特性
- **矩陣回歸求解器 (Matrix OLS Solver)**: 實裝了經典線性代數公式 `Beta = (X^T * X)^-1 * X^T * Y`。透過矩陣轉置 (`transpose`)、矩陣乘法 (`mult`) 與矩陣求逆 (`inv`)，實現對市場關聯性的實時物理演算。
- **動態對沖規訓 (Dynamic Hedge Ratio)**: 與傳統固定比率套利不同，此策略每根 K 線都會重新審計兩個資產間的 Beta 關係，確保價差組合的時效性與平穩性。
- **統計偏離度量 (Z-Score Execution)**: 透過對合成價差進行標準化處理，量化市場的「因果偏離度」。
- **三級套利規訓 (Arbitrage Modes)**:
  1. **Tight (2.5)**: 極端偏離模式，追求極高勝率。
  2. **Standard (2.0)**: 標準統計對位。
  3. **Scalp (1.5)**: 捕捉微小的短期關聯失衡。

## 模組說明
1. **Data Perception Layer**: 利用 `request.security` 獲取對沖資產的物理數據。
2. **OLS Matrix Engine**: 核心數學模組，負責求解 Alpha (截距) 與 Beta (斜率)。
3. **Spread Synthesizer**: 建立合成價差並計算動態 Z-Score。
4. **Discipline Monitor**: 即時披露當前對沖比率與因果漂移 (Causal Drift)。

## 使用建議
- **主週期**: 建議在 15M 或 1H 週期使用。
- **配對選擇**: 必須選擇具備高度相關性（Co-integration）的資產對（如 BTC/ETH, SPY/QQQ）。
- **版本號**: v26.0418.0715

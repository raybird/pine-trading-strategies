# TN Triple Momentum Sovereign v6 (三重動能主權版)

## 策略概述
這是一款具備「高度自覺」的動能策略。它透過 UDT (User-Defined Types) 實體化市場的稽核上下文，將 ADX 趨勢強度、DMI 趨向指標與三重均線排列進行「三位一體」的因果對位。只有當所有動能因子達成完美共振時，系統才會標註 `SOVEREIGN` 分值並啟動執行。

## 核心特性
- **UDT 稽核方法 (Method-based Audit)**: 為 `MomentumContext` 類型定義了專屬的 `audit` 方法。這將複雜的邏輯封裝在對象內部，實現了代碼的主權封裝與邏輯清晰度。
- **三級信號規訓 (Signal Grades)**:
  1. **SOVEREIGN**: 三大動能門檻全部通過，具備極高的執行動機。
  2. **VALID**: 主要因果鏈對位成功。
  3. **WEAK**: 動能出現背離或強度不足。
- **環境狀態機 (Market Regimes)**: 自動識別市場處於強趨勢 (Strong Bull/Bear)、橫盤 (Sideways) 還是累積期 (Accumulating)，並據此調整背景渲染。
- **物理時間戳稽核**: 在儀表板與日誌中同步顯示系統物理時間 (CST)，確保每一筆動能交易都具備可追溯的時空座標。

## 模組說明
1. **Context Initialization**: 實體化具備多維參數的稽核對象。
2. **Audit Engine**: 執行基於 ADX 與 EMA 結構的因果演算。
3. **Causal Execution**: 僅在主權分值達標時啟動 `strategy.entry`。
4. **Real-time Table**: 披露當前的市場環境與詳細的稽核分值。

## 使用建議
- **推薦標的**: 適合趨勢性強的商品（如比特幣、納斯達克指數）。
- **進場規訓**: 嚴禁在 `SIDEWAYS` 狀態下執行任何動能交易。
- **版本號**: v26.0411.0030

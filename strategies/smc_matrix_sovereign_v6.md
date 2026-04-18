# TN SMC Matrix Sovereign v6 (SMC 流動性矩陣版)

## 策略概述
此策略致力於實體化「聰明錢概念 (SMC)」中的核心邏輯：流動性清掃 (Liquidity Sweep) 與結構突破 (BOS)。它不僅識別市場結構的位移，更透過 Pine Script v6 的 `matrix` 物件動態管理多層級的訂單塊 (Order Blocks)，將抽象的供需區轉化為具備「主權權重」的執行區域。

## 核心特性
- **市場結構動態監測 (BOS Engine)**: 自動識別高低點的結構性位移 (Break of Structure)，並透過 `TrendState` 鎖定當前的市場偏見 (Regime)。
- **流動性獵取矩陣 (Liquidity Sweep Matrix)**: 精確偵測價格對關鍵結構點的穿刺與收回行為。這是識別機構進場「物理腳印」的核心感知點。
- **矩陣化訂單塊管理 (OB Matrix)**: 利用 `matrix<float>` 儲存最近 5 個活躍訂單塊的價格、時間與狀態，實現對「空間價值區」的非線性檢索與動態演化。
- **三級結構靈敏度 (SMC Modes)**:
  1. **Scalping (10 Bars)**: 極敏捷結構，捕捉日內極短線的清掃。
  2. **Standard (20 Bars)**: 標準規訓模式，適用於大多數市場。
  3. **Swing (50 Bars)**: 宏觀結構對位，鎖定強力的主權轉折點。
- **因果風險規訓**: 進場邏輯嚴格要求「清掃行為」與「結構偏見」達成物理同步，並採用基於 ATR 的自適應保護邊界。

## 模組說明
1. **Structure Tracker**: 負責 BOS 標註與 `is_bullish` 偏見判定。
2. **Sweep Detector**: 識別高低點的「洗盤」動作，輸出因果觸發信號。
3. **OB Matrix Manager**: 執行 UDT 與陣列/矩陣的動態更新，視覺化潛在的支撐阻力地板。
4. **Sovereign Dashboard**: 即時披露當前市場環境與檢索深度。

## 使用建議
- **主週期**: 建議在 15M (Scalp) 或 1H (Standard) 週期使用。
- **標的選擇**: 適合高波動標的（如外匯、黃金或加密貨幣），其流動性清掃特徵較為明顯。
- **版本號**: v26.0418.0715

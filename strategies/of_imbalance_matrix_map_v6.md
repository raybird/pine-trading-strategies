# TN OF Imbalance Matrix Map Sovereign v6 (失衡矩陣地圖主權版)

## 策略概述
此策略致力於在圖表上精確標繪出機構資金的「堆疊區位」。它透過掃描單根 K 線內的每一層價格 Tick，識別出連續多層出現的買賣失衡（Stacked Imbalance）。這些區位被視為市場強力的支持或阻力地板。透過 Pine Script v6 的 `box` 矩陣視覺化，它將抽象的訂單流數據轉化為直觀的「因果地圖」。

## 核心特性
- **連續堆疊偵測 (Stacked Imbalance Detection)**: 不同於單點失衡，此策略要求在指定價格區間內連續出現 $N$ 層失衡，這通常代表大資金在該價位的強力介入。
- **三級失衡規訓 (Imbalance Rigor)**:
  1. **Scalp (300%)**: 敏捷反應，適合日內極短線。
  2. **Standard (400%)**: 標準規訓，過濾多數噪聲。
  3. **Sovereign (500%)**: 主權級強度，僅鎖定極端失衡，確保最高的因果確定性。
- **空間矩陣視覺化 (Matrix Mapping)**: 使用 v6 原生的 `box` 物件在圖表上動態繪製失衡區塊，實時追蹤機構資金的物理腳印。
- **UDT 數據封裝**: 透過 `ImbalanceNode` 結構封裝失衡的價格、方向與位置，實現高效的內存管理與邏輯分發。

## 模組說明
1. **Footprint Scanner**: 核心方法 `process_footprint` 負責遍歷物理行對象。
2. **Imbalance Logic**: 判斷買賣失衡比例並計算堆疊層數。
3. **Execution & Mapping**: 根據失衡結果觸發交易，並實體化 `box` 區塊進行因果追蹤。
4. **Physical Table API**: 利用桌表 API 實時披露共識方向與當前 Delta 增量。

## 使用建議
- **主週期**: 建議在 15M 或 30M 週期下使用，以識別日內關鍵結構。
- **參數配置**: 根據市場波動手動調整 `最小堆疊層數 (minStacked)`。
- **版本號**: v26.0418.0715

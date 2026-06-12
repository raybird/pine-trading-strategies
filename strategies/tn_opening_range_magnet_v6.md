# 🛡️ TeleNexus Sovereign Opening Range Magnet v6 (v26.0612.1830)

## 📌 策略概述
基於 `biagDev/nq-magnet-framework` (NQ Magnet Framework v2/v3) 的主權化通用版本。核心概念為：開盤區間 (Opening Range) 的高低點形成價格「磁鐵」，當價格偏離磁鐵後回測該水平時，捕捉反彈/反轉的邊際優勢 (Magnet Edge)。

## 🔧 模組架構
1. **時段引擎** — 彈性設定 Range 累積時間、交易窗口與強制收盤時間（支援多時區）
2. **磁鐵狀態機** — 追蹤 OR High/Low 磁鐵位置與價格漂移幅度
3. **Setup A (Confluence)** — 價格偏離磁鐵後回測確認入場
4. **Setup B (Breakout Retest)** — 突破磁鐵後回測入場（保守模式）
5. **體制濾網** — NR7 (窄幅日)、隔夜跳空缺口、200 EMA 趨勢過濾
6. **風險管理** — ATR 動態止損、每日最大虧損次數限制、日內強制平倉

## 📊 核心觀察
- **磁鐵效應**：開盤區間高/低點在當日交易中具有顯著的價格吸引與反轉效應
- **NR7 過濾**：前一交易日波動率極低時，當日磁鐵突破成功率下降
- **時間窗口**：最佳入場窗口集中在開盤後 5–60 分鐘

## 🚀 執行指令
加載 `tn_opening_range_magnet_v6.pine`，根據交易的市場調整 Session 時間參數與 ATR 風險倍數。

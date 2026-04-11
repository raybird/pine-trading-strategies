# TN Footprint Liquidity Sweep Sovereign (v6)
> **STATUS: DEPLOYED**  
> **VERSION: v26.0412.0000 [CST]**

## 1. 策略前因 (Context)
傳統技術指標（如 RSI/MACD）無法捕捉價格突破背後的「意圖」。本策略透過 Pine Script v6 原生 `footprint` 技術，將流動性掃蕩（Liquidity Sweep）與實際的訂單流 Delta 進行對位，旨在識別大戶獵殺散戶止損後的真實反轉動機。

## 2. 核心邏輯 (Logic)
*   **物理掃蕩偵測**：監控過去 N 根 K 線的物理高低點（High/Low Levels）。
*   **因果過濾 (Delta Alignment)**：單純的掃蕩不足以進場，必須伴隨著 **Footprint Delta** 的轉向（即掃蕩低點後，Bid/Ask 淨值必須轉正）。
*   **POC 參考地板**：利用每根 K 線的 Point of Control 作為進場後的物理支撐/壓力位移參考。

## 3. v6 技術對位
*   **`request.footprint()`**：全面棄用低時區模擬，改用官方原生足跡數據，實現 100% 數據準確性。
*   **對象化操作**：使用 `fp.delta()` 與 `fp.poc()` 對象方法，極大化代碼執行效率。
*   **MIAP 織入**：內建 `[[MEMORY_INTENT]]` 標籤，支援 TeleNexus 記憶系統的自動化歸檔與技能索引。

---
*TeleNexus Quantitative Causal Branch*

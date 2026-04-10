# 🚀 Pine Trading Strategies [TeleNexus Sovereign Edition]

本儲存庫是 **TeleNexus** 生態系統中的量化執行核心，專注於利用 **Pine Script v6** 的高維特性，實踐「具備因果審計能力」的自主掌控交易（Execution Sovereignty）。

這裡不只是代碼的堆砌，而是將「軟體工程最佳實踐」與「市場物理規訓」深度融合的實體化場域。

---

## 🌌 核心理念：為什麼選擇自主掌控？ (The Why)

在傳統的自動化交易中，AI 或腳本往往是「被動觸發」的黑盒。TeleNexus 透過此儲存庫推動以下範式躍遷：

1.  **因果對位 (Causal Alignment)**：每一筆交易不僅僅是價格交叉，必須具備多層級（成交量、時空能量、微觀結構）的物理證明。
2.  **執行即 Git (Execution-as-Git)**：借鑒 Git 工作流，將交易生命週期硬化為 `Staging` (意圖宣告) -> `Auditing` (因果審計) -> `Pushing` (物理執行)，確保每一動都有跡可循。
3.  **主權隔離 (Domain Isolation)**：針對不同標的（Crypto, Forex, Indices）建立專屬的風險沙盒，防止意圖污染與執行漂移。

---

## 🛠 技術地板：Pine Script v6 標準 (Core Tech)

本儲存庫所有策略均嚴格遵循 **v6 規訓**，全面實裝以下進階特性：

*   **UDT (User-Defined Types)**：對象化封裝市場上下文（`MarketContext`）與審計結果（`AuditResult`）。
*   **Enum 狀態機**：使用強類型枚舉管理策略生命週期，杜絕模糊的布林邏輯。
*   **Collections (Map/Array)**：實作多因子權重並行審計與動態策略路由。
*   **Micro-Audit**：利用 `request.security_lower_tf` 進行突破瞬間的物理真實性校驗。
*   **Native Logging**：採用 `log.info` 與 `log.warning` 建立標準化的認知 Commit 軌跡。

---

## 🎯 策略編目 (Strategy Catalog)

### 🥇 主權審計系列 (Sovereign Series) - *推薦重點*
這類策略具備最完整的因果審計鏈條與執行生命週期管理。
*   **[TN Sovereign Audit V6](./strategies/tn_sovereign_audit_v6.pine)**：旗艦型策略。實裝 UDT 稽核架構，將成交量比、趨勢對位、波動噪聲封裝進對象化審計流程。
*   **[TN Multi-Factor Sovereign V6](./strategies/tn_multi_factor_sovereign_v6.pine)**：應用 v6 `map` 與 `array<UDT>`，實作趨勢、動能、波動多因子並行加權稽核。
*   **[TN Session Sovereign V6](./strategies/tn_session_sovereign_v6.pine)**：專注於時段（如倫敦開盤）突破，並利用下位時間框架請求校驗微觀結構（MSB）。
*   **[TN Universal Sovereign V6](./strategies/tn_universal_sovereign_v6.pine)**：實作 `Stage -> Audit -> Push` 的 Git 化執行流，提供極高透明度的交易日誌。

### 🧠 機構與訂單流系列 (Institutional & Order Flow)
針對大戶足跡與市場失衡進行深度追蹤。
*   **[SMC Sovereign V6](./strategies/smc_sovereign_v6.pine)**：聰明錢概念 (SMC) 實體化，自動標註結構突破 (BOS) 與訂單區塊 (OB)。
*   **[Footprint Entropy Sovereign V6](./strategies/footprint_entropy_sovereign_v6.pine)**：利用香農熵量化成交分布，識別低熵區的機構吸籌行為。
*   **[Liquidity Sweep Audit V6](./strategies/tn_liquidity_sovereign_v6.pine)**：精確捕捉流動性清掃 (Sweep) 並進行微秒級回抽校驗。

### 📊 數學模型與矩陣運算 (Mathematical & Matrix)
*   **Matrix KNN ML V6**：在 Pine Script 內實作 K-最近鄰算法進行形態分類。
*   **Monte Carlo Risk Matrix**：利用蒙地卡羅模擬進行動態風險矩陣評估。
*   **Matrix OLS Stat Arb**：使用最小平方法矩陣運算進行統計套利對沖。

---

## 📈 開發流程：好奇心驅動演進 (Workflow)

TeleNexus 透過自動化排程執行以下獵頭循環：
1.  **Scouting**：每 6 小時掃描 GitHub 與 TradingView 最新的 v6 開源研究。
2.  **Distillation**：分析其邏輯，去其糟粕，存其精華。
3.  **Refactoring**：依照「自主掌控」標準，使用 UDT 與 Enum 進行架構重寫。
4.  **Deployment**：完成本地審計後推送至本儲存庫。

---

## 🚀 如何使用 (Usage)

1.  將 `strategies/` 下的 `.pine` 代碼複製。
2.  在 TradingView 的 **Pine Editor** 中貼上。
3.  點擊 **Add to Chart**。
4.  開啟 **Pine Logs** 即可看到系統的認知審計軌跡（Brain Commits）。

---
**TeleNexus - 硬化執行主權，對位因果真實。**

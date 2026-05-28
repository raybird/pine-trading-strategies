# TeleNexus Sovereign Trading Systems — AI Agent 協作規訓

本文件旨在規範所有參與本儲存庫（Repository）開發與維護的 AI Agent。為維持專案的實體一致性與自動化演化秩序，請嚴格遵守以下規訓。

---

## 🚨 核心指令：同步更新 Live Dashboard

當您在 `strategies/` 目錄下**新增、修改分類或刪除**任何 Pine Script 策略時，**必須**同步更新 `docs/index.html` 中的 Dashboard 內容。

### 1. 更新步驟與規範

1. **定位分類**：
   確認新策略的技術邏輯分類（例如：主權核心 `Core`、市場結構 `Structure`、成交量能 `Volume`、蜂群協作 `Swarm` 等）。
2. **修改 `docs/index.html`**：
   * 將新策略的檔名（如 `TnSovereignPropFirmUltraV6.pine`）新增至對應卡片的列表 (`<ul>` 標籤內)。
   * **重要**：必須更新 `status-bar` 區塊中的後設數據（Metadata）：
     * `LAST_UPDT`：請使用 CST 台北時間 (UTC+8) 格式，例如：`2026-05-28 21:40 (CST)`。
     * `VERSION`：更新為當前時間版號，格式為 `vYY.MMDD.HHMM`（例如：`v26.0528.2140`）。
3. **更新首頁 `README.md`**：
   * 檢查首頁的「策略全分類一覽」統計表格，將對應分類的數量遞增。
   * 在「最新加入」或「上版」清單中，以當前版號格式填寫最新異動說明。

### 2. Dashboard 狀態欄更新範例

```html
<div class="status-bar">
    LAST_UPDT: 2026-05-28 21:40 (CST)<br>
    VERSION : v26.0528.2140<br>
    STATUS  : DISCIPLINED_EVOLUTION_ACTIVE
</div>
```

---

## 📐 策略命名與版號規訓

1. **檔案命名**：
   * 策略檔案必須使用 `v6` 結尾，採用 CamelCase 或 snake_case（例如：`TnSovereignPropFirmUltraV6.pine` 或 `tn_fakeout_signal_quality_v6.pine`）。
   * 每個 `.pine` 策略檔案，必須一對一配合同步建立一個同名的 `.md` 說明文件（例如：`TnSovereignPropFirmUltraV6.md`）。
2. **程式碼內部版號標記**：
   * 策略頂部的註解中，版號與時間戳必須鎖定 CST (UTC+8)。

---

## 📜 聲明

*執行主權，因果必達。請確保每次提交（Commit）皆維持程式碼與 Dashboard 的完全對位。*

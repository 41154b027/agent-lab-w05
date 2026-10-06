# 東華校園 AI Agent 實作紀錄（Learning Record）

- **學生代碼 / 組別：** W05
- **實作日期：** 2026-10-06
- **實作工具：** Antigravity (Google DeepMind)
- **實作路線：** 個人路線（Individual）
- **完成項目：** 任務 A、任務 B（含 v1 與 v2 改版）、任務 C、任務 D

---

## 任務歷程摘要

### 任務 A：整理社團雜亂檔案（01-club-files）
- **盤點結果：** 輸入 12 個文字檔案，其中包含 2 組內容完全相同的檔案（`announcement` 與 `equipment` 系列），以及 2 份名稱相近但內容不同的企劃案（`proposal_final.txt` 為室外方案、`proposal_final2.txt` 為室內方案）。
- **處理原則：** 原始檔案完全保留在 `input/` 不動；所有整理於 `output/` 建立 4 個分類資料夾（`proposals`, `meetings`, `publicity`, `equipment`），不刪除任何檔案，產出完整 `manifest.json` 與 `report.md`。
- **Commit：** `A: organize club files` (`7aed2e6`)

### 任務 B：課間活動挑選器（02-campus-picker）
- **第一版（v1）：** 讀取 12 筆課間活動，產出單一離線網頁 `index.html`。支援地點（室內/室外/不限）、可用時間（15/30/60分鐘）、強度（低/中/不限）三條件嚴格篩選隨機抽選；支援無符合項目警示、最近 5 次成功紀錄、重設篩選、中英文即時切換。
- **Commit v1：** `B v1: activity picker` (`628ef87`)
- **改版（v2）：** 依據使用者體驗需求，加入即時符合筆數動態統計標籤，並加入鍵盤 `Enter` 快捷挑選功能。
- **Commit v2：** `B v2: add match count indicator and keyboard shortcut` (`85f42a5`)

### 任務 C：社團器材記錄清理（03-equipment）
- **清理成果：** 原始 10 筆資料移除全空空白列，產生 9 筆標準化資料 `normalized.json`。文字欄位去空格、狀態統一為 `available` / `borrowed`，未知狀態標記為 `unknown`。相同 `item_id`（EQ01、EQ02）全數保留，異常數量（空白與負數）原樣保留不瞎猜，完整記錄於 `issues.md`。
- **Commit：** `C: clean equipment records`

### 任務 D：計畫審查與退回（04-review）
- **審查材料：** `bad-plan.txt`
- **退回重點：** 指出「越界存取 Downloads」、「刪除重複檔案」、「主觀以 final2 當最新版」、「捏造缺值補合理值」、「擅自自動公開」等 5 項重大缺失，並提出合規替代方案。
- **Commit：** `D: rejection` (`a344ae2`)

---

## 學習心得與反思
1. **Agent 的邊界控制（Scope Control）：** 指令越明確、邊界定義越清楚，Agent 越能安全執行。在第一階段「只看不動」的確認機制是防止破壞性操作的重要關鍵。
2. **非破壞性原則（Non-destructive）：** 面對重複檔案或多版本時，保留副本與詳細日誌比貿然刪除更為安全可靠。
3. **驗收與人為把關（Human in the loop）：** AI 產出的程式碼與整理成果，必須透過實際極端值（如無符合條件）與功能測試親自驗證，不能只看 AI 說「完成」就盲目相信。

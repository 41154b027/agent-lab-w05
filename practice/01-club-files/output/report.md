# 社團檔案整理報告（Task A 整理成果）

## 一、分類說明
本題輸入共 12 個文字檔案，已全部完整保留於 `input/` 原始資料夾。依據活動籌備性質，在 `output/` 建立 4 個分類資料夾並各存一份副本：

1. **`proposals/`（企劃與預算類）**
   - `proposal_final.txt`：企劃草案一（室外 30 分鐘方案）。
   - `proposal_final2.txt`：企劃草案二（室內 20 分鐘方案）。
   - `budget_draft.txt`：活動預算草案（非正式核准支出，標示 100 虛擬單位）。
   - `rain_plan.txt`：雨天備案企劃。

2. **`meetings/`（會議紀錄與追蹤類）**
   - `meeting_notes.txt`：幹部會議筆記，討論室內或室外選項。
   - `next_steps.txt`：下一步指示（提醒比較兩份企劃，勿預設立場）。
   - `feedback_questions.txt`：活動問卷與回饋設計題目。

3. **`publicity/`（宣傳與通知類）**
   - `announcement.txt`：行前公告文案。
   - `announcement_copy.txt`：行前公告副本（內容完全相同）。
   - `poster_text.txt`：海報短標語。

4. **`equipment/`（器材物資類）**
   - `equipment_list.txt`：器材清單（白板筆 4、紙 2 包）。
   - `equipment_backup.txt`：器材清單副本（內容完全相同）。

---

## 二、內容相同檔案（完全重複項目）
經由 SHA-256 雜湊比對，以下兩組檔案內容完全相同：
- `announcement.txt` 與 `announcement_copy.txt`
  - SHA-256：`C19164B1054EBF52ED33BC5321C887985EA043A0B07DB1E99F866986D2CCD584`
- `equipment_list.txt` 與 `equipment_backup.txt`
  - SHA-256：`C21D53BA1F8D3AD06E1833539935120A5BACA4D13B34A2AA98CE157FF4502FA3`

**處理方式：** 依任務卡規範，相同內容各自保留副本於對應分類資料夾，未進行任何刪除或覆蓋。

---

## 三、名稱相近但內容不同（待人為確認）
- **`proposal_final.txt` vs `proposal_final2.txt`**：
  - `proposal_final.txt` 規劃為「室外活動，30 分鐘」。
  - `proposal_final2.txt` 規劃為「室內活動，20 分鐘」。
  - **重要警示：** 檔名帶有 `final` 或 `final2` 並不代表正式定稿或最新版。兩者分別代表室外與室內的不同構想，需由社團幹部開會決議採用哪一方案。

---

## 四、待確認問題
1. **活動地點與時間尚未定案：** `announcement.txt` 提及時間地點未定，須等會議決議方案後更新。
2. **預算尚未核准：** `budget_draft.txt` 所列金額為草案，尚未經正式經費審核。
3. **重複副本清理時機：** `announcement_copy.txt` 與 `equipment_backup.txt` 現已保留副本，後續可由負責人確認是否留存或歸檔。

---

## 五、實際做過的檢查
1. **原檔完整性檢驗：** 確認 `input/` 資料夾內 12 個檔案完全未被移動、修改或刪除。
2. **輸出副本數量檢驗：** 確認 `output/` 內分類複製後共有 12 個檔案，無遺漏。
3. **內容一致性檢驗：** 比對原檔與複製副本的雜湊值，內容完全一致，未被更動。
4. **輸出清單檢驗：** `output/manifest.json` 包含 12 筆物件，格式正確。

---

## 六、還沒確認的部分
1. **文字編碼與跨系統換行相容性：** 各檔案在 Windows 與 Unix 系統間之換行符號（CRLF vs LF）未統一轉換。
2. **實體業務真實性：** 本次為教學模擬資料，未涉及真實社團決策。

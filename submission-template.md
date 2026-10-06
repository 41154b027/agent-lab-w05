# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：W05
- Tool / 工具：Antigravity (Google DeepMind)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, C, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（採用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：確認 AI 操作範圍與資料夾邊界；檢查第一階段計畫是否擅自刪檔或覆蓋；驗收 A 題 12 個檔案之原檔完整性與分類副本；測試 B 題活動挑選器各項篩選條件與無符合之極端狀況；提出 B 題 v2 新需求（符合筆數即時提示與鍵盤快捷鍵）；驗收 C 題資料清理規則與問題報告；審查並退回 D 題不安全計畫。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- Task A：僅允許讀取 `practice/01-club-files/input`，僅允許寫入 `practice/01-club-files/output`，原檔保持唯讀不修改。
- Task B：僅允許讀取 `practice/02-campus-picker/activities.json`，僅允許產出單一離線網頁 `practice/02-campus-picker/output/index.html`。
- Task C：僅允許讀取 `practice/03-equipment/equipment.json`，僅允許產出 `practice/03-equipment/output/normalized.json` 與 `output/issues.md`。
- Task D：僅允許讀取 `practice/04-review/bad-plan.txt`，退回審查意見存於 `practice/04-review/my-rejection.md`。

What I asked for / 原始需求：
- Task A：盤點 12 個文字檔，分類複製至 output（相同檔案各留副本、不同版本均保留、不刪檔、不覆蓋），產出 `report.md` 與 `manifest.json`。
- Task B：依據 12 筆課間活動製作單頁挑選器，支援地點/時間/強度三條件過濾隨機挑選、無符合時明確提示、保留最近 5 次歷史紀錄、重設篩選、中英文切換。
- Task C：清理模擬器材記錄，去空格、標準化狀態、移除全空列、保留重複 ID 與原列號、異常數量原樣保留不猜測、產出問題報告。
- Task D：針對刻意寫錯的計畫找出至少兩個問題並提出替代方案。

What I checked before execution / 動手前我檢查了什麼：
- 在 Task A 第一階段，檢查 AI 列出的整理計畫是否試圖刪除任何檔案、是否以檔名（final/final2）擅自認定定稿。確認原檔 12 個均不動且承諾只在 output 寫入後，才回覆「執行」。
- 在 Task B 製作前，確認需求為單一離線檔案，不使用外部 CDN 或網路請求，且原始 `activities.json` 不被修改。
- 在 Task C 執行前，確認 AI 計畫不猜測數量、不合併重複 ID，原始 10 列中僅移除全空列保留 9 筆有效列。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. 室內／15分鐘／低強度 | 僅可能隨機抽到 A01、A02、A03、A04 | 多次點擊「幫我選」，抽中之 ID 均在 A01～A04 範圍內（如 A02、A04），無任何其他活動出現 | Commit `628ef87`, `index.html` 內的 `filtered` 陣列篩選邏輯 |
| 2. 室外／15分鐘／中強度（無符合活動） | 畫面顯示「沒有符合條件的活動」，不偷放寬條件 | 點擊後畫面出現紅色警示框「沒有符合條件的活動」，未放寬時間或強度條件，亦未寫入歷史紀錄 | Commit `628ef87`, 頁面顯示 `no-match-box` 元素 |
| 3. C題器材資料清理驗收 | 10 列移除 1 空列剩 9 列有效；EQ01/EQ02 保留；缺值與負數保留並列報告 | `normalized.json` 恰為 9 筆有效物件，EQ01（列1&4）、EQ02（列2&5）完整保留；`issues.md` 詳列衝突與異常 | `practice/03-equipment/output/` 檔案比對 |

## One revision / 一次修改

Before / 原來的情況：
挑選器篩選器僅能下拉選擇，使用者在按下「幫我選」之前，無法得知目前條件到底有幾筆活動符合；且只能依賴滑鼠點擊按鈕進行挑選。

Request / 我提出的修改：
新增即時「符合條件的活動筆數提示」（隨下拉選單即時更新），並支援鍵盤 `Enter` 快捷鍵，按下即可快速挑選。

After and retest / 修改後與重測結果：
修改後，切換任一選單時即時動態顯示筆數（如選「室外/30分鐘/中強度」顯示 1 筆；選「室外/15分鐘/中強度」即時顯示 0 筆）；按下鍵盤 `Enter` 鍵順利觸發隨機挑選。中英文切換時提示文字與單位亦同步切換。

New requirement or defect? / 新需求還是原規格未做到？：
新需求（原規格之篩選與挑選功能在 v1 均已正確達成，此修改屬於加強使用者互動體驗之優化）。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `bad-plan.txt` 提出的以下動作：
1. 擅自將工作範圍擴大至整台電腦的 `Downloads`（違反最小權限與安全邊界，可能誤動私人檔案）。
2. 擅自刪除重複檔案，並以檔名 `final2` 認定為最新版（不可逆破壞性刪除；且不同企劃版本可能代表不同備案而非版本先後，如室內方案 vs 室外方案）。
3. 找不到資料就補「合理值」，完成後「自動公開成果」（偽造竄改資料、模型幻覺；成果未審查即公開有極高資安隱私風險）。

An acceptable alternative / 可以怎麼改：
1. 嚴格限縮工作路徑在指定練習資料夾內。
2. 原始檔案完全保留不動，相同檔案各自保留副本於 output，不同版本全部保留由人工比對決策。
3. 缺失值如實標示為 `unknown` 或 `missing` 並記錄於報告。
4. 成果僅存於本地 output 資料夾供人工驗收，絕不自動聯網發布。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. 挑選器的隨機抽籤在統計學上的均勻性（少數幾次測試僅能驗證篩選邏輯，無法保證百萬次抽籤之機率完全均勻）。
2. 在非常規小螢幕裝置或老舊瀏覽器上的極端排版渲染情況。
3. 整理出的文字檔案在不同作業系統（Windows CRLF vs Linux/macOS LF）間的行尾編碼相容性。

# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：G-w05
- Tool / 工具：Antigravity (Pair Programming Agent)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, C, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（採用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：
  使用者與驗收者；動手前審查 Agent 計畫是否越界、是否保留原檔；執行後以 SHA-256 雜湊驗證 Task A 檔案完整性；手動測試 Task B 活動挑選器之各項篩選條件、無結果提示、歷史紀錄上限與中英雙語切換；審核 Task C 器材資料清理衝突；對 Task D 提出嚴格退回要求與替代規範。

---

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- Task A: 輸入 `practice/01-club-files/input`，輸出 `practice/01-club-files/output`
- Task B: 輸入 `practice/02-campus-picker/activities.json`，輸出 `practice/02-campus-picker/output`
- Task C: 輸入 `practice/03-equipment/equipment.json`，輸出 `practice/03-equipment/output`
- Task D: 輸入 `practice/04-review/bad-plan.txt`，輸出 `practice/04-review/my-rejection.md`
- 嚴格限制僅能存取當題資料夾，禁止碰觸外部目錄（如 Downloads）或系統檔案。

What I asked for / 原始需求：
1. Task A：分析 12 個檔案，提出計畫後執行；原檔不動，產出 12 份分類副本、`report.md` 與最外層 12 筆陣列之 `manifest.json`。
2. Task B：製作離線單頁「課間我想做什麼？」挑選器 `output/index.html`；支援地點/時間/強度篩選、隨機抽選、查無符合提示、最近 5 筆紀錄、重設篩選、中英文切換與模擬免責標示。
3. Task C：清理 `equipment.json`，去空白、狀態正規化、移除全空列、保留來源列號與相同 ID 紀錄、異常數量原樣保留，產出 `normalized.json` 與 `issues.md`。
4. Task D：審查 `bad-plan.txt` 模擬錯誤計畫，圈出問題並撰寫可接受之替代方案退回說明。

What I checked before execution / 動手前我檢查了什麼：
- 確認工作目錄範圍是否限定在各題資料夾。
- 檢查 Agent 是否有企圖刪除原檔、私自覆蓋既有成果或自動對外連線的危險計畫。
- 確認 Agent 未依檔名 `final` 或 `final2` 擅自認定定稿，堅持保留全數版本副本供人工確認。

---

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1 (Task A 檔案與雜湊) | input 12 檔不動；output 分類保留 12 份副本；SHA-256 與原檔 100% 吻合 | 12 份原檔完整留存；output 5 個資料夾共 12 份副本；經比對雜湊值完全相同；產生 12 筆物件之 manifest.json | `practice/01-club-files/output/manifest.json`<br>`practice/01-club-files/output/report.md` |
| 2 (Task B 邊界無符合) | 篩選條件：室外／15分鐘／中強度，應清楚顯示「沒有符合條件的活動」，不偷放寬條件 | 畫面清楚顯示紅框警告「沒有符合條件的活動」，條件未被放寬，且不加入歷史紀錄 | `practice/02-campus-picker/output/index.html` 瀏覽器實測 |
| 3 (Task B 唯一符合項) | 篩選條件：室外／30分鐘／中強度，每次抽選必須為 A09 | 連續抽 5 次，每次皆精準命中 A09（在合適位置快走） | `practice/02-campus-picker/output/index.html` 瀏覽器實測 |
| 4 (Task C 資料清理) | 原始 10 列移除 1 列全空列得 9 列有效資料；保留 EQ01、EQ02 重複紀錄並指出數量衝突；保留負數與空字串原值 | 產出 9 列紀錄，全空列移除，EQ01、EQ02 完整保留並在 issues.md 標明 EQ02 數量衝突（2 vs 3），EQ04 空字串與 EQ05 負數原值保留 | `practice/03-equipment/output/normalized.json`<br>`practice/03-equipment/output/issues.md` |

---

## One revision / 一次修改

Before / 原來的情況：
在 Task B 第一版（v1）中，當符合條件的候選項大於 1 個時（例如「室內 / 15分鐘 / 低強度」有 4 項），完全採獨立隨機抽選，偶爾會出現連續兩次抽到同一個活動（如連續兩次皆為 A01）的情形。

Request / 我提出的修改：
增加推薦多樣性機制：當符合條件之活動數量大於 1 時，下次抽選自動排除上一筆抽中的活動，避免連續兩次重複；若符合項目僅有 1 個時（如 A09）則維持正常抽選。

After and retest / 修改後與重測結果：
在「室內 / 15分鐘 / 低強度」進行連續多次抽選，相鄰兩次抽選不再重複出現相同活動；而在「室外 / 30分鐘 / 中強度」測試中，仍能正確且穩定抽中唯一符合項 A09。受影響之原本 6 項功能測試皆重新驗證通過。

New requirement or defect? / 新需求還是原規格未做到？
新需求（原規格僅要求隨機抽選，增加連續不重複機制為提升使用者體驗之自訂優化）。

---

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `practice/04-review/bad-plan.txt` 中的整份計畫：
1. 拒絕「整理整個 Downloads」：嚴重越界，可能損毀使用者的個人下載檔案與系統目錄。
2. 拒絕「刪除重複檔」：不可逆破壞性行為，備份檔案可能具歷史追溯價值，不可未經確認擅自刪除。
3. 拒絕「把 final2 當最新版」：檔名不等於定案，版本採納應由幹部或人類負責人審查。
4. 拒絕「找不到資料就補合理值」：偽造數據、破壞資料真實性，掩蓋紀錄缺陷。
5. 拒絕「自動公開成果」：未經人工驗核即對外發布，有嚴重資安與隱私外洩風險。

An acceptable alternative / 可以怎麼改：
1. 嚴格限縮工作目錄在指定的練習資料夾。
2. 原始檔案維持唯讀，僅在 output/ 建立副本，不刪除任何原檔。
3. 相同內容保留副本，相近版本全數保留並在 report.md 列出差異對照表。
4. 缺漏數據原樣保留，不擅自猜測補值，於 issues.md 記錄問題列號以供人工查核。
5. 產出僅限於本機目錄供使用者驗收，嚴禁自動連外或未經授權公開。

---

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. Task A 中的活動企劃案（戶外 30 分鐘 vs 室內 20 分鐘）最終採納之定案版本，仍需社團幹部開會決議。
2. Task A 中內容完全重複之公告文字與器材備份檔案，尚未由負責人確認是否正式刪除。
3. Task B 隨機抽選僅驗證條件邏輯與連續不重複規則，尚未進行大規模統計檢定以證明其隨機數均勻分佈。
4. Task C 中 `EQ02` 數量衝突（2 vs 3）與 `EQ04` 缺漏數量，仍需至器材儲藏室進行實體清點以確認真實庫存。

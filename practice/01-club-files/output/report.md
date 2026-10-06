# 社團檔案整理報告（Task A: 01-club-files）

本報告記錄 `practice/01-club-files/input` 檔案整理至 `practice/01-club-files/output` 之結果與分析。

---

## 1. 整理概況與檔案盤點

- **原始輸入檔案（input）：** 12 個文字檔（原檔完全保留，未作任何修改或刪除）。
- **整理後輸出副本（output）：** 12 個檔案，分別複製至 5 個分類資料夾中。
- **一致性檢驗：** 12 個輸出副本皆通過 SHA-256 雜湊值比對，與原始檔案完全一致（100% 完整無損）。

---

## 2. 分類規劃與說明

依據檔案性質與用途，建立 5 個分類資料夾：

| 分類資料夾 | 包含檔案 | 分類說明 |
|---|---|---|
| `output/proposals/` | `proposal_final.txt`<br>`proposal_final2.txt`<br>`rain_plan.txt` | 活動主企畫草案與雨天備案企劃 |
| `output/meetings/` | `meeting_notes.txt`<br>`next_steps.txt` | 開會記錄與活動後續追蹤事項 |
| `output/publicity/` | `announcement.txt`<br>`announcement_copy.txt`<br>`poster_text.txt` | 社團公告與海報宣傳文字文案 |
| `output/resources/` | `budget_draft.txt`<br>`equipment_list.txt`<br>`equipment_backup.txt` | 活動預算草案與器材清單備份 |
| `output/feedback/` | `feedback_questions.txt` | 活動後續意見與問卷題目 |

---

## 3. 重複檔案與版本差異分析

### (1) 內容完全相同之重複檔案（已各留副本，未刪除）
經 SHA-256 比對，以下兩組檔案內容完全相同：
1. `announcement.txt` 與 `announcement_copy.txt`
   - **SHA-256：** `C19164B1054EBF52ED33BC5321C887985EA043A0B07DB1E99F866986D2CCD584`
   - **內容：** 「SIMULATION / 教學模擬 Bring your own notebook. Time and location are undecided. 請帶筆記本。時間地點尚未決定。」
   - **處理：** 兩者皆複製至 `output/publicity/` 保留，待活動幹部確認是否刪除或改名。
2. `equipment_list.txt` 與 `equipment_backup.txt`
   - **SHA-256：** `C21D53BA1F8D3AD06E1833539935120A5BACA4D13B34A2AA98CE157FF4502FA3`
   - **內容：** 「SIMULATION / 教學模擬 markers: 4 paper packs: 2」
   - **處理：** 兩者皆複製至 `output/resources/` 保留備查。

### (2) 檔名相近但內容不同之企畫版本（均保留，不依 final 命名認定）
- `proposal_final.txt`：
  - **內容：** 「Proposal v1: outdoor activity, 30 minutes. 企畫第一版：戶外活動，30分鐘。尚未定案。」
- `proposal_final2.txt`：
  - **內容：** 「Proposal v2: indoor activity, 20 minutes. 企畫第二版：室內活動，20分鐘。仍待討論。」
- **說明：** 依規範不得因檔名含 `final` 或 `final2` 而擅自認定最新版或定稿，兩者皆為待決策方案，全數完整保留於 `output/proposals/`。

---

## 4. 待確認問題（需幹部或負責人決策）

1. **企劃案定稿確認：** `proposal_final.txt`（戶外30分鐘）與 `proposal_final2.txt`（室內20分鐘）尚未定案，且 `rain_plan.txt` 與 `meeting_notes.txt` 皆提及室內室外之取捨，需由社長或社員大會開會決議最終採行版本。
2. **宣傳公告細節待補：** `announcement.txt` 提及「時間地點尚未決定」，後續應於確認場地與時間後更新定稿，並可清除重複之 `announcement_copy.txt`。
3. **預算審核：** `budget_draft.txt` 標明模擬值 100 尚未核定，需由總務人員編列正式預算並送審。

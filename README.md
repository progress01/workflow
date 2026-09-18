# Project Lab README｜手動 AI 模式

## 1. 這個工具是做什麼的

Project Lab 是「正式白板」之外的專案規劃與推演空間。

它的目的不是取代正式白板，而是把以下幾件事分開：

- **正式白板**：目前真正採用、正在執行的專案版本。
- **Project Lab**：檢討、討論、假設、風險、方案推演。
- **AI**：協助分析與提出候選方案，不直接改正式資料。
- **人工決策**：最後由自己判斷哪些方案值得採用，再手動更新正式白板。

核心原則：

> 正式資料保持穩定；思考空間允許混亂；候選方案可以大改；最後再由人決定。

---

# 2. 主要資料物件

## Project
專案層級資訊。

建議欄位：

- projectId
- 專案名稱
- 專案目的
- Deadline
- Deadline 類型：硬期限 / 目標日期
- Definition of Done
- Constraints
- Milestones
- Next Review Date
- Planning Horizon（近期要規劃到多細）

---

## Snapshot
某一時間點的正式專案狀態。

用途：

- 保存「當時真實狀態」
- 讓 AI 建議可以追溯
- 避免數天後正式白板改變，卻不知道 AI 當時是依據哪一版分析

Snapshot 原則：

- 唯讀
- 不修改歷史
- 每次重要檢討前可建立一份

---

## Review
一輪完整的思考或 AI 討論紀錄。

應保存：

- 基於哪一個 Snapshot
- 使用哪個 Prompt 模板
- 自訂問題
- 實際送給 AI 的 Prompt
- AI 完整回答
- 自己的補充與反應
- 時間

Review **不要求形成結論**。

資訊不足、仍有疑問，本身就是合理結果。

---

## Finding
從 Review 中提煉出值得追蹤的事項。

建議類型：

- Assumption：尚未驗證的假設
- Risk：尚未發生，但可能影響專案
- Issue：已經發生的問題
- Dependency：依賴條件
- Decision Candidate：需要決定，但目前尚未定案

Finding 不等於正式工項。

---

## Decision
真正作出的專案決策。

建議記錄：

- 問題
- 當時背景
- 考慮過的方案
- 決定
- 理由
- Trade-off / 代價
- Confidence
- 狀態：Accepted / Superseded / Rejected

舊 Decision 不直接修改。
若未來改變決策，新增一筆 Decision，並標示舊決策已被取代。

---

## Scenario
從 Snapshot 複製出的「完整候選專案版本」。

Scenario 可以自由：

- 新增卡
- 刪除卡
- 拆卡
- 合併卡
- 改日期
- 改預估工時
- 改順序
- 改產出
- 改驗收條件
- 改專案安排

但是：

- 實際工時唯讀
- 工作紀錄唯讀
- 已發生歷史唯讀

Scenario 是推演空間，不是正式資料。

---


# 2.1 工時資料：規劃與實際必須一起看

Project Lab 會把正式白板的 `workLogs` 一起帶入 Snapshot 與 AI Context。

每張既有卡片至少比較：

- 預估工時
- 實際累積工時
- 工時使用率
- 預估尚餘 / 已超出
- 實際開始日期
- 最後一筆實際工時日期
- 每筆工時明細：日期、分鐘、來源、工作內容

注意：

- **進行中的工項**不能把「實際少於預估」直接解讀成估算準確，因為工作可能尚未完成。
- **完成的工項**才比較適合回顧估算誤差。
- 沒有預估工時但已有實際工時，應標示為「未規劃工時」，這本身就是規劃檢討訊號。
- 自由卡若有工時，也應保留，因為它可能代表原本未被排進正式工項的投入。

在 Scenario 中：

- 預計日期、預估工時、產出、驗收條件可調整。
- `workLogs`、工作紀錄、目前既有狀態與進度屬於歷史事實，唯讀。
- AI 產生 Scenario JSON 時不需要回傳 `workLogs` / `entries`。Project Lab 會依 `baseSnapshotId` 自動補回，避免 AI 改寫歷史。

因此：

> Scenario 改的是未來計畫；Snapshot 保存的是當時事實；工時明細連接兩者，讓估算與實際可以被真正比較。


# 3. 建議日常使用流程

## 情境 A：只是想檢討目前專案

1. 從正式白板讀入專案
2. 建立 Snapshot
3. 選擇 AI Review 模板
4. 在「我的額外問題」輸入真正困惑的地方
5. 產生 Prompt
6. 把 Prompt 貼到 AI，取得回答後手動貼回
7. 把完整回答存成 Review
8. 有重要內容時才轉成 Finding
9. 不需要為了「有產出」硬做 Scenario

合理結果可能只是：

> 現在資訊不足，需要先確認兩件事。

這不是失敗。

---

## 情境 B：開始形成候選方案

1. 選擇一份 Snapshot
2. 回顧相關 Review / Finding / Decision
3. 從 Snapshot 建立 Scenario
4. 自己修改，或要求 AI 提出候選安排
5. 在 Scenario 中自由推演
6. 使用「檢查 Scenario」再讓 AI 挑戰一次
7. 與 Snapshot 比較 Diff
8. 決定：
   - 繼續調整
   - 不採用
   - 決定採用

決定採用後，**目前仍手動更新正式白板**。

這是刻意保留的學習步驟。

---

## 情境 C：規劃變化很大

不要要求 AI 只回欄位變更。

流程改為：

1. 先進行 Review
2. 記錄重大 Finding
3. 確認必要 Decision
4. 建立完整 Scenario
5. 在 Scenario 中重新規劃整個專案
6. 最後才由系統計算 Snapshot vs Scenario 的 Delta

原則：

> Delta 是比較結果，不是思考格式。

---

# 4. AI 互動模式：固定採手動 Copy / Paste

Project Lab v1.2 不直接呼叫生成式 AI API，也不保存生成式 AI API Key。

固定流程：

1. 在 Project Lab 選擇專案與 Snapshot。
2. 選擇 Prompt 模板。
3. 在「這次我特別想問」補上自己的問題。
4. 按「產生提問」。
5. 按「複製完整提問」。
6. 貼到 ChatGPT / Gemini / Claude 或其他 AI。
7. 將 AI 完整回答貼回 Project Lab。
8. 一般分析存成 Review。
9. 有追蹤價值的內容再轉成 Finding。
10. 真正形成候選規劃後，再要求 AI 輸出 Scenario JSON。
11. 將 Scenario JSON 貼回 Project Lab 驗證與匯入。

這種模式刻意保留人工閱讀與判斷，讓 AI 不會在背景自動改變資料。

## 為什麼目前採手動模式

- 可以在 AI 介面繼續追問，不被單次 API 回覆限制。
- 可以先看完整回答，再決定哪些內容值得帶回 Project Lab。
- 不需要管理生成式 AI API Key、額度、模型版本或錯誤重試。
- 不會因為「按一個按鈕很方便」而把思考、決策和正式資料更新綁在一起。
- 比較符合目前的目標：練習專案規劃，而不是追求最大程度自動化。

## 兩種貼回方式

### A. 一般文字 → Review

任何自然語言回答都可以直接保存。

適合：
- 專案健檢
- 找未知與假設
- 期限壓力
- Premortem
- 工項拆解討論
- 方案優缺點比較

### B. 結構化 JSON → Scenario

只有當討論已形成一個值得試排的方案時才使用。

Project Lab 會驗證：
- schemaVersion
- projectId
- baseSnapshotId
- 卡片 ID
- 新卡 temp_ ID
- 歷史工時與工作紀錄不得由 AI 回傳或改寫

格式錯誤時，可使用「複製修復提示詞」請 AI 只修格式。


# 5. 哪些項目暫時不要直接交給 AI

v1 不建議 AI 直接：

- 修改正式白板
- 刪除正式卡片
- 修改實際工時
- 修改歷史工作紀錄
- 自動關閉 Finding
- 自動建立 Accepted Decision
- 自動把 Scenario 套用正式資料

這些都應保留人工確認。

---

# 6. 建議內建 AI Prompt 模板

## A. 專案健檢

目的：

- 找出規劃結構問題
- 找資訊不足
- 找不合理依賴
- 不強迫產生修改方案

---

## B. 期限壓力分析

AI 應檢查：

- Deadline
- Milestones
- 剩餘工時
- 尚未開始工項
- 高風險工項
- Blocking issue
- 哪些工作可能應延後或降級

---

## C. 找未知與假設

AI 應把內容分成：

- 已知事實
- 尚未驗證假設
- 缺少資訊
- 需要決定事項

---

## D. 工項拆解

AI 應檢查：

- 一張卡是否同時包含多個產出
- 驗收條件是否混在一起
- 是否拆得過細
- 是否存在不必要的卡片

---

## E. 產出與驗收檢查

AI 應回答：

- 產出是否具體
- 驗收是否可判斷
- 「做了工作」和「完成成果」是否混淆

---

## F. Premortem：假設專案失敗

Prompt 核心：

> 假設已經到了 Deadline，而專案沒有達成預期成果。  
> 根據目前 Snapshot，列出最合理的失敗原因。  
> 區分 Risk、Issue、Assumption、Dependency。  
> 不要把所有極端例外都列入，只保留足以影響專案成果的項目。

---

## G. Scenario Review

目的：

不是重新規劃，而是挑戰目前 Scenario：

- 是否能在期限完成
- 是否遺漏依賴
- 工時是否自洽
- 是否存在同時過度承諾
- 是否有必要保留人工流程

---

# 7. 自訂問題欄位

每個 Prompt 模板下方保留：

> 「這次我特別想問」

例如：

- 我不確定 02 要不要拆成兩張卡。
- 我擔心圖表與目錄在 9/30 前來不及。
- 我不知道現在是不是過度在意例外案例。
- 請不要替我直接決定，先指出目前缺少哪些資訊。

系統產生 Prompt 時：

`固定模板 + 專案資料 + Snapshot + 自訂問題`

---

# 10. 建議的第一次使用

1. 選擇一個正在進行中的專案。
2. 補上 Deadline。
3. 寫 Definition of Done。
4. 寫 3～5 個 Constraints。
5. 建立 Snapshot。
6. 使用「專案健檢」。
7. 把 AI 回答存成 Review。
8. 挑 1～3 個真正影響專案的內容建立 Finding。
9. 若出現需要取捨的問題，再建立 Decision。
10. 從 Snapshot 建立一個 Scenario。
11. 只調整最近 1～2 週需要詳細規劃的內容。
12. 使用 Scenario Review。
13. 比較 Diff。
14. 決定是否採用。
15. 手動更新正式白板。

---

# 11. 使用時最重要的幾個原則

### 不要求每一輪 AI 討論都有變更
「目前不要改，先確認資訊」可以是正常結果。

### 不把 AI 分析當成事實
AI 提出的未知、風險、推論應留在 Review / Finding，直到被驗證。

### 不要求遠期工作和近期工作有相同精度
近期詳細，遠期保持粗略。

### 不因為 Scenario 可以亂改，就改寫歷史
Scenario 改未來，不改已發生事實。

### 不把所有風險都列入
優先追蹤會改變決策、期限、成本或成果的項目。

### Decision 要留下理由
數字改變不重要，為什麼改才有學習價值。

---

# 12. v1 成功標準

Project Lab v1 不以「功能很多」為成功。

應觀察：

1. Review 是否真的幫助重新理解專案。
2. Finding 是否能區分未知與正式工作。
3. Decision 是否留下了可回顧的理由。
4. Scenario 是否讓人更敢推演不同方案。
5. Diff 是否能清楚看到正式版與候選版的差異。
6. 手動更新正式白板時，是否能重新思考一次規劃。
7. 使用 2～3 個專案後，是否逐漸看見自己常見的估算與拆解模式。

如果以上成立，再增加自動化。


# 13. 關於 HTML 裡的 Firebase apiKey

`project_lab_v1_2_manual.html` 仍保留原本 Firebase Web 設定，因為目前工具使用 Firebase Auth 取得使用者身分，並以同一使用者的白板 localStorage 作為資料來源。

這個 `firebaseConfig.apiKey` 是既有 Firebase Web client 設定，**不是生成式 AI API Key**。

Project Lab v1.2 沒有：
- OpenAI API Key
- Gemini API Key
- Claude / Anthropic API Key
- 任何直接呼叫生成式 AI 模型的程式

AI 協作固定採「複製 Prompt → 外部 AI 討論 → 貼回 Review / Scenario」。

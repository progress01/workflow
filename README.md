# GitHub Pages 上傳方式

此資料夾已整理成可直接上傳 GitHub Pages 的檔名：

- `index.html`：正式白板首頁
- `app.js`：正式白板程式
- `project_lab.html`：Project Lab
- `README.md`：使用說明

請把四個檔案放在同一個 GitHub Pages 目錄。

正式白板網址：
`https://<帳號>.github.io/<repo>/`

Project Lab 網址：
`https://<帳號>.github.io/<repo>/project_lab.html`

兩個頁面必須在同一個 origin，Project Lab 才能讀到正式白板的 localStorage。

---

# Project Lab v1.4 README

## 1. 這一版的定位

v1.4 把整套工具拆成兩個責任清楚的區域：

- **白板 & 心流沙盒**：工作現場。照原本方式記工作紀錄、心流工時、自由卡、排程卡與發想，不強迫新增固定紀錄格式。
- **Project Lab**：思考與檢討場所。讀取白板既有資料後，做聚焦規劃、管理事項、AI 教練、AI 批改、Outcome Review、Scenario 推演。

Project Lab 預設唯讀正式白板。討論後若認為正式計畫需要修正，仍由使用者回白板手動修改。

---

## 2. 檔案

正式白板：

- `index_v1_4_focus.html`
- `app_v1_4_focus.js`

Project Lab：

- `project_lab_v1_4.html`

三個檔案請放在**同一個網站 origin**。例如都在同一個 GitHub Pages 網域與路徑層級下。

`index_v1_4_focus.html` 會載入 `app_v1_4_focus.js`，所以兩個檔案必須一起上傳。

---

## 3. 白板 v1.4：聚焦執行模式

原本的工作紀錄與工時功能保留，不要求改寫紀錄習慣。

卡片的「規劃」區改成預設聚焦模式，一次處理少量問題。

### 開始做

- 我要完成什麼？
- 現在下一步是什麼？
- 下一個判斷點是什麼？

### 拆解

- 這張卡是不是太大？
- 有哪些可獨立管理的成果？
- 現在最先要確認哪一塊？

### 近期規劃

- 自由卡或排程工項
- 日期
- 預估工時
- 依賴／前置條件

### 產出／驗收

- 最後交出什麼？
- 怎樣算完成？
- 用什麼證據確認？

### 回顧

直接顯示預估與實際工時，並可留下簡短回顧。

仍可按「展開完整資料」，回到原本較完整的規劃介面。

---

## 4. 規劃成熟度

卡片增加四級規劃成熟度：

- 想法
- 可行動
- 已規劃
- 已承諾

它和「未開始／進行中／完成」是不同概念。

舊卡片沒有這些欄位也可以正常使用，系統會以預設值顯示，不做破壞性資料轉換。

---

## 5. 白板資料會如何進 Project Lab

白板仍把卡片存在：

`whiteboard_state_<Firebase UID>`

Project Lab 會在同一瀏覽器、同一 origin、同一登入帳號下直接讀取這份 localStorage。

會讀到：

- title / content
- project / category
- status / progress
- 預計日期與預估工時
- deliverable / acceptance
- 新增的 planningMaturity / nextAction / decisionPoint 等聚焦規劃欄位
- `workLogs` 心流計時與手動補登工時
- `entries` 自由工作紀錄
- 發想節點

Project Lab 不要求白板工作紀錄改成固定格式。

---

## 6. Project 層：目的、目標、目前做法

Project Lab 的 Project 區增加：

### 目的

為什麼做？真正想解決什麼問題？

### 目標

在這個期限內，要達到什麼狀態？

### 目前做法

目前打算怎麼達成。這是可修改的手段，不視為不可變的目的。

原本的 Deadline、Definition of Done、Constraints、Milestones 等資料仍保留。

---

## 7. 管理事項：聚焦思考狀態

管理事項仍保留完整資料，但預設一次只顯示目前思考狀態相關的內容。

### 抓住

- 我的角色
- 原始交辦
- 現在下一步

### 釐清

- 真正希望得到什麼結果？
- 最重要的不知道是什麼？
- 誰可能知道／真正要問什麼？

### 判斷

- 有哪些做法？
- 各自犧牲什麼？
- 我目前傾向什麼？

### 推進

- 誰有權決定？
- 誰執行／承接？
- 現在球在誰手上？
- 何時再追？

### 收斂

- 最後怎麼處理？
- 問題有沒有解決？
- 正式計畫需不需要改？

按「展開完整資料」仍可查看背景、已知事實、連結正式卡片等完整欄位。

---

## 8. Outcome Review：留下真正值得帶走的經驗

Review 現在有兩種：

- 一般 Review：保存 AI / 人的討論與自己的後續想法。
- Outcome Review：事情結束後對照原本設想與實際結果。

Outcome Review 會記：

- 原本要解決的問題
- 已解決 / 部分解決 / 未解決 / 尚不能確認
- 原本打算怎麼解
- 實際最後怎麼解
- 為什麼不同／出現了什麼新資訊
- 本次經驗
- 是否值得提煉成可遷移原則

可以從管理事項的「收斂」狀態建立 Outcome Review，也可以在 Reviews 頁直接新增。

---

## 9. AI 使用方式：固定手動 Copy / Paste

本版不使用生成式 AI API Key。

### AI 教練

適合還在思考時。

Prompt 會要求 AI：

- 最多先提出 1～3 個真正重要的問題或判斷點
- 資訊已足夠時要明確說可以先去做
- 分辨目的、目標、手段
- 不把所有管理事項都變成自己的執行工作
- 結合預估、實際工時與工作紀錄分析

回覆用正常文字，貼回後存成 Review。

### AI 批改 Patch

適合「整體方向沒問題，只想知道哪幾個地方可以調整」。

先選一張卡，產生批改提示詞。AI 最多回傳 3 項修改。

Project Lab 會用刪除線與紅字顯示：

- 原文
- 建議文字
- 修改理由

每一項可以標記：

- 採用這項
- 保留原文
- 自己修改

這些選擇只記在 Project Lab，**不會直接寫回正式白板**。

Patch 使用 `expectedOriginal` 檢查原文。如果白板內容已經改變，會顯示過期警告。

### Scenario

只有整個計畫需要重新拆解或重排時使用。

Scenario 仍是一份完整候選專案副本，不是只有 Delta。

系統最後才比較 Snapshot 與 Scenario，算出新增、刪除、修改差異。

歷史工時與工作紀錄不允許 AI 改寫。

---

## 10. Snapshot

Snapshot 會保存當下：

- Project 資料
- 正式卡片
- 心流／手動工時
- 工作紀錄
- 發想節點
- 管理事項

因此 Review、Patch、Scenario 都能追溯「當時 AI 或自己看到的是哪一版資料」。

---

## 11. 建議第一次試用方式

不要一次把所有欄位補滿。

選一個正在進行中的專案：

1. 在 Project Lab 補目的、期限內目標、目前做法。
2. 回正式白板，挑一張正在進行的卡，先只寫「下一步」與「下一判斷點」。
3. 照原本習慣工作、計時、寫工作紀錄。
4. 過一段時間回 Project Lab 重新讀白板。
5. 建 Snapshot。
6. 用 AI 教練問 1～3 個關鍵問題。
7. 如果只是文字不清楚，用 Patch 批改。
8. 如果整體計畫真的不合理，再用 Scenario。
9. 事情結束後建立 Outcome Review，判斷問題是否真的解決。
10. 最後再自己回白板修正正式資料。

---

## 12. v1.4 刻意不做

暫時不做：

- 全專案驗收總表
- 全人員進度管理
- 跨人資源配置
- 完整責任矩陣
- AI 自動改正式白板
- AI API 串接
- 強迫工作紀錄使用固定格式

這些未來如果真的有使用需求，再從實際經驗長出來。

---

## 13. 資料相容性

- 白板 v1.4 沿用原本的 `whiteboard_state_<uid>`，舊卡可直接讀。
- Project Lab v1.4 沿用 `project_lab_state_<uid>`，會保留 v1.3 的 Project、Management、Review、Finding、Decision、Scenario 資料。
- 舊 Project 的「專案目的」欄位會在第一次載入 v1.4 時搬到新的 `purpose` 欄位，新的「目標」保持空白，讓使用者自己重新定義。
- 新增欄位不存在時都使用安全預設值，不要求一次 migration 全部補齊。

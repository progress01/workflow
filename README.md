# Project Lab v1.6.2｜中文化與存檔範圍定稿版

部署主入口仍為：`https://progress01.github.io/workflow/`

本版沿用 v1.6.1 的白板、Project Lab 與 Firebase 資料，不需要重建資料庫。`ProjectLab_Data/{uid}` 仍是同一份雲端備份。

## 本版調整

- 主介面統一使用中文與中性名稱：歷史狀態、檢討紀錄、重要發現、決策紀錄、修改建議、重新規劃方案。
- 保留 `Project Lab` 作為產品名稱；JSON 欄位、資料鍵與 API 協定仍維持英文，避免破壞既有資料相容性。
- 舊版 `lastPrompt`、`lastPatchPrompt`、`lastScenarioPrompt` 改為只存在當前頁面記憶體，不再寫入 localStorage 或 Firebase。
- 舊檢討紀錄若含 `prompt` 欄位，載入後會在新的持久化資料中移除；AI 回覆與你的後續想法仍保留。
- 「說明與分析」新增固定的「資料保存說明」。

## 存檔範圍

### 1. 正式白板

正式白板繼續自行保存工作卡、自由卡、日期、工時、工作紀錄、下一步、驗收等資料。Project Lab 只讀取，不直接改寫。

### 2. Project Lab 本機自動保存

以下資料會自動存在 `project_lab_state_<uid>`：

- 專案目的、目標、目前做法、期限、限制、里程碑
- 目前問題、補充情境、我目前怎麼看
- 管理事項與其思考狀態
- 拆解練習
- 已主動保存的檢討紀錄
- 重要發現
- 決策紀錄
- 歷史狀態
- 修改建議
- 重新規劃方案

### 3. Project Lab 雲端備份

只有按下「備份練習資料」時，才會將上述 Project Lab 持久資料備份到 Firebase `ProjectLab_Data/{uid}`。

### 4. 不會永久保存

- Gemini API Key
- 尚未主動保存的 AI 快速分析結果
- 整理詢問產生的文字
- 深入討論產生的文字
- AI 呼叫用的暫時提示內容

重新整理或關閉頁面後，這些暫時內容可以消失。若某次 AI 回覆值得留下，請按「存成檢討紀錄」。

## 歷史狀態保存內容

「保存目前狀態」會固定當下的專案資料、正式工作卡／自由卡、工時與工作紀錄、發想節點、管理事項，用於之後比較與重新規劃。它不是整份 Project Lab 的重複備份。

## 相容性

- 白板資料格式與 `whiteboard_state_<uid>` 不變。
- Firebase Collection 與 Rules 不變。
- 既有 Project、管理事項、歷史狀態、檢討紀錄、重要發現、決策、修改建議、重新規劃方案、拆解練習均沿用。
- 內部資料鍵（例如 `snapshots`、`reviews`、`scenarios`）不改名，避免資料遷移風險；畫面名稱已中文化。

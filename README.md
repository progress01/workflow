# Workflow / Project Lab v1.4

固定部署網址：

- Project Lab 主入口：https://progress01.github.io/workflow/
- 白板與心流工作區：https://progress01.github.io/workflow/whiteboard.html
- Project Lab 備用入口：https://progress01.github.io/workflow/project_lab.html

## 檔案

- `index.html`：Project Lab／專案檢討首頁
- `project_lab.html`：Project Lab 備用入口
- `whiteboard.html`：白板 & 心流工作區
- `app.js`：白板程式
- `README.md`：本說明

## 上傳方式

把以上檔案一起放在 GitHub repository 的 Pages 根目錄即可。

`index.html` 與 `whiteboard.html` 透過相對路徑互相跳轉；`whiteboard.html` 會載入同目錄的 `app.js`。

Project Lab 與白板必須維持在同一個 origin，才能共用 `whiteboard_state_<uid>` 的 localStorage 資料。

Project Lab 讀取白板資料做 Snapshot、Review、Patch、Outcome Review 與 Scenario；不直接改寫正式白板資料。

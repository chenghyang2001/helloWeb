# 第3章｜自動化 Commits

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Golden Rule: Never Code on Main（黃金法則：絕不在 Main 寫程式） |
| 2 | Scenario: The Dark Mode Experiment（情境演練：深色模式） |
| 3 | Automating the Commit: Meaningful Snapshots |
| 4 | Pushing to the Cloud: Syncing the Parallel Universe |
| 5 | The Executive Review: Automating Pull Requests |
| 6 | The Rhythm of the Architect（架構師的工作節奏） |
| 7 | Chapter Summary |

## 主要概念

- **Main 是聖地，絕不直接修改**：AI 在 main 上幻覺 = 正式應用直接崩潰
- **Branch = 平行宇宙**：在分支裡盡情破壞，main 毫髮無傷
- **AI 寫有意義的 Commit 訊息**：人累了會寫 "fixed stuff"，強迫 Claude 分析 diff 寫出符合業界標準的技術說明
- **PR = 架構師的高階審查點**：Claude 是初階工程師提案，你是資深架構師拍板
- **架構師節奏**：需求 → 建分支 → 本地測試 → AI commit → Push → PR 審閱，形成可預測的標準化循環

## 四步實作（以「深色模式」為情境演練）

| Step | 動作 | Claude 做什麼 |
|------|------|--------------|
| 1 | 建立分支 | `git checkout -b feature/dark-mode` |
| 2 | Auto Commit | 分析 diff → 自動生成專業 commit 訊息 → `git commit` |
| 3 | Push 上雲 | `git push --set-upstream origin feature/dark-mode` |
| 4 | 草擬 PR | 生成含功能摘要、技術變更清單、測試指引的結構化 PR 說明 |

> 最後一步（點 Merge）由你在 GitHub 頁面手動審閱確認——這是架構師的職責，不交給 AI。

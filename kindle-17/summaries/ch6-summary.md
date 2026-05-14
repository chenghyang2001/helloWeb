# 第6章｜進階 GitHub 工作流程與 Claude

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Panic-Free Rollback: Reversing Time（無恐慌的復原：時光倒流） |
| 2 | The Scariest Task: Database Migrations（最可怕的任務：資料庫遷移） |
| 3 | The Silent Killer: Technical Debt and Dependency Updates |
| 4 | The Monthly Refactoring Routine |
| 5 | Chapter Summary |

## 主要概念

- **架構師不恐慌**：線上崩潰時業餘者直接改 production server；專業架構師依賴自動化系統，冷靜處理
- **Git Revert ≠ 刪除歷史**：Revert 建立一個「數學上完美抵銷」的新 Commit，應用迅速退回穩定狀態，歷史完整保留
- **資料庫遷移必須有 rollback 函數**：做錯 = 用戶資料全毀，絕不讓 AI 隨興發揮，強制用結構化遷移腳本
- **軟體會「腐敗」**：5 年不動的應用因第三方套件安全漏洞而腐爛，技術債是持續累積的隱形殺手
- **重構 = 提升估值**：AI 快速寫出的 spaghetti code 降低商業價值；每月重構讓數位資產保持高流動性

## 四大進階技術

**1. 緊急 Rollback（先止血再調查）**

```
崩潰發生 → Claude 查 git log 找最後穩定 commit
→ git revert <hash> → push → CI/CD 自動重新部署
全程 < 5 分鐘，不碰 production server
```

**2. 資料庫遷移（最嚴格的場景）**

- 新分支 `feature/db-migration` → 撰寫遷移腳本
- **鐵律**：腳本必須包含 `down` / `rollback` 函數
- 遷移失敗 → 自動退回，資料不遺失

**3. Dependabot 安全警告處理**

- 收到警告 → 建立專屬更新分支（不一次更新全部）
- Claude 更新特定套件 → 掃描 codebase 確認語法相容 → PR

**4. 每月重構衝刺**

- 新分支 + 指令：「**絕對不能新增功能或改 UI**，唯一目標是讓程式碼更精簡」
- 提取重複邏輯 → 加 inline comment → PR 合併
- 頻率：每月一次，養成習慣

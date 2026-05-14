# Kindle 17 — Mastering Claude Code & GitHub

## 全書摘要（第1章 ～ 第7章）

---

# 第1章｜版本控制與 AI 的威力

## 各節大綱

| # | 節名 |
|---|------|
| 1 | Demystifying Version Control：終極時光機 |
| 2 | The "Hallucination Loop"：AI 為何需要安全網 |
| 3 | The AI Multiplier：Claude Code 作為你的 DevOps 工程師 |
| 4 | The Freedom to Break Things：開發中的心理安全感 |
| 5 | The Paradigm Shift：從寫程式到建立數位資產 |
| 6 | Chapter Summary |

## 主要概念

- **版本控制 = 時光機 + 數位金庫**：讓每一步程式碼變更可追溯、可還原，取代「隨意存本機」的危險做法
- **對抗 AI 幻覺的安全網**：AI 生成的錯誤程式碼若沒有版本控制，一個錯誤 prompt 可能永久破壞應用
- **心理安全感（破壞的自由）**：有版本控制保護後，可大膽測試新想法，不怕「改壞」
- **典範轉移**：身分從「Vibe Coder」轉變為「軟體架構師（CEO）」，目標是建立具長期商業價值的數位資產

## 學習目標

1. 理解版本控制為何在 AI 輔助開發中不可或缺
2. 消除「改壞會怎樣」的開發焦慮
3. 建立「架構師思維」——將 AI 輸出轉化為穩定結構的資產，而非拋棄式草稿

---

# 第2章｜設置 GitHub 與 Claude Code 環境

## 各節大綱

| # | 節名 |
|---|------|
| 1 | Step 1: Claiming Your Real Estate on GitHub |
| 2 | Step 2: Waking Up Claude Code |
| 3 | Step 3: The Environment Initialization Prompt |
| 4 | Chapter Summary |

## 主要概念

- **架構師心態**：你的角色不是記憶 terminal 指令，而是聘請 Claude Code 替你執行
- **PAT = VIP 數位門禁卡**：現代替代 SSH key，賦予 Claude Code 操作 GitHub 的權限，隨時可撤銷
- **委派的心理學**：Terminal 從「敵人」變成「儀表板」

## 三步實作

1. **手動生成 PAT**：GitHub → Settings → Developer settings → `repo` + `workflow` scope → 立刻複製保存
2. **喚醒 Claude Code**：Terminal → 導航到專案資料夾
3. **環境初始化提示詞**：Claude 自動 `git init` → 身分驗證 → 建 repo → commit + push

---

# 第3章｜自動化 Commits

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Golden Rule: Never Code on Main |
| 2 | Scenario: The Dark Mode Experiment |
| 3 | Automating the Commit: Meaningful Snapshots |
| 4 | Pushing to the Cloud: Syncing the Parallel Universe |
| 5 | The Executive Review: Automating Pull Requests |
| 6 | The Rhythm of the Architect |
| 7 | Chapter Summary |

## 主要概念

- **Main 是聖地，絕不直接修改**：AI 在 main 幻覺 = 正式應用崩潰
- **Branch = 平行宇宙**：在分支裡盡情破壞，main 毫髮無傷
- **AI 寫有意義的 Commit 訊息**：強迫 Claude 分析 diff 寫業界標準說明
- **PR = 架構師的高階審查點**：Claude 提案，你拍板

## 四步實作（以「深色模式」為演練）

| Step | Claude 做什麼 |
|------|--------------|
| 建立分支 | `git checkout -b feature/dark-mode` |
| Auto Commit | 分析 diff → 生成專業 commit 訊息 |
| Push | `git push --set-upstream origin feature/dark-mode` |
| 草擬 PR | 生成含功能摘要、技術變更清單的 PR 說明 |

---

# 第4章｜CI/CD 基礎入門

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Nightmare of Manual Uploads |
| 2 | The Modern Plumbing: Understanding CI/CD |
| 3 | GitHub Actions: Your Automated Assembly Line |
| 4 | Preparing the Server Connection |
| 5 | Instructing Your AI DevOps Engineer |
| 6 | The Magic of the Green Checkmark |
| 7 | Deploying Fearlessly |
| 8 | Chapter Summary |

## 主要概念

- **CI** = 品管檢查點：PR 合併前自動跑測試
- **CD** = 自動送貨車：Merge 到 main → 自動上線，人工零介入
- **GitHub Actions** = 雲端機器人軍團，YAML 讓 Claude 寫
- **GitHub Secrets** = 企業級金庫，部署金鑰加密儲存

## 三步實作

1. **存入部署金鑰**：Vercel/Netlify token → GitHub Secrets
2. **Claude 建立 Workflow**：`.github/workflows/` YAML，merge 到 main 觸發
3. **綠色打勾**：Merge → 30~60 秒 → 全球用戶看到更新

---

# 第5章｜將程式碼轉為數位資產

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Front Door of Your Asset: The README |
| 2 | Automating the Master Documentation |
| 3 | Centralizing the Brain: GitHub Issues |
| 4 | The Professional Rhythm: Issue-Driven Development |
| 5 | Internal Documentation: The "Why" Behind the Code |
| 6 | Building to Sell: The Acquire.com Mindset |
| 7 | Chapter Summary |

## 主要概念

- **運作中的應用 vs 數位資產**：有文件、可移轉 = 資產；靠記憶維持 = 脆弱應用
- **README = 資產的門面**：第一印象影響估值
- **Issue-Driven Development**：每行程式碼連結到一個 Issue
- **Acquire.com 心態**：乾淨文件 → 年營收 3-5 倍溢價出售

## 四步實作

1. **Auto-generate README**：Claude 分析 codebase → 生成含 Tech Stack、Getting Started 的 README
2. **用 GitHub Issues 管理**：每項任務 = 一個 Issue，不用外部工具
3. **Magic Resolution**：commit 訊息加 `Resolves #N` → Merge 後 Issue 自動關閉
4. **Documentation Pass**：Claude 加 inline comment，說明「為什麼」

---

# 第6章｜進階 GitHub 工作流程與 Claude

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Panic-Free Rollback: Reversing Time |
| 2 | The Scariest Task: Database Migrations |
| 3 | The Silent Killer: Technical Debt and Dependency Updates |
| 4 | The Monthly Refactoring Routine |
| 5 | Chapter Summary |

## 主要概念

- **架構師不恐慌**：依賴自動化系統，不直接改 production server
- **Git Revert ≠ 刪除歷史**：建立數學上完美抵銷的新 Commit
- **資料庫遷移必須有 rollback 函數**：做錯 = 用戶資料全毀
- **軟體會「腐敗」**：技術債是持續累積的隱形殺手
- **重構 = 提升估值**：每月清理 spaghetti code

## 四大進階技術

1. **緊急 Rollback**：`git revert` → push → CI/CD 自動重新部署，< 5 分鐘止血
2. **資料庫遷移**：遷移腳本必含 `rollback` 函數，失敗自動退回
3. **Dependabot 處理**：收到警告 → 專屬分支 → 更新特定套件 → PR
4. **每月重構衝刺**：「絕不新增功能」，唯一目標讓程式碼更精簡

---

# 第7章｜結論：完全自動化的工作流程

## 全書四大基石

| 基石 | 核心技術 | 成果 |
|------|---------|------|
| 1️⃣ 堅不可摧的金庫 | Git + GitHub + PAT | 每行程式碼追蹤備份，硬碟毀損不再致命 |
| 2️⃣ 分支的平行宇宙 | Branch + PR + Auto Commit | 絕不碰 main，超越 90% 獨立創辦人 |
| 3️⃣ 自動送貨車 | GitHub Actions CI/CD | Merge → 幾秒內自動上線，每天可部署數次 |
| 4️⃣ 高流動性數位資產 | Issue-Driven Dev + README | 隨時可移轉、可聘人、可溢價出售 |

## 核心轉變

```
Before：Prompter（提示詞玩家）
        本地硬碟 → 混亂檔案 → 恐懼改壞 → 手動上傳

After：Software Architect（軟體架構師）
        雲端金庫 → 平行宇宙 → 自動化工廠 → 隨時出售
```

> 軟體工廠已建置完畢，裝配線順利運轉。現在把專注力放在真正重要的事：**行銷、擴展與增加營收**。

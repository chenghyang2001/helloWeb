# 第2章｜設置 GitHub 與 Claude Code 環境

## 各節大綱

| # | 節名 |
|---|------|
| 1 | Step 1: Claiming Your Real Estate on GitHub（建立 GitHub 空間） |
| 2 | Step 2: Waking Up Claude Code（喚醒 Claude Code） |
| 3 | Step 3: The Environment Initialization Prompt（環境初始化提示詞） |
| 4 | Chapter Summary |

## 主要概念

- **架構師心態**：你的角色不是記憶 terminal 指令，而是聘請 Claude Code（無限耐心的 DevOps 工程師）替你執行
- **Personal Access Token（PAT）= VIP 數位門禁卡**：現代替代 SSH key，賦予 Claude Code 操作 GitHub 的權限，隨時可撤銷
- **委派的心理學**：Terminal 從「敵人」變成「儀表板」，用來監控 AI 員工自主執行工作

## 三步實作流程

**Step 1：手動生成 PAT（唯一純手動步驟）**

1. GitHub → Settings → Developer settings → Personal access tokens → Classic
2. 勾選 **`repo`**（私有庫完整控制）+ **`workflow`**（未來自動化部署）
3. 生成後**立刻複製儲存**——離開頁面後永遠消失

**Step 2：喚醒 Claude Code**

- 打開 Terminal → 導航到專案資料夾 → 啟動 Claude Code

**Step 3：用「環境初始化提示詞」自動完成所有 git 設定**

Claude Code 依序自動執行：

1. 確認 git 已安裝
2. `git init` 初始化
3. 用 PAT 進行 GitHub 身分驗證
4. 在 GitHub 建立同名私有 repo
5. Commit + Push 到 master

> 若遇到問題（如未設定 Git Email），Claude 不會報錯當機，而是用白話文解釋並等待你批准修復指令。

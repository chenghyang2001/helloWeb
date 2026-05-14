# helloWeb

> **留言自動觸發 AI PR Pipeline 的示範專案**

在網頁輸入一則留言，背後自動完成：建立 Git branch → 建立 GitHub PR → 三個 Claude AI Agent 依序處理 → 自動合併。

---

## 線上展示

**網頁**：[https://chenghyang2001.github.io/helloWeb/](https://chenghyang2001.github.io/helloWeb/)

---

## 功能概覽

| 功能 | 說明 |
|------|------|
| 即時時鐘 | 頁面顯示 `HH:MM:SS`，每秒更新 |
| 留言送出 | 輸入文字 → 自動建立 GitHub PR（需 GitHub PAT） |
| PR 狀態追蹤 | 建立後每 10 秒輪詢 CI 狀態，顯示 ⏳ / ✅ / ❌ |
| Token 管理 | GitHub PAT 存在瀏覽器 `localStorage`，有彈窗 UI 設定 |

---

## 自動化 Pipeline

本專案有三條 Workflow，各自負責不同的觸發情境：

| Workflow | 觸發條件 | 說明 |
|----------|----------|------|
| `pr-agent-pipeline.yml` | 網頁留言建立 PR | 主流程：classify → resolver → qa → merge |
| `issue-driven-pipeline.yml` | 手動建立 GitHub Issue | 從 Issue 標題/內文自動產生 PR 並執行 pipeline |
| `auto-merge-comment-pr.yml` | comment-* branch 的 PR | 自動合併通過 QA 的 PR |

```
使用者送出留言（或建立 Issue）
      ↓
JavaScript → GitHub API
  1. 取得 master SHA
  2. 建立 comment-{timestamp} branch
  3. 寫入 comments/{timestamp}.md
  4. 建立 PR
      ↓
GitHub Actions（pr-agent-pipeline.yml）
  classify  → Claude Haiku  判斷 PR 類型
  resolver  → Claude Sonnet 處理並可修改 PR
  qa        → Claude Sonnet 驗證品質
  merge     → 自動合併並刪除 branch
```

---

## 技術棧

- **前端**：HTML5 + Vanilla JavaScript（無框架，單一 `index.html`）
- **CI/CD**：GitHub Actions
- **AI**：Anthropic Claude API（Haiku + Sonnet）
- **部署**：GitHub Pages（master branch 根目錄）

---

## 本地開發

```bash
# 不需要安裝套件，直接開啟
open index.html
# 或用 VS Code Live Server
```

**GitHub PAT 設定（首次使用）：**

1. GitHub → Settings → Developer settings → Tokens (classic)
2. 勾選 `repo` + `workflow` 權限，90 天有效期
3. 在網頁右下角「設定 / 更換 GitHub Token」填入

---

## 專案結構

```
helloWeb/
├── index.html                    # 主頁面（單一檔案）
├── spec.md                       # 功能規格文件
├── pipeline.config.json          # Pipeline 設定
├── scripts/
│   ├── classify_pr.py            # Claude Haiku：分類 PR 意圖
│   ├── resolver_agent.py         # Claude Sonnet：處理 PR
│   └── qa_agent.py               # Claude Sonnet：QA 驗證
├── comments/                     # PR 合併後的留言 Markdown 檔
└── .github/workflows/
    ├── pr-agent-pipeline.yml         # 主 Pipeline（classify→resolver→qa→merge）
    ├── issue-driven-pipeline.yml     # Issue 觸發模式
    └── auto-merge-comment-pr.yml     # 自動合併機制
```

---

## 環境設定

### GitHub Secrets（Repo 管理者必設）

| Secret 名稱 | 說明 | 設定路徑 |
|-------------|------|----------|
| `ANTHROPIC_API_KEY` | Anthropic API Key，需有 Credits | Repo → Settings → Secrets and variables → Actions |

### 瀏覽器設定（使用者端）

GitHub PAT（Personal Access Token）存在瀏覽器 `localStorage`，不需要後端：

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 勾選 `repo` + `workflow` 權限，建議 90 天有效期
3. 複製 token → 網頁右下角「設定 / 更換 GitHub Token」填入

> Token 僅存在你的瀏覽器，不會傳送到任何伺服器。

---

## 緊急 Rollback SOP

線上出問題時，< 5 分鐘止血流程：

1. 在 GitHub 建立新 Issue，套用 **Rollback** 範本
2. 填入目標 commit hash（上一個穩定版本）
3. `issue-driven-pipeline.yml` 自動觸發，執行 `git revert`
4. CI/CD 自動重新部署，GitHub Pages 約 60 秒後恢復

不需要登入伺服器，不需要手動操作。

---

## Pipeline 防護機制

- **Bot-loop 防護**：偵測到 `github-actions[bot]` 是最後 committer → 跳過整條 pipeline
- **Race condition 防護**：`concurrency` 設定確保同一 PR 只跑一個 pipeline 實例
- **Fork 安全**：只處理同 repo 的 PR，fork 來的 PR 拿不到 secrets

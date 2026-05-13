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

```
使用者送出留言
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
    └── pr-agent-pipeline.yml     # 主 Pipeline（classify→resolver→qa→merge）
```

---

## Pipeline 防護機制

- **Bot-loop 防護**：偵測到 `github-actions[bot]` 是最後 committer → 跳過整條 pipeline
- **Race condition 防護**：`concurrency` 設定確保同一 PR 只跑一個 pipeline 實例
- **Fork 安全**：只處理同 repo 的 PR，fork 來的 PR 拿不到 secrets

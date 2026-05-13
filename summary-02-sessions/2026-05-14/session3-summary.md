# Session 3 Summary — 2026-05-14

## 完成事項

### 1. IDD Pipeline PAT 修正（PR #19）
- **問題**：`issue-driven-pipeline.yml` 使用 `GITHUB_TOKEN` 建立 PR，GitHub 安全機制導致 `pr-agent-pipeline.yml` 不被觸發（Actions 不能用自己的 token 觸發其他 workflow）
- **修正**：改用 `GH_PAT` secret，並動態從 PAT 取得 git identity（`gh api user --jq .login`）
- **結果**：IDD 完整端對端流程（Issue → branch → PR → classify → resolver → QA → merge）可全自動運行

### 2. 第6章 PPTX 完整摘要（進階 GitHub 工作流程與 Claude）
- 讀取 17 張投影片，輸出完整結構化摘要
- 核心主題：緊急回退（Git Revert）、依賴安全更新（隔離分支）、每月重構（對抗技術債）
- 提取 3 項 helloWeb 現況 gap 分析並轉換為待辦任務

### 3. Dependabot 設定（PR #20）
- 新增 `.github/dependabot.yml`：每週追蹤 pip（anthropic/pytest）+ GitHub Actions 版本更新
- 新增 `requirements.txt`：讓 Dependabot pip 生態系有檔案可讀取
- 走 feature branch → pr-agent-pipeline → auto-merge 完整流程

### 4. ROLLBACK IDD 完整流程（PR #25）
- **Issue 模板**：`.github/ISSUE_TEMPLATE/rollback.yml`，結構化欄位（commit_hash / reason / confirm checkbox）
- **classify 升級**：`[ROLLBACK]` 標題快速路徑，跳過 Haiku API 直接輸出 `mode=ROLLBACK`（省 token）
- **resolver 升級**：
  - `extract_commit_hash()`：同時支援標題 inline 格式（`commit <hash>`）與 Issue template body 格式（`### 目標 commit hash\n\n<hash>`）
  - `handle_rollback()`：`git cat-file -t` 驗證 hash 存在 → `git revert --no-edit` → 衝突時 `git revert --abort` + PR comment
- **qa_agent 升級**：偵測 `MODE=ROLLBACK`，改為結構性驗證（index.html 存在 + `<html>`/`<body>` 標籤），不呼叫 Sonnet / pytest
- 走 code-writer → code-qa → code-reviewer 三 agent 流程，reviewer 發現 3 個 must-fix 全部修正

## 關鍵技術筆記

### GITHUB_TOKEN vs PAT 觸發差異
GitHub 安全機制：用 `GITHUB_TOKEN` 建立的 PR / push 不會觸發其他 workflow，用 PAT 才會。IDD pipeline 必須用 `GH_PAT` secret 才能讓 `pr-agent-pipeline` 自動啟動。

### Reviewer 發現的 extract_commit_hash Bug
Issue template body 格式為 `### 目標 commit hash\n\n<hash>`，原本 regex `r"\bcommit\s+([0-9a-f]{7,40})\b"` 無法匹配。需補加 `r"###\s*目標\s*commit\s*hash\s*\n+([0-9a-f]{7,40})"` fallback。

### git cat-file -t 驗證模式
`git cat-file -t <hash>` 回傳 commit / blob / tree 等型別，non-zero exit code 表示不存在。在 `git revert` 前必須驗證，防止對不存在的 ref 操作。

### QA ROLLBACK 模式設計
ROLLBACK 後的 QA 不應用 AI 生成測試（生成的測試對「是否真的 revert 成功」毫無驗證能力）。改為結構性驗證（HTML 標籤存在性）並 `return 0`，讓 merge job 正常執行。

## 產出檔案表格

| 檔案 | 動作 | PR | 說明 |
|------|------|----|------|
| `.github/workflows/issue-driven-pipeline.yml` | 修改 | #19 | 改用 GH_PAT，動態取得 git identity |
| `.github/dependabot.yml` | 新增 | #20 | pip + github-actions 每週掃描 |
| `requirements.txt` | 新增 | #20 | anthropic==0.40.* / pytest==8.* |
| `.github/ISSUE_TEMPLATE/rollback.yml` | 新增 | #25 | 結構化緊急回退 Issue 模板 |
| `scripts/classify_pr.py` | 修改 | #25 | ROLLBACK 快速路徑（+6 行）|
| `scripts/resolver_agent.py` | 修改 | #25 | extract_commit_hash + handle_rollback（+75 行）|
| `scripts/qa_agent.py` | 修改 | #25 | ROLLBACK 結構驗證模式（+24 行）|

## HANDOFF（下次 session 優先處理）

### 立即行動
- [ ] **Task #1**：建立 GitHub Issue（用 rollback 模板，填入任意近期 commit hash，例 `d1a2b4f`）測試 ROLLBACK 端對端流程是否全自動跑完（classify → resolver git revert → qa structural check → auto-merge）
- [ ] **Task #2**：重構 `scripts/pipeline_utils.py` 共用模組（抽出 `load_pipeline_config()` + `post_pr_comment()`，classify / resolver / qa 三腳本共用），對應第6章「每月重構衝刺」
- [ ] 建立 `rollback` label（`gh label create rollback --color "D93F0B" --description "緊急回退操作" --force --repo chenghyang2001/helloWeb`），讓 Issue 模板的 labels 欄位生效

### 進行中（需接續）
- Task #1（ROLLBACK 測試）尚未執行，因使用者在測試前直接觸發收工。Issue 模板已上線，流程邏輯已部署，缺最後一步驗證。
- Task #2（重構）已規劃但未開始，被 Task #1 阻擋。
- 第7章 PPTX（`第7章｜結論：完全自動化的工作流程.pptx`）尚未摘要，是本書最後一章。

### 注意事項
- ROLLBACK 流程的 QA 是結構性驗證（非 AI 測試），index.html 只要存在且含 `<html>`/`<body>` 就通過 QA。如果 revert 後的 index.html 格式嚴重損壞，可能誤判通過。
- `extract_commit_hash()` 優先順序：標題 inline → body inline → body template section。若使用 Issue template 填寫但標題沒補 hash，必須確認 body 裡的 `### 目標 commit hash` section 格式正確。
- Dependabot 開的 PR 屬 `feature/` branch，會走 pr-agent-pipeline → resolver 可能誤改 index.html。建議日後加 label filter 排除 dependabot PR 的 resolver 行為。

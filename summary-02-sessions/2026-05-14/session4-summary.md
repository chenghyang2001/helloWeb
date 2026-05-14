# Session 4 — aihcr-daily IDD Pipeline 部署、除錯與驗證

**日期**：2026-05-14  
**專案**：helloWeb（aihcr-daily IDD 部署）  
**Session 類型**：IDD 新 Repo 接入 + Pipeline 多輪除錯

---

## 完成事項

### 1. aihcr-daily IDD Pipeline 部署完成

- 執行 `/add-idd-to-repo`，為 `chenghyang2001/aihcr-daily` 加入 IDD AI PR Pipeline
- 新增 8 個檔案，**零覆蓋既有檔案**（遵循使用者偏好）
- 新增檔案：3 workflows + 3 Python agents + `pipeline.config.json` + `requirements.txt`
- `implementation_target` 設為 `scripts/issue_solution.py`（新 Issue 建新檔，不修改既有代碼）

### 2. resolver_agent.py 新檔創建 bug 修復（Round 3 失敗原因）

- **Bug**：`build_prompt()` 對空檔案沒有提示 Claude 如何建立新檔
- Claude 回傳 `<old>\n</old>`，但 `'\n' in ""` 為 False → 無法套用 replacement
- **Fix**：加入 `if not code:` block，要求 Claude 使用 `<old></old>`（完全空）建立新檔
- commit `14630ef`（aihcr-daily）+ `f3c5eba`（idd-template）

### 3. qa_agent.py 空 test_target bug 修復（Round 4 失敗原因）

- **Bug**：`TEST_PATH = REPO_ROOT / CONFIG["test_target"]`，`test_target = ""` 時等於 `REPO_ROOT`（目錄本身）
- `write_test_file()` 對目錄呼叫 `.write_text()` → `[Errno 21] Is a directory`
- **Fix**：`main()` 加入 early return，`test_target` 為空時改做結構性檢查並留言 PR
- commit `244574c`（aihcr-daily）+ `c81d4fc`（idd-template）
- 兩個修復均同步 push 到 `idd-template`（SHA256 一致）

### 4. GH_PAT 權限問題修復（Round 1-2 失敗原因）

- Fine-grained PAT 缺乏 GraphQL `repository.pullRequests` 存取
- 使用者換用 Classic PAT（`gho_...`）含 `repo + workflow` scope 後解決

### 5. Pipeline 全流程驗證（Round 5 + Round 6）

- Round 5（Issue #7）：第一次完整成功，Issue 自動關閉
- Round 6（Issue #9）：完整流程 classify → resolver_qa → merge，耗時 **~82 秒**
- Issue 自動關閉機制驗證：`feature/issue-N` branch regex 正確觸發 `gh issue close`

### 6. Stale PR/Issue 清理

- 手動關閉 PR #4（Round 3）、PR #6（Round 4）及 Issue #5
- 原因：失敗的 pipeline 不會觸發 merge → issue close 無法自動執行

---

## 關鍵技術筆記

### Python pathlib 陷阱

`pathlib.Path(root) / ""` 靜默回傳 `root` 本身（非錯誤）。config 系統的空字串欄位會製造隱性 bug，必須在使用前 `if not value:` guard。

### resolver SEARCH/REPLACE 新檔創建

- 新檔創建：`<old></old>`（完全空，無任何 whitespace）+ `<new>CONTENT</new>`
- Python：`"".replace("", content, 1)` 正確回傳 `content`
- 必須在 prompt 中明確告知 Claude 此格式，否則 Claude 會嘗試 `<old>\n</old>` 導致 replacement 失敗

### IDD Pipeline issue-closing 機制

- 關閉 Issue 的步驟在 `pr-agent-pipeline.yml` 的 merge job 最後
- 只有 `resolver_qa.result == 'success'` + `qa_passed == 'true'` 才會執行
- pipeline 失敗留下 stale 開放 Issue，需手動清理

### idd-template 同步紀律

- aihcr-daily 的 bug fix 必須同步 push 到 `idd-template`
- 同步方式：相同 fix 邏輯 + 驗證兩個檔案 SHA256 一致

---

## 產出檔案

| 檔案 | 狀態 | Repo |
|------|------|------|
| `.github/workflows/issue-driven-pipeline.yml` | 新增 | aihcr-daily |
| `.github/workflows/pr-agent-pipeline.yml` | 新增 | aihcr-daily |
| `.github/workflows/auto-merge-comment-pr.yml` | 新增 | aihcr-daily |
| `scripts/classify_pr.py` | 新增 | aihcr-daily |
| `scripts/resolver_agent.py` | 新增 + 修復 | aihcr-daily + idd-template |
| `scripts/qa_agent.py` | 新增 + 修復 | aihcr-daily + idd-template |
| `pipeline.config.json` | 新增 | aihcr-daily |
| `requirements.txt` | 新增 | aihcr-daily |

---

## HANDOFF（下次 session 優先處理）

### 立即行動

- [ ] 在 `spec.md`（aihcr-daily）補充實際業務規格，讓 resolver 能解決真正的 AIHCR 任務而不只是測試
- [ ] 觀察 aihcr-daily 真實 Issue 的 pipeline 表現（目前驗證都是 hello world 等級）
- [ ] 確認 idd-template 公開 README 反映最新修復（`resolver_agent.py` + `qa_agent.py` 兩個 bugfix）

### 進行中（需接續）

- aihcr-daily IDD Pipeline 已完全可用，next 是真正業務場景測試
- idd-template 兩個 bugfix 已同步（commit `c81d4fc`），但 README 尚未更新說明已知 bugfix

### 注意事項

- `test_target` 設為空字串是刻意的（aihcr-daily 用 Python 腳本但不跑 pytest），不要改回有值
- GH_PAT 必須是 Classic PAT 含 `repo + workflow` scope，Fine-grained PAT 不夠用
- Round 3/4 的 stale PR（#4/#6）與 Issue（#5）已手動關閉，不用再處理

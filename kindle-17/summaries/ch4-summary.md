# 第4章｜CI/CD 基礎入門

## 各節大綱

| # | 節名 |
|---|------|
| 1 | The Nightmare of Manual Uploads（手動上傳的噩夢） |
| 2 | The Modern Plumbing: Understanding CI/CD |
| 3 | GitHub Actions: Your Automated Assembly Line |
| 4 | Preparing the Server Connection (The Concept) |
| 5 | Instructing Your AI DevOps Engineer |
| 6 | The Magic of the Green Checkmark（綠色打勾的魔力） |
| 7 | Deploying Fearlessly（無所畏懼地部署） |
| 8 | Chapter Summary |

## 主要概念

- **告別手動 FTP 上傳**：拖錯資料夾、網路中斷 = 網站崩潰，讓開發者對部署產生心理恐懼
- **CI/CD 裝配線比喻**：
  - **CI（持續整合）** = 品管檢查點：PR 合併前自動跑測試
  - **CD（持續部署）** = 自動送貨車：Merge 到 main 後自動上線，人工零介入
- **GitHub Actions = 雲端機器人軍團**：YAML 觸發條件滿足 → 隱形機器人自動執行部署，YAML 讓 Claude 寫，你只需審閱
- **企業級安全 = GitHub Secrets 金庫**：部署金鑰加密儲存，絕不寫進程式碼

## 三步實作流程

**Step 1：取得並存入部署金鑰**

- Vercel / Netlify 取得 Deployment Token
- GitHub repo → Settings → Secrets and variables → 存入（命名如 `VERCEL_TOKEN`）

**Step 2：指示 Claude 建立 Workflow**

- 新分支 `feature/ci-cd-setup` → 喚醒 Claude
- 提示詞：「在 `.github/workflows/` 建立 YAML，觸發條件：merge 到 main，使用 `${{ secrets.VERCEL_TOKEN }}` 自動部署」

**Step 3：體驗綠色打勾的魔力**

```
你按 Merge → GitHub Actions 出現黃色旋轉圈 → 30~60 秒後變綠色打勾
→ 全球用戶看到更新版本，你沒碰任何伺服器
```

> helloWeb 這個專案正是運行在這套機制上。

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

- **運作中的應用 vs 數位資產**：有文件、自動化、可移轉 = 資產；靠創辦人記憶維持 = 脆弱的應用
- **README = 資產的門面**：潛在買家/接手開發者第一眼看到的東西，影響第一印象與估值
- **GitHub Issues = 集中管理的專案大腦**：點子散在 Trello、Apple Notes = 低效；全集中在 GitHub = 可搜尋的乾淨歷史
- **Issue-Driven Development**：每一行程式碼都連結到一個 Issue——開源專案和大型科技公司維持秩序的方法
- **程式碼註解說明「為什麼」**：`how` 已在程式碼裡，`why`（商業邏輯）才是難以重建的知識
- **Acquire.com 銷售心態**：買家買的是**可維護性**，乾淨文件 + CI/CD + Issue 歷史 → 以年營收 3-5 倍溢價快速售出

## 四步實作

**Step 1：Auto-generate 企業級 README**

- 提示詞：「擔任首席技術寫手，分析整個 codebase，生成含 Tech Stack、架構總覽、Getting Started、環境變數清單的 README.md，然後自動 commit」

**Step 2：用 GitHub Issues 管理每項任務**

- 收到 user 反饋 → 直接建 Issue（自動分配 `#N` ID），不要存在任何外部工具

**Step 3：Magic Resolution — Commit 自動關閉 Issue**

```
Commit 訊息結尾加上 "Resolves #12"
→ PR Merge 後 GitHub 自動關閉 Issue
→ 建立完美的程式碼稽核軌跡
```

> helloWeb 專案用 `Resolves #N` 實作自動關 Issue 的原理即來自此章。

**Step 4：Documentation Pass**

- 每完成一個重大功能後，讓 Claude 審閱核心檔案、加入 inline comment
- 只解釋複雜函式的**商業邏輯意圖**，不過度註解

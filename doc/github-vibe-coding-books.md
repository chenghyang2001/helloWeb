# GitHub PR Vibe Coding — 推薦書單

> 主題：使用 GitHub PR + YAML Workflow 自動化驅動 AI 實作程式碼

> 價格標示：✅ 已確認來源 ／ ～ 約略值（建議點連結確認當前 Amazon Kindle 定價）

---

## 誠實說明

你建的這套流程（使用者提 PR → YAML pipeline 觸發 → AI 讀取 PR → 自動實作 → 自動合併）
在 GitHub 2025 年稱為「Continuous AI」，目前尚無專書。
以下分兩層推薦：

---

## Layer 1：基礎 — GitHub Actions + YAML Pipeline

1. **Learning GitHub Actions** — Brent Laster (O'Reilly)
   https://www.amazon.com/Learning-GitHub-Actions-Brent-Laster-ebook/dp/B0CG2QBN3Q
   - 出版日期：2023 年 8 月
   - Kindle 定價：～ $44.99（O'Reilly 標準定價）
   - 範例程式碼：✅ https://github.com/techupskills/learning-github-actions（第 2–13 章資料夾，Apache-2.0）
   - 最完整的參考書。涵蓋 pull_request 觸發、job 依賴、secrets、check-runs。

2. **GitHub Actions in Action** — Kaufmann, Ros, de Vries (Manning)
   https://www.amazon.com/GitHub-Actions-Action-Continuous-integration-ebook/dp/B0DL7Q4J6Q
   - 出版日期：2024 年 10 月
   - Kindle 定價：✅ $41.24（折扣後，原價 $54.99，來源：Manning 官網）
   - 範例程式碼：✅ https://github.com/GitHubActionsInAction（5 個 repo，含票務 app 完整範例）
   - 最新出版。聚焦安全性、workflow 架構、可擴展 pipeline 設計。

3. **Mastering GitHub Actions** — Eric Chapman (Packt)
   https://www.amazon.com/Mastering-GitHub-Actions-automation-integration-ebook/dp/B0CW1KXWX8
   - 出版日期：2024 年 3 月 22 日
   - Kindle 定價：✅ $39.99（來源：Apple Books）
   - 範例程式碼：✅ https://github.com/PacktPublishing/Mastering-GitHub-Actions（按章分資料夾）
   - 16 章從入門到企業級，含 self-hosted runners 與監控。

4. **Automating Workflows with GitHub Actions** — Priscila Heller (Packt)
   https://www.amazon.com/Automating-Workflows-GitHub-Actions-applications-ebook/dp/B09BZVWZV2
   - 出版日期：2021 年 10 月
   - Kindle 定價：～ $35.99（Packt 舊版書標準定價）
   - 範例程式碼：✅ https://github.com/PacktPublishing/Automating-Workflows-with-GitHub-Actions
   - 適合初學者。從 YAML 語法開始，含可重用 workflow 與 marketplace actions。

5. **Hands-on GitHub Actions** — Chandrasekara & Herath (Apress)
   https://www.amazon.com/Hands-GitHub-Actions-Implement-Applications-ebook/dp/B08X675RHC
   - 出版日期：2021 年 2 月 22 日
   - Kindle 定價：～ $34.99（Apress 標準定價）
   - 範例程式碼：❌ 無（Apress 無對應公開 repo）
   - 強調跨語言生態系的 CI/CD 實作模式。

6. **DevOps with GitHub Actions** — Anthony M. Lewis (自出版)
   https://www.amazon.com/DevOps-GitHub-Actions-Automate-Pipelines-ebook/dp/B0GCM5JV9L
   - 出版日期：2024 年 12 月
   - Kindle 定價：～ $9.99–$14.99（KDP 自出版典型定價）
   - 範例程式碼：❌ 無（自出版，無伴隨 repo）
   - 涵蓋成本優化與 matrix 策略。

---

## Layer 2：AI Agent 層 — LLM + PR 自動化

7. **Vibe Coding: Building Production-Grade Software With GenAI, Chat, Agents, and Beyond**
   — Gene Kim & Steve Yegge (IT Revolution)
   https://www.amazon.com/Vibe-Coding-Building-Production-Grade-Software-ebook/dp/B0DQ5SVH4Y
   - 出版日期：2025 年 10 月 21 日
   - Kindle 定價：～ $14.99–$19.99（IT Revolution 標準；Google Play 顯示折扣版）
   - 範例程式碼：❌ 無（以作者真實專案為例，無獨立範例 repo）
   - **最推薦。** Phoenix Project 作者 + 前 Google/Amazon 30 年工程師。
   - 涵蓋 AI agent 整合到真實工程 pipeline。2026 Axiom Gold Medal 得主。

8. **AI-Assisted Coding** — Kofler, Öggl, Springer (Rheinwerk / SAP Press)
   https://www.amazon.com/AI-Assisted-Coding-Practical-Development-Rheinwerk-ebook/dp/B0DPL8FPW5
   - 出版日期：2024 年 11 月 7 日
   - Kindle 定價：✅ $44.99（來源：SAP Press 官網）
   - 範例程式碼：✅ ZIP 下載（sap-press.com 書籍補充頁，54.6 KB）
   - 涵蓋 Claude、Copilot、Aider — AI 讀程式碼並修改的工作流程。

9. **Learning GitHub Copilot** — Brent Laster (O'Reilly)
   https://www.amazon.com/Learning-GitHub-Copilot-Multiplying-Productivity-ebook/dp/B0FHSDHRFF
   - 出版日期：2025 年 7 月 10 日
   - Kindle 定價：✅ $59.99（來源：Apple Books）
   - 範例程式碼：✅ https://github.com/techupskills/learning-github-copilot
   - Copilot agent 模式自動 review PR、建議程式碼——與你的 resolver 同概念。

10. **Introduction to the Modern AI Stack: LLM, RAG, Agents, MCP, RPA, and Workflow**
    — Jerome Stack (自出版)
    https://www.amazon.com/Introduction-Modern-AI-Stack-Workflow-ebook/dp/B0GX33CDG4
    - 出版日期：2025 年（確切日期待查）
    - Kindle 定價：～ $9.99–$19.99（KDP 自出版典型定價）
    - 範例程式碼：❓ 書介提到「working Python code」，但無公開 GitHub repo
    - 涵蓋 tool calling、agent 推理、workflow orchestration 的底層架構。

---

## 總覽比較表

| # | 書名 | 出版日期 | Kindle 定價 | 定價確認 | 範例程式碼 | Repo |
|---|------|---------|------------|---------|:---------:|------|
| 1 | Learning GitHub Actions | 2023-08 | ～$44.99 | 估算 | ✅ | [techupskills/learning-github-actions](https://github.com/techupskills/learning-github-actions) |
| 2 | GitHub Actions in Action | 2024-10 | $41.24 | ✅ 確認 | ✅ | [GitHubActionsInAction](https://github.com/GitHubActionsInAction) |
| 3 | Mastering GitHub Actions | 2024-03-22 | $39.99 | ✅ 確認 | ✅ | [PacktPublishing/Mastering-GitHub-Actions](https://github.com/PacktPublishing/Mastering-GitHub-Actions) |
| 4 | Automating Workflows with GitHub Actions | 2021-10 | ～$35.99 | 估算 | ✅ | [PacktPublishing/Automating-Workflows-with-GitHub-Actions](https://github.com/PacktPublishing/Automating-Workflows-with-GitHub-Actions) |
| 5 | Hands-on GitHub Actions | 2021-02-22 | ～$34.99 | 估算 | ❌ | — |
| 6 | DevOps with GitHub Actions | 2024-12 | ～$9.99–$14.99 | 估算 | ❌ | — |
| 7 | Vibe Coding (Gene Kim) | 2025-10-21 | ～$14.99–$19.99 | 估算 | ❌ | — |
| 8 | AI-Assisted Coding | 2024-11-07 | $44.99 | ✅ 確認 | ✅ | ZIP（SAP Press 官網下載） |
| 9 | Learning GitHub Copilot | 2025-07-10 | $59.99 | ✅ 確認 | ✅ | [techupskills/learning-github-copilot](https://github.com/techupskills/learning-github-copilot) |
| 10 | Introduction to the Modern AI Stack | 2025 | ～$9.99–$19.99 | 估算 | ❓ | 書介提到 working Python code，無公開 repo |

---

## 建議閱讀順序

```
書 1 → Learning GitHub Actions      (學 YAML / triggers)
書 2 → GitHub Actions in Action     (安全性 & 架構)
書 7 → Vibe Coding by Gene Kim      (AI agent 整合)
書 8 → AI-Assisted Coding           (LLM 改程式碼模式)
```

書 3–6、9–10 按需查閱。

---

_建立日期：2026-05-08 ／ 更新：2026-05-08（加入出版日期 & 定價 & 範例程式碼 repo）_

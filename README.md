# Copilot Agent Lab

依「Coding with agent」筆記建置的 GitHub Copilot app 實驗專案。

## 結構
```
copilot-agent-lab/
├─ AGENTS.md                         專案指示（house rules，名字：哈哈）
├─ articles.json                     文章紀錄（由 save-article 寫入）
├─ viewer.html                       瀏覽 articles.json 的網頁
└─ .github/
   ├─ agents/
   │  └─ youtube-researcher.agent.md 自訂 Agent
   └─ skills/
      ├─ save-article/               自訂 Skill：存文章到 JSON
      ├─ qa-workflow/                範本 Skill：lint + 單元 + E2E
      ├─ scaffold-feature/           範本 Skill：Next.js 功能模組
      ├─ firestore-rules/            範本 Skill：Firestore 規則
      └─ pr-preflight/               範本 Skill：PR 提交前檢查
```

## 使用步驟
1. 開啟 GitHub Copilot app → 新增專案 → 開啟這個資料夾。
2. **必須先 `git init`**（Terminal 或 Git Bash），否則 `/agent` 找不到自訂 agent。
3. **開新的 Session**（Agent 與 Session 綁定，舊 Session 看不到新 agent）。
4. 測試指示：問「你叫甚麼名字？」→ 應回答「哈哈」。
5. 測試 Skill：貼上文章網址 + 截圖 → 應寫入 `articles.json`。
6. 測試 Agent：輸入 `/agent` 選 `youtube-researcher` → 「請幫我搜尋影片」。
7. 瀏覽文章：用瀏覽器開啟 `viewer.html`（若沒自動載入，按畫面上的選檔鈕選 `articles.json`）。

## 備註
- `qa-workflow`、`scaffold-feature`、`firestore-rules` 針對 Next.js + Firebase 專案，本專案不適用時可刪除。
- Skill 給所有 Agent 共用；只屬於單一 Agent 的內容請寫在該 `.agent.md`，避免浪費 context。

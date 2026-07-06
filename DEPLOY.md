# 食品營養標示分析系統 — 部署資訊

## 基本資料

- **系統類型**：HTML 單檔工具（類型 A）
- **部署平台**：GitHub Pages（⏸️ 暫不遷移 Firebase Hosting，2026-07-06 小關決定）
- **線上網址**：https://jacky5453-beep.github.io/nutrition-system/
- **GitHub Repo**：https://github.com/jacky5453-beep/nutrition-system（🌍 Public）
- **Firebase 專案**：derlife-audit（Google 登入 + 白名單）
- **Firestore Collections**：`nutrition-whitelist`（帳號白名單，doc id = email）
- **Supabase 專案**：`btnyditozvaqcxthomjk`（資料本體：`nutrition_db` 原物料／`trans_db` 翻譯詞庫／`expand_db` 展開庫／`product_history` 產品歷史記錄；2026-07-05 起 RLS 收緊，只認 Firebase idToken）
- **最後部署日期**：2026-07-06（成分排序新增「英文版比例匯出」：成分名查翻譯詞庫（含展開型基本名稱後備）、品名走 Google 翻譯、缺譯保留中文並 toast 提醒補詞庫；表頭 No./Ingredient/Percentage (%)。commit 0a47f2b）
- **前次部署**：2026-07-06（成分排序新增「匯出比例」功能——外銷用：複製文字與匯出 Excel 都只含排序＋成分名稱＋百分比，不含克數。commit 865d1da）
- **前次部署**：2026-07-06（修正 RLS 收緊後「歷史記錄消失」bug：頁面開啟瞬間未登入就抓 Supabase，被 RLS 擋拿到空陣列、還把 localStorage 備援洗掉。修法＝所有雲端讀取等 Firebase 登入狀態確定才執行、未登入直接用本地備援不覆寫，登入完成後自動清快取重新 render。commit a3467eb）
- **前次部署**：2026-07-05（Supabase 綁 Firebase idToken：sbFetch 登入後帶 idToken，配合 RLS 收緊。commit 898afea）
- **前次部署**：2026-04-15

## 部署指令

```bash
cd "/Users/jacky/Desktop/claude/claude code/食品營養標示分析系統"
git add -A && git commit -m "描述" && git push origin main
# GitHub Pages 自動部署（來源：main 分支 / 根目錄），約 1～2 分鐘生效
```

## 資料庫

- **Supabase**（主要）：`https://btnyditozvaqcxthomjk.supabase.co`
  - 原物料資料庫、翻譯詞庫、展開庫、產品歷史記錄 雲端同步
  - ⚠️ 2026-07-05 起 RLS 收緊：匿名（anon key）SELECT 一律回空陣列，讀寫都要 Firebase 登入 idToken（Third-Party Auth 認 derlife-audit）
- **localStorage**（備援）：未登入或 Supabase 連線失敗時自動降級，只讀不覆寫

## 環境變數 / Secrets

無（翻譯用 API Key 由使用者在前端輸入，存於 localStorage）

## 測試方式

1. 開 https://jacky5453-beep.github.io/nutrition-system/
2. 用 Google 登入（白名單帳號，admin = jacky5453@gmail.com）
3. 切到「📦 產品歷史記錄」分頁，預期看到「共 12 筆」（咔脆G腿、清香餛飩、栗粒粽…）
4. 其他分頁（原物料資料庫／翻譯詞庫／原料展開庫）也應正常顯示雲端資料

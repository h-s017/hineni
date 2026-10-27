# 旗袍合作｜2026 年 12 月、2027 年 1 月線上時段投票

## 已部署的獨立投票頁

https://ihmvziqisputjnjkuhvm.supabase.co/functions/v1/qipao-availability-2026-2027

- 官網 `hineni.hanascent.com` 不變；程式存放於 GitHub `internal/qipao-availability-2026-2027` 分支，不合併 `main`。
- 獨立網址由現有 **hana-ai-office** Supabase 專案的 Edge Function `qipao-availability-2026-2027` 提供。
- 不加入官網導覽、不設定搜尋引擎索引（`X-Robots-Tag: noindex, nofollow`），但網址可由任何拿到連結的人開啟，因此**不是登入限制的私人網站**。
- 同個瀏覽器以隨機 UUID 更新自己的既有票；換瀏覽器可能算另一位使用者。
- 每日「上午 10:00–14:00／下午 14:00–18:00」複選，週日為每週第一天。
- 全體可見每時段累積票數；姓名和各人的選擇僅在使用私下管理碼時顯示。
- 統籌者可匯出包含姓名的 CSV，**切勿公開管理碼或姓名 CSV**。
- 匿名投票不具嚴格身分驗證，適合小型內部協調，不宜用於需要防灌票的正式票選。

## 原始碼與部署

- `internal-tools/qipao-availability-poll.html`：網頁原始碼（線上版本）。
- `internal-tools/qipao-poll-edge-function.ts`：完整已部署的 Edge Function 來源（內嵌同一 HTML）。
- 資料表：`public.qipao_availability_votes`（RLS 啟用，前端無資料表直接讀取權限）。
- 公開 RPC：`qipao_availability_submit`、`qipao_availability_mine`、`qipao_availability_summary`。
- 保護 RPC：`qipao_availability_admin`，必須提供不記入版本庫的管理碼。
- 從瀏覽器發送投票到 Supabase Data API；不需 LINE 回傳投票碼，也不需建立新付費專案。

## 後續修改

若要改日期、時段或表單樣式，需一起更新 GitHub HTML、Edge Function 源碼與必要的資料庫限制，再重新部署。**不要將此分支合併到官網 `main`，避免改動正式站。**

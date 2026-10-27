# 旗袍合作｜2026 年 12 月、2027 年 1 月線上時段投票

## 現況（2026-10-27）

- 投票原始網頁：`internal-tools/qipao-availability-poll.html`。
- Supabase 資料庫提供跨裝置的投票與統計服務。
- **Supabase Edge Functions 不能直接託管 HTML。** 原先網址會顯示原始碼，已修正為 HTTP 302 暫時導向 GitHub 原始檔的網頁預覽 CDN。
- 暫時預覽： https://rawcdn.githack.com/h-s017/hineni/68563e3552afd5378cd595ddd77672ccbe223f15/internal-tools/qipao-availability-poll.html
- 暫時轉址： https://ihmvziqisputjnjkuhvm.supabase.co/functions/v1/qipao-availability-2026-2027
- 第三方預覽 CDN 在瀏覽器首次開啟 HTML 可能要求確認；**此方案不作正式發送用**。正式建議改用獨立的 Vercel 靜態網頁網站。
- `internal-tools/vercel.json` 已準備網站根目錄改寫與 noindex 標頭；Vercel 部署時選此 repo、**分支 `internal/qipao-availability-2026-2027`**、專案根目錄 `internal-tools`、Other framework。
- 官網 `hineni.hanascent.com`、其 `main` 分支與導覽均不更動。

## 投票規格

- 2026/12/01 至 2027/01/31，週日為每週第一日。
- 上午 10:00–14:00／下午 14:00–18:00。
- 無須登入，但填寫姓名後才可提交多個時段；相同瀏覽器的識別碼可更新投票。
- 所有人可見各時段總票數；姓名及個別選擇只有輸入統籌者管理碼後才能看到。
- 管理碼不得進版控。統籌者可匯出 CSV。
- 因為未要求身份驗證，**網址不是私人存取控制**，適合內部小組協調而非正式身分驗證／防重複投票用途。

## Supabase

- 使用既有 HANA AI OFFICE Supabase 專案，**不新增付費專案**。
- 資料表 `public.qipao_availability_votes` 啟用 RLS，匿名使用者不可直接讀取資料表。
- `qipao_availability_submit` 提交、`qipao_availability_mine` 個人讀取、`qipao_availability_summary` 聚合統計、`qipao_availability_admin` 管理查詢。
- `internal-tools/qipao-poll-edge-function.ts` 為首版錯誤 HTML 回應的歷史原始碼，**不要重新部署該檔案**；現行 Edge Function 已替換為純 HTTP 302 轉址。

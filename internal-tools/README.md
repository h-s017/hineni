# 旗袍合作｜2026 年 12 月、2027 年 1 月時段投票

## 正式投票網址

**https://qipao-availability-2026-2027.vercel.app/**

- Vercel 專案：`qipao-availability-2026-2027`（獨立專案）
- 網頁使用 `internal-tools/qipao-availability-poll.html` 的原始碼，已單獨部署到 Vercel 的 Production 環境。
- **不修改、不嵌入、不在導覽列連結 `hineni.hanascent.com` 官網。**
- 在 GitHub `hineni` 的 `internal/qipao-availability-2026-2027` 分支保留程式碼，不合併到 `main`。
- 網址可由任何收到連結的人開啟，已關閉 Vercel 登入保護；只是不列入官網，**不等於私人網站**。
- 不須再透過第三方預覽 CDN。舊 Supabase Edge Function 網址目前以 302 轉址到正式 Vercel 網頁。
- 目前 **Vercel 採 API 單檔部署，未啟用 GitHub 自動同步**。將來 GitHub 變更網頁後，仍須重新部署。

## 投票功能

- 日期：2026/12/01 – 2027/01/31
- 週曆第一天：星期日
- 時段：上午 10:00–14:00／下午 14:00–18:00
- 參與者填姓名或暱稱，勾選多個時段，直接提交至 Supabase 共用資料庫
- 同一瀏覽器以本機隨機 UUID 更新其投票；其他裝置可能被算為另一位投票者
- 所有參與者可查看各半日時段票數，不開放查看個別姓名
- 統籌者管理碼僅提供給統籌者，用於檢視名單與匯出 CSV；管理碼不寫入公開程式碼

## 技術架構

- 前端：Vercel 靜態 HTML，含 UTF-8 字元集
- 雲端資料庫：現有 Supabase `hana-ai-office` 專案
- 後端資料表：`public.qipao_availability_votes`，RLS 啟用且匿名角色不具表的直接 SELECT 權限
- RPC：`qipao_availability_submit`、`qipao_availability_mine`、`qipao_availability_summary`、`qipao_availability_admin`
- 原 Edge Function `qipao-availability-2026-2027` 僅作舊連結重新導向，**不得再拿來直接提供 HTML**。
- `internal-tools/qipao-poll-edge-function.ts` 是首次嘗試的歷史檔，非目前部署中的程式。

## 隱私限制

不採帳號登入，因此並非嚴格一人一票。連結持有者可匿名投票，管理碼請勿流出群組。不要將管理碼或含姓名的匯出檔公開分享。

# garmin-dashboard-fallback

`pc0620022002/garmin-dashboard` 的離線備援版,部署在 GitHub Pages,Railway 掛時可用。

## URL

https://pc0620022002.github.io/garmin-dashboard-fallback/

## 運作方式

- 每天 22:30 台灣時間,GHA workflow 從私有 repo `garmin-dashboard` 的 `cache` 分支拉 7 個 JSON commit 進來
- GitHub Pages 從 `main` 分支 root 部署 `index.html`,前端直接 `fetch` 同目錄的 JSON
- 完全不依賴 Railway,Railway outage 時也能讀資料

## 與 Railway 主站差別

| 功能 | Railway 主站 | 此 fallback |
|---|---|---|
| 看圖表 / 表格 | ✅ | ✅ |
| 手動 refresh(打 Garmin) | ✅ | ❌(沒 server) |
| 手動編輯配速 / 隱藏紀錄 | ✅ | ❌(唯讀) |
| 管理員模式 | ✅ | ❌ |
| 資料新鮮度 | 即時(每天 22:00 自動 + 隨時可手動觸發) | 每天 22:30 同步一次 |

## 需要的 secret

`PRIVATE_REPO_TOKEN` — fine-grained PAT,scope: `pc0620022002/garmin-dashboard` 的 `Contents: Read`。

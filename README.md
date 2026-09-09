# Pondahai 個人網站

一個結合「數位分身」與「個人品牌」的 GitHub Pages 網站。

## 專案總覽

本網站包含以下主要區塊：

| 區塊 | 說明 |
|------|------|
| **🎯 作品集** | 技術專案展示區 |
| **🛠️ 個人作品集** | 個人業餘專案 |
| **📄 學術履歷** | 博士候選人學經歷 |
| **📰 每日回顧報** | 歷史上的今天（自動從數位分身知識庫生成）|

## 📰 每日回顧報（重點功能）

由 OpenClaw 回顧數位分身的知識庫，自動產生並更新到位於 GitHub Pages 的網頁。

### 功能
- **每日自動更新**：Cron 每天 9:00 自動產生
- **歷史上的今天**：根據當天月/日，從知識庫提取過去年份的紀錄
- **AI 改寫**：使用本地 LLM `gemma4:12b` 將原始素材改寫成自然口語（早期曾用 `qwen3.5:9b`）
- **多元內容**：支援 FB 貼文、AI 圖片分析、外部連結摘要等
- **時間顯示**：超過 1 年顯示「X年前」

### 資料來源（位於本機 OpenClaw 工作區）

> 以下資料夾位於 `~/.openclaw/workspace/`，不在 GitHub repo 中

1. `memory/YYYY-MM-DD.md` - 日常筆記
2. `cerebras-kb-chat/knowledge/**` - 數位分身知識庫（FB/部落格記錄，約 20,000+ 筆）

### 更新流程
1. 掃描當天月/日的歷史紀錄（從知識庫）
2. 擷取段落級內容（不是只有標題）
3. 透過本地 LLM `gemma4:12b` 改寫成 FB 回顧文風
4. 寫入 `js/daily-data.js`
5. 自動推送到 GitHub Pages

### 相關檔案
- **生成腳本**：`scripts/generate_dahai_daily.js`（位於本機 OpenClaw 工作區）
- **資料檔**：`js/daily-data.js`
- **前端**：`index.html`

## 🔧 技術架構

```
dahai/                    # 本 repo 根目錄
├── index.html            # 主頁面
├── css/                  # 樣式
├── js/
│   ├── daily-data.js     # 每日回顧資料
│   └── archive/          # 年度歸檔（按需載入）
├── images/               # 圖片
└── README.md             # 本說明檔
```

## 📝 相關腳本（位於本機 OpenClaw 工作區）

> 以下腳本位於 `~/.openclaw/workspace/scripts/`，不在 GitHub repo 中

| 腳本 | 功能 |
|------|------|
| `generate_dahai_daily.js` | 每日回顧報生成器（Cron 自動執行） |
| `enrich_digital_twin_links.js` | 數位分身連結補摘要腳本 |

## 🖥️ 維運筆記（生成機器）

> 內容由**另一台機器**每天自動生成後 push，本 repo 只存成品。以下是從 git history 反推的側寫，供日後指認。

| 項目 | 內容 |
|------|------|
| Commit 身分 | `Pondahai <pondahai@github.com>`（腳本專用的手動設定信箱，非 GitHub noreply，也非個人 gmail） |
| 時區 | 全部 `+0800`，無例外 |
| 排程時間 | 每天 09:00 觸發，實際落地約 09:03 |
| 啟用日 | 2026-02-27（當天 15:04–15:31 有 8 筆調試 commit，標題仍是未整理的時間格式） |
| 可用度 | 194 天中僅缺 **2026-04-06**、**2026-08-21** 兩日 —— 該機器唯二離線的日子 |
| 腳本位置 | 該機器的 `~/.openclaw/workspace/scripts/generate_dahai_daily.js` |

**若忘記是哪台**，在候選機器上執行：

```bash
crontab -l 2>/dev/null | grep -i dahai; ls -la ~/.openclaw/workspace/scripts/
```

有輸出的即是。註：資料檔中不含任何路徑、主機名或內網 IP，無法從 repo 內容判斷。

## 網址

- 主站：https://pondahai.github.io/
- 每日回顧：https://pondahai.github.io/dahai/

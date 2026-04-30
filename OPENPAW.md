# 🐾 OpenPaw — My Pet Anywhere

基於 [OpenAB](https://github.com/openabdev/openab) 的寵物產業 AI 助手架構。

Fork → Config → Deploy — 讓你的寵物品牌擁有自己的 AI 助手。

---

## 什麼是 OpenPaw

OpenPaw 是一個基於 OpenAB 的垂直領域應用，專為寵物產業設計。它提供：

- **寵物照護 AI 問答** — 飼主在 LINE/Discord 直接問 AI，搜尋獸醫資源回答
- **每日推播** — 天氣提醒 + 寵物照護知識（cronjob 排程）
- **多平台** — LINE（消費者）+ Discord（社群）同一套架構
- **可定制 Persona** — 改 CLAUDE.md 就能換品牌語氣

## 金金 — 第一隻 OpenPaw 寵物 AI

金金是一隻黃金獵犬 AI 助手，作為 OpenPaw 的參考實作：
- 寵物健康 Q&A（飲食安全、行為異常、日常照護）
- 找附近獸醫院、寵物活動
- 每日早安（天氣 + 寵物照護提醒）
- 週末寵物活動推薦

## 目錄結構

```
OpenPaw/
├── OPENPAW.md              ← 你正在看的文件
├── agents/
│   └── jin-jin/
│       └── CLAUDE.md       ← 金金的人格設定
├── configs/
│   ├── jin-jin.toml        ← agent config（平台 + AI 後端）
│   └── cronjob.toml        ← 排程設定（早安/晚安/週末）
└── (OpenAB 原始檔案)        ← fork 自 openabdev/openab
```

## 快速開始

### 1. Clone

```bash
git clone https://github.com/BlakeHung/openab.git OpenPaw
cd OpenPaw
```

### 2. Config

修改 3 個檔案：

**`configs/jin-jin.toml`** — 填入你的平台 token 和頻道 ID
```toml
[discord]
bot_token = "${DISCORD_BOT_TOKEN}"
allowed_channels = ["你的頻道ID"]

[agent]
command = "claude"
args = ["code", "--trust-all-tools"]
working_dir = "/path/to/OpenPaw/agents/jin-jin"
```

**`configs/cronjob.toml`** — 填入目標頻道 ID
```toml
[[jobs]]
schedule = "0 8 * * *"
channel = "你的頻道ID"
timezone = "Asia/Taipei"
```

**`agents/jin-jin/CLAUDE.md`** — 自定義 AI 人格（或直接用金金的設定）

### 3. Run

```bash
# 用 config flag 指定設定檔
cargo run -- --config configs/jin-jin.toml
```

或 Docker：
```bash
docker compose up -d
```

## 自定義你的寵物 AI

想做自己品牌的寵物 AI？

1. 複製 `agents/jin-jin/` 為 `agents/your-pet/`
2. 修改 `CLAUDE.md` — 換品牌名、語氣、專業領域
3. 複製 `configs/jin-jin.toml` 為 `configs/your-pet.toml`
4. 修改 `working_dir` 指向你的 agent 目錄
5. 搞定

## 技術底層

- **OpenAB** v0.8.2 — Rust，開源 AI Agent Broker
- **平台** — LINE / Discord / Telegram / Slack
- **AI 後端** — Claude Code / Kiro / Gemini / OpenCode+Ollama
- **排程** — Cronjob with hot-reload（改 cronjob.toml 自動生效）
- **部署** — Docker / K8s / Helm

## 行銷頁面

[wchung.tw/OpenPaw](https://wchung.tw/OpenPaw/)

## 聯絡

- Blake Hung — blake@wchung.tw
- GitHub: [BlakeHung](https://github.com/BlakeHung)
- 素材授權：小金毛 咘咘BuBu [@goldenbubu0504](https://www.threads.com/@goldenbubu0504)

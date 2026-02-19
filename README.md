# 📕 OpenClaw XHS Skill

> Xiaohongshu (Little Red Book) automation for [OpenClaw](https://openclaw.ai) — trending topics, AI content generation, and auto-publishing via Telegram/Discord.

小红书自动化技能 — 通过 Telegram / Discord 控制：爬取热点、AI 生成图文、一键发布。

## Features

- **Trending** — Scrape trending topics from Xiaohongshu explore page
- **AI Content** — Generate copywriting (Claude) + images (Gemini) tailored for XHS style
- **Auto Publish** — Upload images, fill title/content/topics, click publish — fully automated
- **Full Pipeline** — Trending → Generate → Preview → Publish in one command

## Requirements

- macOS or Linux
- [OpenClaw](https://openclaw.ai) installed and configured
- [uv](https://docs.astral.sh/uv/) (Python package manager)
- Google Chrome
- [OpenRouter](https://openrouter.ai) API key (for AI image generation)

## Install

```bash
git clone https://github.com/pearl799/openclaw-skill-xhs.git
cd openclaw-skill-xhs
./install.sh
```

The installer will:
1. Copy the skill to `~/.openclaw/skills/xhs/`
2. Install Python dependencies
3. Configure `openclaw.json` (prompts for your API key)

After installation, login to XHS (one-time QR scan):
```bash
cd ~/.openclaw/skills/xhs/xhs-toolkit && \
uv run python ~/.openclaw/skills/xhs/scripts/xhs_login_persistent.py
```

Then restart the gateway:
```bash
openclaw gateway --force
```

## Usage (Telegram / Discord)

| Command | What it does |
|---------|-------------|
| 小红书热点 | Fetch trending topics |
| 帮我生成一篇关于AI的小红书 | Generate content + images |
| 发布 | Publish the generated content |
| 小红书登录状态 | Check login status |
| 全自动发布 | Full pipeline: trending → generate → publish |

## Configuration

All settings are in `~/.openclaw/openclaw.json` under `skills.entries.xhs.env`:

| Variable | Required | Description |
|----------|----------|-------------|
| `IMAGE_API_KEY` | Yes | OpenRouter API key for image generation |
| `IMAGE_MODEL` | No | Default: `google/gemini-3-pro-image-preview` |
| `XHS_TOOLKIT_DIR` | Auto | Set by installer |
| `XHS_COOKIES_FILE` | Auto | Set by installer |
| `OPENCLAW_GATEWAY_TOKEN` | Auto | Detected from gateway config |

## Uninstall

```bash
cd openclaw-skill-xhs
./uninstall.sh
```

## Troubleshooting

**QR code login required every time**
- Make sure `XHS_CHROME_PROFILE` points to a persistent directory
- Kill any stale Chrome processes: `pkill -f chrome-data`

**Publishing fails**
- Check login status first: tell the bot "小红书登录状态"
- If expired, re-login: run `xhs_login_persistent.py`

**Image generation fails**
- Verify your OpenRouter API key is valid
- The API is intermittent — the script retries up to 3 times automatically

**Chrome won't start**
- Kill stale processes: `pkill -f chrome-data`
- Verify Chrome path: `ls "/Applications/Google Chrome.app/"` (macOS)

## License

MIT

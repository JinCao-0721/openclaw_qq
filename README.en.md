# OpenClaw QQ Plugin (OneBot v11)

> 中文版: [README.md](./README.md)

## 📚 Docs Hub

- [Docs Home](./docs/index.en.md)
- [3-minute Quickstart](./docs/quickstart.en.md)
- [Config Reference (Grouped)](./docs/config-reference.en.md)
- [Advanced Features & Full Parameters](./docs/advanced.en.md)
- [NapCat Deployment Guide](./deploy/napcat/README.en.md)

## 📢 Official Support Channel (Primary)

**Designated forum for this plugin:**

**https://aiya.de5.net/c/25-category/25**

- We do not run a QQ support group.
- All questions and feedback are centralized on the forum for long-term searchability.

## What This Plugin Does

Provides OneBot v11 QQ channel integration for OpenClaw:

- Direct and group message handling
- Group @mention trigger control
- Multimodal support (image/voice/file depending on your OneBot server)
- Production-oriented reliability features (reconnect/retry/fallback)

## 3-minute Quickstart

### 1. Prerequisites

- OpenClaw is installed and running
- A OneBot v11 server is running (NapCat/Lagrange recommended)
- `message_post_format=array` in OneBot config

### 2. Install

```bash
cd openclaw/extensions
git clone https://github.com/constansino/openclaw_qq.git qq
cd ../..
pnpm install && pnpm build
```

### 3. Minimal Config

Edit `~/.openclaw/openclaw.json`:

```json
{
  "channels": {
    "qq": {
      "wsUrl": "ws://127.0.0.1:3001",
      "accessToken": "your_token",
      "requireMention": true
    }
  },
  "plugins": {
    "entries": {
      "qq": { "enabled": true }
    }
  }
}
```

### 4. Start & Verify

```bash
openclaw gateway restart
```

Check:

- Bot replies in DM
- Bot replies when @mentioned in groups
- No persistent auth/reconnect errors in logs

## Suggested Reading Order

1. [Quickstart](./docs/quickstart.en.md)
2. [Config Reference](./docs/config-reference.en.md)
3. [Advanced Features](./docs/advanced.en.md)
4. [Deployment Guide](./deploy/napcat/README.en.md)

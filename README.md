# OpenClaw QQ 插件 (OneBot v11)

> English: [README.en.md](./README.en.md)

## 📚 文档中心

- [文档主页](./docs/index.md)
- [3 分钟快速开始](./docs/quickstart.md)
- [配置参考（分组版）](./docs/config-reference.md)
- [高级能力与完整参数](./docs/advanced.md)
- [NapCat 部署说明](./deploy/napcat/README.md)

## 📢 官方交流方式（唯一）

**本插件指定交流地点：**

**https://aiya.de5.net/c/25-category/25**

- 不建立 QQ 群，统一在论坛交流与反馈。
- 论坛更适合问题沉淀、检索和版本追踪。

## 这个插件解决什么问题

为 OpenClaw 提供 OneBot v11 的 QQ 渠道接入能力：

- 私聊与群聊消息收发
- 群聊 @ 触发控制
- 多媒体消息支持（图/语音/文件，取决于服务端能力）
- 生产向稳定性能力（重连、重试、失败兜底等）

## 3 分钟快速开始

### 1. 前置条件

- 已安装并运行 OpenClaw
- 已运行 OneBot v11 服务端（推荐 NapCat / Lagrange）
- OneBot 配置里 `message_post_format=array`

### 2. 安装

```bash
cd openclaw/extensions
git clone https://github.com/constansino/openclaw_qq.git qq
cd ../..
pnpm install && pnpm build
```

### 3. 最小配置

编辑 `~/.openclaw/openclaw.json`：

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

### 4. 启动与验证

```bash
openclaw gateway restart
```

检查：

- 私聊机器人有回复
- 群聊 @ 机器人有回复
- 日志无持续鉴权/重连错误

## 推荐阅读路径

1. [快速开始](./docs/quickstart.md)
2. [配置参考（分组）](./docs/config-reference.md)
3. [高级能力与完整参数](./docs/advanced.md)
4. [部署说明](./deploy/napcat/README.md)

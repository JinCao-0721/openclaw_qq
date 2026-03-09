# 提案：完善 file:// 入站图片与语音附件提示

对应 Issue: #23

Refs #23

## 说明
- 这是一个正式评审用 PR。
- 当前 PR 先以独立方案文档与最小变更承载评审，供团队决定是否继续沿本分支补正式实现。

## 目标
- 改善入站 `file://` 图片、语音、文件消息对 AI 的可见性。
- 让模型至少能明确知道“有本地媒体附件”，而不是只看到 `[图片]` / `[语音消息]`。

## 本 PR 的边界
- 只处理 ingress：消息进来时如何构造上下文。
- 不改 outbound 发送，不处理截图发不出去，不处理 transport 或 session。

## 拟议改动
1. `extractImageUrls(...)`
   - 接受 `file://` 图片地址
2. `cleanCQCodes(...)` / `summarizeOneBotSegments(...)`
   - 对本地图片与语音附件生成更明确的文本提示
3. `<attachments>` 系统块
   - 增加 `qq_image url=...`
   - 增加 `qq_audio url=...`
   - 对 `file` 段统一补附件信息
4. 入站 message segment 解析
   - 在不强依赖本地文件可直接读取的前提下，优先把附件 URL 暴露给模型

## 不在本 PR 范围
- #26 的截图/本地媒体发送链路
- 自定义 wxid/chatroom target 的 routing 兼容

## 验收标准
- 收到 `file://` 图片时，模型上下文可看到真实附件提示
- 收到无文本语音时，模型上下文仍能看到音频附件存在

## 相关 issue
- #23
- #26
- #7
- #13


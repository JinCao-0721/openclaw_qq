# 提案：向 AI 透传 sender.role 群角色信息

对应 Issue: #29

Refs #29

## 说明
- 这是一个正式评审用 PR。
- 当前 PR 先以独立方案文档与最小变更承载评审，供团队决定是否继续沿本分支补正式实现。

## 目标
- 把群内协议角色 `sender.role` 透传给 AI。
- 明确区分“群内角色”和“本地配置里的 admins 权限”。

## 本 PR 的边界
- 只改隐藏 `<qq_context>` 元数据块。
- 不顺手改 `MessageSid`、会话标签、routing。

## 拟议改动
1. `buildQQHiddenMetaBlock(...)`
   - 新增 `senderRole=owner|admin|member|unknown`
2. 兼容回退
   - 缺失 role 时统一回落为 `unknown`
3. 可选扩展（后续再决定）
   - `senderTitle`
   - `senderLevel`

## 不在本 PR 范围
- #30 的 `MessageSid`
- #31 的 `ConversationLabel`
- #33 的 runtime tools

## 验收标准
- 群消息中 AI 能区分 owner/admin/member
- 私聊或缺失字段时行为稳定

## 相关 issue
- #29
- #30
- #33
- #35


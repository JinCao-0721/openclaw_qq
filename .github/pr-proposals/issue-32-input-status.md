# 提案：优先使用 NapCat set_input_status 显示输入中

对应 Issue: #32

Refs #32

## 说明
- 这是一个正式评审用 PR。
- 当前 PR 先以独立方案文档与最小变更承载评审，供团队决定是否继续沿本分支补正式实现。

## 目标
- 优先使用 NapCat 的 `set_input_status` 作为“输入中”状态。
- 保留对非 NapCat / 不支持实现的安全 fallback。

## 本 PR 的边界
- 只改 processing / typing indicator 机制。
- 不改 transport、session、正文 dispatch、runtime tools。

## 拟议改动
1. `src/client.ts`
   - 增加 `setInputStatus(...)` API 封装
2. `src/channel.ts`
   - processing 状态优先调用 `set_input_status`
   - 不支持时再回退到 `setGroupTypingCard(...)`
3. capability cache
   - 按账号缓存是否支持原生 typing
4. fallback 细化
   - 恢复逻辑不再依赖固定 `"输入中"` 假设

## 不在本 PR 范围
- #17 的 transport 抽象
- #22 的 routing / session 问题
- #33 的 AI 工具暴露

## 验收标准
- NapCat 下优先出现原生输入状态
- 非 NapCat 下可自动 fallback
- 自定义 `processingStatusText` 不再导致恢复异常

## 相关 issue
- #32


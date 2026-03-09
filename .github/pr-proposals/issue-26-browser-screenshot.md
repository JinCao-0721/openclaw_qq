# 提案：增强 agent browser 截图发送链路

对应 Issue: #26

Refs #26

## 说明
- 这是一个正式评审用 PR。
- 当前 PR 先以独立方案文档与最小变更承载评审，供团队决定是否继续沿本分支补正式实现。

## 目标
- 提高本地截图、尤其是 agent browser 生成截图的发送成功率。
- 把发送前的路径识别、文件存在性检查、fallback 顺序标准化。

## 本 PR 的边界
- 只改 outbound 本地图片/文件发送链路。
- 不改 ingress 媒体提示、不改 transport、不改 routing。

## 拟议改动
1. 发送前路径归一化
   - 统一走 `toLocalPathIfAny(...)`
   - 补文件存在性与扩展名检查
2. 图片优先发送策略
   - 本地截图优先走 `base64://` 图片发送
   - 失败后再尝试共享目录 staging
   - 群场景再尝试 `upload_group_file` fallback
3. 错误分类
   - 区分“文件不存在 / 文件可读但 rich media 失败 / staging 失败 / OneBot 拒收”
4. 日志与诊断
   - 让 browser 截图问题能明确定位到失败阶段

## 不在本 PR 范围
- #23 的入站附件提示
- #17 的 HTTP transport
- 上游 message tool 历史兼容问题之外的核心改动

## 验收标准
- browser 生成的本地 PNG/JPG 可稳定发出
- 含空格、中文文件名的截图不再轻易失败
- 群聊与私聊路径都可工作

## 相关 issue
- #26
- #13
- #7


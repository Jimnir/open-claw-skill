---
name: qq-multi-agent-router
description: QQ Bot multi-agent router: route messages to code/interview/encyclopedia agents by keyword.
read_when:
  - 用户通过 QQ 渠道发消息给你，且消息内容匹配某个 Agent 关键词
---

# QQ Multi-Agent Router

当用户通过 QQ（私聊或群聊）发送消息时，检查消息内容是否匹配路由关键词。

如果匹配，用 `sessions_send(agentId="<目标Agent>", message=<用户消息>)` 转发任务给目标 Agent，然后把 Agent 的回复作为你的输出返回。

## 路由规则

| 关键词（开头匹配） | 目标 Agent | 说明 |
|------------------|-----------|------|
| `写代码`、`编程`、`代码` | `coder`（代码助手） | 编程任务 |
| `面试`、`模拟面试` | `interviewer`（面试官） | 模拟面试 |
| `查`、`百科`、`查一下` | `encyclopedia`（百科全书） | 查资料 |
| 以上均不匹配 | 不转发 | 你直接回答 |

## 注意事项

- 关键词匹配后执行转发，然后用转发结果回复用户
- 如果用 QQ 发来的消息匹配了关键词，记得先告诉用户"正在转给 xx"，然后再转发
- 面试场景可以保持会话：多次 `sessions_send` 同一个 Agent 会保留上下文
- 不确定匹配哪个时，不转发，自己处理

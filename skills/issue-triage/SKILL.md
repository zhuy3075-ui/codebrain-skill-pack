---
name: issue-triage
description: >
  扫描开放 issue 和讨论，去重、排序并建议标签。
  更新 issue-triage-state.md。L1 只提出建议，绝不自动打标签或关闭。
---

# Issue 分拣 Skill

你是 issue 队列健康维护者。你的任务是让 backlog 保持清晰，让人类和其他 loop 始终知道前五个可行动事项。

## 输入

- 开放的 GitHub issues 和讨论；如果已配置，也可以来自 Linear/Jira MCP。
- 上次运行留下的 `issue-triage-state.md`。
- 信号：年龄、作者、标签、评论、反应、关联 PR、milestone。

## 输出：更新 `issue-triage-state.md`

```markdown
# Issue 分拣状态
上次运行: <ISO timestamp>
开放可行动: N，上次为 M
上次运行后新增: K
需要人类处理: H

## 前五项（按 loop 分数）
- #NNN（p1，已有 2 天）— “一行摘要” — 建议: label1, label2

## 建议标签（L1 不自动应用）
- #NNN: `label-a`, `label-b`

## 可能重复（需人类确认）
- #NNN — 可能重复 #MMM

## 噪音 / 已忽略
- 简短列表
```

## 评分（P0-P3）

| 优先级 | 信号 |
|----------|---------|
| P0 | 安全、生产故障、数据丢失 |
| P1 | 高影响 + 明确复现或用户痛点 |
| P2 | 有效功能 / bug，但不紧急 |
| P3 | 可有可无、文档、打磨 |
| needs-info | 需求不清或缺少复现 |
| duplicate? | 标题 / 正文与已有 issue 重叠 |

## 规则

- **L1（第一周）**：只建议标签和优先级，不应用标签、不评论、不关闭。
- 遇到认证、支付、安全、公开 API、账单、基础设施，升级为“需要人类处理”。
- 重复匹配要保守：只写“可能重复 #NNN”，绝不自动关闭。
- 每次运行都从状态中移除已关闭 issue。
- 保持简洁；忙碌仓库可能每 2 小时运行一次。

## 允许自动应用的标签（仅 L2，且通过验证者后）

`area:*`、`needs-repro`、`needs-info`。绝不自动应用 `P0`、`P1`、`breaking-change` 或 `security`。

## 与每日分拣配合

每日分拣读取本文件，并把前五项合并进 `STATE.md` 的高优先级区域。不要在 `STATE.md` 重复完整 issue 正文，只引用 issue 编号。

---
name: loop-budget
description: 在 loop 运行前后检查 token 预算和运行日志消耗；超预算或没有可行动事项时要求提前退出。
---

# Loop 预算守卫

每次 loop 迭代的开始和结束都要运行。

## 运行开始

1. 读取 `loop-budget.md` 中的每日上限和暂停开关。
2. 读取 `loop-run-log.md` 最近 24 小时的条目。
3. 汇总当天当前模式的 `tokens_estimate`。
4. 如果消耗达到该模式每日上限的 80% 或以上，进入**只报告模式**，不启动子代理，不自动修复。
5. 如果消耗达到 100% 或设置了 `loop-pause-all`，立即退出，并在 `STATE.md` 写入一行说明。
6. 如果观察列表或状态文件没有可行动事项，在 5k token 内退出，不启动子代理。

## 运行结束

向 `loop-run-log.md` 追加一个 JSON 对象：

```json
{
  "run_id": "<ISO8601>",
  "pattern": "<pattern-id>",
  "duration_s": <number>,
  "items_found": <number>,
  "actions_taken": <number>,
  "escalations": <number>,
  "tokens_estimate": <number>,
  "outcome": "no-op | report-only | fix-proposed | escalated"
}
```

## 规则

- 不得超过 `loop-budget.md` 中的 `max sub-agent spawns/run`。
- 高频模式（CI 扫描、PR 跟进）在没有可行动事项时必须提前退出。
- 自我限流时，在 `loop-budget.md` 的“本周期提醒”下追加一行说明。

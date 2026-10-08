---
name: ci-triage
description: >
  解析 CI 失败，识别失败 job/step，并分类为偶发、回归、环境或配置问题。
  在 CI 扫描 loop 中用于任何修复尝试之前。
---

# CI 分拣 Skill

## 每个失败项的输出

```markdown
### 失败 — branch @ sha
- Job / step:
- 错误: 1-3 行
- 分类: 偶发 / 回归 / 环境 / 配置
- 是否可行动: 是 / 否
- 建议 loop 行动: 最小修复 / 观察 / 升级给人类
```

## 分类规则

- **偶发**：间歇性失败，重试通过，无需代码改动。
- **回归**：新失败与近期提交相关。
- **环境**：runner、registry、secrets、quota 等问题。
- **配置**：workflow、依赖安装、缓存等问题。

环境失败应升级给人类，不要用代码改动“修复”。

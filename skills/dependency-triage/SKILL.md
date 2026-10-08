---
name: dependency-triage
description: >
  扫描 package manifest 和 lockfile，查找过期依赖和已知 CVE。
  按风险分组更新（patch、minor、major），用于依赖扫描 loop。
---

# 依赖分拣 Skill

## 每个包的输出

```markdown
### package-name (ecosystem: npm|pip|go|etc.)
- 当前版本: x.y.z
- 建议版本: x.y.z
- 风险: patch | minor | major
- CVE: none | CVE-XXXX (severity)
- 是否可行动: 是 / 否；说明是否在禁止清单或需要人类放行
- 建议 loop 行动: 在 worktree 中升级 patch / 升级给人类 / 跳过
```

## 分类规则

- **patch**：semver patch，或只改 lockfile 且没有 API 变化的安全修复。
- **minor**：semver minor，需要谨慎处理并经过验证者。
- **major**：除非状态文件明确预批准，否则一律升级给人类。
- **禁止清单**：状态文件禁止清单中的包一律升级给人类，不自动触碰。
- **高危 CVE**：如果修复需要 major 或破坏性变更，升级给人类。

## 规则

- 优先选择能解决公告的最小安全升级。
- 不要把无关包升级打包进同一个改动。
- 每次运行都记录 `dependency-sweeper-state.md` 中的人类覆盖决策。
- 如果出现 lockfile 冲突或 peer dependency 警告，升级给人类。

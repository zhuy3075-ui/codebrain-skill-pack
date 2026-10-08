# 技能目录

本包共 12 个技能。以下为文件内容所描述的用途，不代表已连接实际服务或已启用自动运行。

每个技能目录都可以单独安装，不要求全装。只做 Obsidian 项目记忆时，选择 `codebrain-memory` 即可；其他工程技能不以 Vault 为共同前提。完整的“何时调用、所需输入、结果与边界”见 [README 的使用条件](../README.md#每个技能的使用条件)。

| 技能 | 用途 | 说明 |
| --- | --- | --- |
| [codebrain-memory](../skills/codebrain-memory/SKILL.md) | 项目长期记忆 | 维护索引、任务、决策、阶段记录、交接和经验。 |
| [loop-budget](../skills/loop-budget/SKILL.md) | 预算约束 | 读取预算和运行日志，约定超预算时退出或只报告。 |
| [loop-triage](../skills/loop-triage/SKILL.md) | 工程信号汇总 | 将 CI、工单、近期变更等信息分为高优先级、观察和噪音。 |
| [pr-review-triage](../skills/pr-review-triage/SKILL.md) | PR 状态分拣 | 整理 CI、审查意见及合并阻塞。 |
| [ci-triage](../skills/ci-triage/SKILL.md) | CI 失败分析 | 区分偶发、回归、环境和配置问题。 |
| [dependency-triage](../skills/dependency-triage/SKILL.md) | 依赖检查 | 按升级幅度与安全风险提出处理建议。 |
| [post-merge-scan](../skills/post-merge-scan/SKILL.md) | 合并后检查 | 查找 TODO、废弃 API、坏链接和过期功能开关。 |
| [changelog-scan](../skills/changelog-scan/SKILL.md) | 变更素材整理 | 提取近期合并和提交中的用户可见变化。 |
| [draft-release-notes](../skills/draft-release-notes/SKILL.md) | 发布说明草稿 | 生成分类说明，发布前要求人工复核。 |
| [issue-triage](../skills/issue-triage/SKILL.md) | Issue 分拣 | 排序、识别可能重复项并建议标签。 |
| [minimal-fix](../skills/minimal-fix/SKILL.md) | 最小范围修复 | 约束明确问题的修复范围和验证要求。 |
| [loop-verifier](../skills/loop-verifier/SKILL.md) | 独立验证约定 | 从范围、意图、测试和风险检查修复结果。 |

`codebrain-memory` 包含 4 份参考文档、30 个 Vault 模板文件和界面配置。其余 11 个技能各包含一个 `SKILL.md`；部分是简短规则提示，成熟度与完整度不同。

分拣类技能依赖具体项目的数据和工具；`loop-budget` 引用的预算文件与日志需要另行提供；`minimal-fix` 和 `loop-verifier` 规定了角色分工，但本包未实现调度这些角色的程序。

独立安装不等于独立完成整条工作流。例如发布说明可以接收用户给出的变更清单，不必依赖 `changelog-scan`；验证技能则必须拿到实际改动和测试环境，并由独立角色执行。缺少所需输入或权限时，应说明缺口，而不是输出未经验证的结论。

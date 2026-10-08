# CODEBRAIN Skill Pack

**为 Codex 提供可持续的项目记忆与工程协作规范。**

CODEBRAIN Skill Pack 将项目目标、任务、决策、阶段证据、交接状态和经验保存为 Markdown 文档，使用 Obsidian Vault 作为长期记忆库，帮助 Codex 在后续会话中恢复项目上下文。

本仓库包含 **12 个技能、2 份 AGENTS 协议模板和一套完整 Vault 模板**，采用 [MIT 许可证](LICENSE)。

[快速开始](#快速开始) · [安装说明](docs/installation.md) · [技能目录](docs/skills.md) · [贡献指南](CONTRIBUTING.md)

## 适用场景

- 项目跨多个会话推进，需要快速恢复目标、进度和下一步。
- 希望把任务、技术决策和验证证据留在自己可管理的文件中。
- 使用 Codex 开发或维护项目，希望形成明确的计划、审查和交接流程。
- 需要按任务选择 CI、PR、Issue、依赖检查或变更整理的辅助规则。

## 核心功能

| 组成 | 功能 |
| --- | --- |
| `codebrain-memory` | 按需读取项目上下文，维护长期记忆和交接状态 |
| 工程辅助技能 | 分拣工程信号，规范最小修复、独立验证和发布说明草稿 |
| AGENTS 协议模板 | 定义需求理解、方案评估、计划、编码、审查与人工放行边界 |
| Vault 模板 | 提供项目、收件箱、知识、全局索引和归档的基础目录 |

本包提供技能指令与文档模板。它没有后台服务、调度器或自动执行的 Hook；相关行为发生在 Codex 加载技能并处理任务时。外部工具、连接器和权限需要在使用环境中实际可用。

## 快速开始

### 1. 新建 Obsidian Vault

**首次使用前，先在 Obsidian 中新建一个专门用于 CODEBRAIN 的 Vault 文件夹，并记下它的完整绝对路径。**

例如 `D:\Obsidian\CODEBRAIN`。这是个人项目记忆库，应放在本技能分发仓库之外。

### 2. 安装技能

将本仓库中的 `skills/codebrain-memory/` 整个目录复制到 `~/.codex/skills/codebrain-memory/`。保留技能内部的 `references/`、`assets/` 和 `agents/`。

其他 11 个技能按需复制到 `~/.codex/skills/`。目标已存在时，先比较和备份，避免覆盖自己的修改。然后新开 Codex 会话，确认所需技能已出现在可见技能列表中。

### 3. 首次把 Vault 路径告诉 Skill

在 Codex 中发送下面的提示词，将示例路径替换为刚创建的文件夹路径：

```text
使用 $codebrain-memory。
我已经在 Obsidian 中新建了 CODEBRAIN Vault，完整路径是：D:\Obsidian\CODEBRAIN
请在这个目录中初始化记忆库模板，保留已有文件和 Obsidian 配置，
检查目录结构，并告诉我后续项目记录保存在哪里。
```

技能应优先使用你明确提供的路径，检查目录是否存在，只补充缺失模板，并报告初始化结果。只提供路径而未要求初始化时，技能先做只读检查。

**新会话不一定保留上一段聊天里的路径。** 后续可以再次告知路径，或自行把 `CODEBRAIN_HOME` 配置为该目录。设置方式及恢复顺序见[安装说明](docs/installation.md)。

### 4. 开始记录项目

```text
使用 $codebrain-memory。
我的 Vault 路径是：D:\Obsidian\CODEBRAIN
请为当前项目记录目标、验收标准和待办，完成工作后更新阶段日志和交接文档。
```

如需长期采用工程协议，再阅读 `templates/agents/` 中的模板，按需合并到全局或项目 `AGENTS.md`，不要直接覆盖已有协议。

## 技能清单

| 技能 | 用途 |
| --- | --- |
| [codebrain-memory](skills/codebrain-memory/SKILL.md) | 项目记忆与上下文恢复 |
| [loop-budget](skills/loop-budget/SKILL.md) | 预算约束与退出规则 |
| [loop-triage](skills/loop-triage/SKILL.md) | 工程信号分拣与状态汇总 |
| [pr-review-triage](skills/pr-review-triage/SKILL.md) | PR、CI 和审查阻塞整理 |
| [ci-triage](skills/ci-triage/SKILL.md) | CI 失败分类与定位 |
| [dependency-triage](skills/dependency-triage/SKILL.md) | 依赖升级与风险分组 |
| [post-merge-scan](skills/post-merge-scan/SKILL.md) | 合并后清理项扫描 |
| [changelog-scan](skills/changelog-scan/SKILL.md) | 提取变更记录素材 |
| [draft-release-notes](skills/draft-release-notes/SKILL.md) | 生成发布说明草稿 |
| [issue-triage](skills/issue-triage/SKILL.md) | Issue 排序、去重和标签建议 |
| [minimal-fix](skills/minimal-fix/SKILL.md) | 明确问题的最小范围修复 |
| [loop-verifier](skills/loop-verifier/SKILL.md) | 独立验证与风险复核 |

辅助技能需要实际项目数据和可调用工具。`loop-budget` 等技能引用的状态与预算文件需要按任务准备，本包不包含完整 Loop 启动器。

## 仓库结构

```text
codebrain-skill-pack/
├── README.md                 # 项目介绍与快速开始
├── LICENSE                   # MIT 许可证
├── CHANGELOG.md              # 变更记录
├── CONTRIBUTING.md           # 贡献与验证规范
├── .gitignore
├── .gitattributes
├── docs/
│   ├── installation.md       # 安装、Vault 初始化与验证
│   ├── skills.md             # 技能说明与使用边界
│   └── structure.md          # 目录职责
├── templates/
│   └── agents/
│       ├── AGENTS.global.md
│       └── AGENTS.project.md
└── skills/
    ├── codebrain-memory/
    │   ├── SKILL.md
    │   ├── agents/openai.yaml
    │   ├── references/
    │   └── assets/vault-template/
    └── …                     # 其余 11 个技能
```

Vault 模板只维护一份，位于 `codebrain-memory` 的资源目录中，复制整个技能即可携带模板。

## 项目记忆如何组织

个人 Vault 中，每个项目位于 `01_Projects/<project-slug>/`，核心文件如下：

| 文件 | 保存内容 |
| --- | --- |
| `PROJECT_INDEX.md` | 项目目标、代码入口、文档位置和模块地图 |
| `TASKS.md` | 按优先级排序的任务与验收标准 |
| `DECISIONS.md` | 重要决策、原因和取舍 |
| `PHASE_LOG.md` | 阶段摘要、修改范围和验证证据 |
| `HANDOFF.md` | 当前状态、阻塞项和下一步 |
| `LESSONS.md` | 已验证、可复用的经验 |

## 使用边界

- L1 用于报告和分拣；L2 修复需要明确授权、隔离工作区和验证证据；L3 无人值守默认不启用。
- 技能提供流程约定，不会自动安装插件、创建定时任务、取得外部权限或执行发布。
- 不将私人 Vault、敏感对话、凭据或真实项目记录写回分发模板。
- 合并、部署、发布、回滚及权限变更遵循用户明确授权和项目规则。

## 验证与贡献

本仓库是文档与技能包，没有应用编译步骤。修改时应检查技能元数据、资源完整性、模板结构及文档相对链接；涉及行为变更时，还应在实际会话中验证。详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证

本项目采用 [MIT License](LICENSE)。

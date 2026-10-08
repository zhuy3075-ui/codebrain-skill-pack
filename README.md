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

**这是一个技能合集，每个 `skills/<技能名>/` 都是独立的安装单位，不需要一次安装全部 12 个。** 独立安装不代表没有使用前提：有些技能需要项目数据、状态文件或另一个角色提供的修复结果。

### 先决定安装哪些

- **只需要 Obsidian 项目记忆：** 安装 `codebrain-memory` 即可；其他 11 个技能和两份 AGENTS 模板都不是必装依赖。
- **遇到具体工程问题：** 按下表选择对应技能，例如 CI 失败时选择 `ci-triage`。其他工程技能不要求先创建 Vault；Vault 是 `codebrain-memory` 记忆工作流的前提。
- **需要修复并复核：** 可组合 `minimal-fix` 与 `loop-verifier`，由不同角色完成实现和验证。
- **需要持续巡检：** 再考虑 `loop-triage` 与 `loop-budget`；先准备数据源、状态、预算和执行环境。仅复制这两个技能不会启动定时任务。

### 每个技能的使用条件

下表说明什么时候值得调用，以及调用前需要什么。数据可来自当前会话可读取的本地材料、用户提供的日志或已连接服务；涉及 GitHub 等远端时，必须具备相应访问权限。缺少输入时，应先补充材料，不能把“无法读取”当成“没有问题”。

| 技能 | 什么时候用 | 使用前需要准备 | 结果与边界 |
| --- | --- | --- | --- |
| [codebrain-memory](skills/codebrain-memory/SKILL.md) | 项目跨会话推进，需要记录任务、决策和交接 | 新建 Obsidian Vault，首次告知完整路径；提供项目目标和上下文；写入时需要相应授权 | 维护 Markdown 记忆；可单独使用，不是后台记忆服务 |
| [loop-budget](skills/loop-budget/SKILL.md) | 已有 Loop 工作流，需要检查预算与退出条件 | `loop-budget.md`、`loop-run-log.md`、`STATE.md` 的位置，以及预算上限、暂停设置、用量记录；首轮需先初始化 | 按记录判断是否只报告或退出；不会自行获取真实账单或启动 Loop |
| [loop-triage](skills/loop-triage/SKILL.md) | 需要汇总近期工程信号并确定处理顺序 | 指定时间范围内的 CI、Issue/工单、提交或相关对话，以及现有状态；说明哪些来源不可用 | 输出高优先级、观察、噪音与状态建议；不直接修复业务代码 |
| [pr-review-triage](skills/pr-review-triage/SKILL.md) | 有具体 PR，需要判断被什么阻塞 | PR 地址或编号、最新 CI 状态、审查意见、项目合并规则和必需检查 | 整理阻塞项与建议；“可合并”不是自动合并授权 |
| [ci-triage](skills/ci-triage/SKILL.md) | CI 流水线失败，需要先分类定位 | 失败 job/step 的日志、对应分支或提交；如有，提供历史成功/重试结果 | 区分偶发、回归、环境和配置问题；环境问题不能靠无关代码修改掩盖 |
| [dependency-triage](skills/dependency-triage/SKILL.md) | 需要检查过期依赖、升级幅度或漏洞 | 依赖清单与 lockfile、可核实的版本/安全公告、项目升级约束；持续使用时维护 `dependency-sweeper-state.md` | 提出升级分组与风险建议；缺少最新公告时不能声称已完成 CVE 检查 |
| [post-merge-scan](skills/post-merge-scan/SKILL.md) | 代码已合并，希望发现后续清理项 | 合并记录、相关 diff 和代码；指定范围，原规则默认最近 7 天 | 报告 TODO、废弃 API、坏链接等；不据此自动展开大型重构 |
| [changelog-scan](skills/changelog-scan/SKILL.md) | 准备发版，需要整理实际变更素材 | 上次发布的 tag/提交或明确起止范围，以及该范围的提交/合并记录 | 输出面向用户的变化、破坏性变更和安全信号；不创建发布 |
| [draft-release-notes](skills/draft-release-notes/SKILL.md) | 已有变更素材，需要编写发布说明 | 已核实的变更清单；可由 `changelog-scan` 提供，也可由用户提供 | 生成草稿，发布前人工复核；不强制安装 `changelog-scan` |
| [issue-triage](skills/issue-triage/SKILL.md) | 有待处理的 Issue/讨论，需要排序和识别重复 | Issue/讨论内容、当前状态；持续使用时提供 `issue-triage-state.md`，首次先初始化 | 输出优先事项与标签建议；L1 不自动打标签、评论或关闭 Issue |
| [minimal-fix](skills/minimal-fix/SKILL.md) | 问题已明确，适合一个小范围修复 | 精确问题/复现或预期、相关代码、测试命令、允许与禁止范围；L2 还需明确授权和隔离工作区 | 实现最小修复并给出证据；超出范围时升级，由独立验证者复核 |
| [loop-verifier](skills/loop-verifier/SKILL.md) | 已有代码改动，需要独立验收 | 原始目标、diff、允许范围、测试/lint 命令和可运行环境；验证者与实现者分开 | 自行检查并报告通过、拒绝或升级；不能只复述实现者的测试结论 |

`loop-budget.md` 等运行状态文件应放在实际工作项目指定的位置，不是需要安装到技能目录中的依赖包。本仓库不包含完整 Loop 启动器，也没有预设所有运行状态文件。首次使用前应先明确它们的位置和初始内容。

### 技能怎样配合

常见组合是 `ci-triage → minimal-fix → loop-verifier`，以及 `changelog-scan → draft-release-notes`。这是按任务选择的工作顺序，不是安装后自动执行的流水线；阶段之间仍需满足各自的输入、权限和人工放行要求。

## 两份 AGENTS 文档有什么区别

**本仓库当前的 `AGENTS.global.md` 和 `AGENTS.project.md` 内容完全相同。** 它们是同一套工程协议的两份放置模板，没有不同的技能功能，也不是两个会独立运行的 Agent。文件名中的 `global` 和 `project` 用来提示安装范围。

| 模板 | 合并到哪里 | 用于什么范围 | 什么时候选 |
| --- | --- | --- | --- |
| [AGENTS.global.md](templates/agents/AGENTS.global.md) | Codex 用户配置目录中的 `AGENTS.md`，默认 `~/.codex/AGENTS.md`；自定义 `CODEX_HOME` 时使用该目录 | 为该 Codex 配置下的不同项目提供通用约定 | 希望多个项目都采用这套工作方式 |
| [AGENTS.project.md](templates/agents/AGENTS.project.md) | 目标项目根目录的 `AGENTS.md` | 为该项目提供规则；子目录可有更具体的约定 | 先在一个项目试用，或与项目协作者共享规则 |

默认识别的文件名是 `AGENTS.md`（也支持 `AGENTS.override.md` 等机制），不是这里用于分发的 `AGENTS.global.md` / `AGENTS.project.md`。把文件留在 `templates/agents/` 并不等于已安装。全局规则与项目规则可以同时加载，越接近工作目录的规则越具体；详情见 [OpenAI 官方 AGENTS.md 说明](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。

**建议先在单个项目中按需合并项目模板。** 确定通用习惯后，再把共性规则放进全局文件，项目文件只保留本项目的测试命令、目录约束等差异。不必把当前两份相同内容各复制一遍，也不要覆盖已有协议。

只想显式调用 `codebrain-memory` 时，可以先不使用这两份协议。`SKILL.md` 描述一项任务如何完成，`AGENTS.md` 提供跨任务的工作约定；安装技能不会自动安装 AGENTS 协议，协议提到的技能也不会因此自动安装。

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

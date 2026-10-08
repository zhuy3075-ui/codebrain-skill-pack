# 目录职责

| 路径 | 职责 |
| --- | --- |
| `README.md` | 项目入口、功能说明、快速开始 |
| `LICENSE` | MIT 许可证 |
| `CHANGELOG.md` | 面向使用者的变更记录 |
| `CONTRIBUTING.md` | 修改与验证约定 |
| `docs/` | 安装、技能说明和目录职责 |
| `templates/agents/` | 供用户合并的全局与项目协议模板 |
| `skills/<name>/` | 可独立复制的技能目录 |
| `skills/codebrain-memory/assets/vault-template/` | 唯一维护的空 Vault 模板 |

技能的 `references/`、`assets/` 和 `agents/` 保留在技能内部，以便单独分发。顶层不再复制另一套 Vault 模板，避免内容不同步。

`templates/agents/` 中的协议供使用者选择与合并，不直接放在仓库根目录作为自动生效的 `AGENTS.md`。本仓库没有应用运行代码，因此没有空的 `src/`、构建目录或定时运行的 CI 配置。

私人 Vault、临时分析与导出 ZIP 位于仓库之外。根目录的 `.gitignore` 排除常见本地文件，`.gitattributes` 统一 Markdown 和配置文件的 Git 文本换行约定。

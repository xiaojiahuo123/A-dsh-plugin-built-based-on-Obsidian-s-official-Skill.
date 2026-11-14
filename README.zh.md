# dsh-obsidian-skills

[English](README.md) | [中文](README.zh.md)

将 [Obsidian 官方 Agent Skills](https://github.com/obsidianmd/obsidian-skills) 重新打包为 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)（DSH）插件。一次安装，**全部 7 个**技能在所有会话中可用，无需手动复制目录。技能文件与上游（`plugins/obsidian/skills/`）逐字节一致，包含全部 `references/` 参考文档。

## 包含的技能

| 技能 | 教会智能体什么 | 额外依赖 |
|---|---|---|
| **obsidian-markdown** | Obsidian 风味 Markdown：wikilink、嵌入、callout、frontmatter 属性、标签、高亮、LaTeX、Mermaid | 无 |
| **obsidian-bases** | `.base` 文件：数据库式视图（table/cards/list/map/kanban）、过滤器、公式、汇总 | 无 |
| **json-canvas** | `.canvas` 文件：节点、连线、分组，含布局规则与校验清单 | 无 |
| **defuddle** | 用 Defuddle CLI 从网页提取干净的 Markdown | `npm i -g defuddle` |
| **knap** | 用 JSON/CSV 数据 + 模板批量渲染 Markdown 笔记 | `npm i -g knap` |
| **obsidian-cli** | 操控运行中的 Obsidian 桌面端：读取/创建/搜索笔记、任务、属性，以及插件与主题的开发调试 | `obsidian` CLI（随安装包提供）+ 桌面端运行且已启用 CLI |
| **obsidian-headless** | 用 `ob` 在服务器、CI 或沙箱中通过命令行运行 Obsidian Sync / Publish | Node.js 22+ 及 `npm i -g obsidian-headless` |

前 3 个是纯知识包（格式参考文档），其余 5 个是教智能体调用对应的命令行工具——需要单独安装/启用这些工具才能完整使用。

## 安装

**从本地目录安装**（克隆本仓库后）：

- DSH Web 界面 → **插件** → **添加插件** → 选择本目录；或
- 直接对智能体说："安装 `<本目录路径>` 下的 bundle"。

**从 git 地址安装：**

```
https://github.com/xiaojiahuo123/A-dsh-plugin-built-based-on-Obsidian-s-official-Skill..git
```

启用后，打开**新会话**即可在技能目录中看到 7 个技能。禁用插件即可移除。

## 工作原理

本插件为纯配置型 bundle。`cordis.patch.yml` 挂载了一个独立的 `@deepseek-ai/dsh-skill-filesystem` 实例，设置 `includeDefaultRoots: false`，并用 `bundledSkillDir` 指向包内 `skills/` 目录（rank 600，不会覆盖你的项目级或用户级同名技能）。技能文件带 watch 监听；原始目录结构（`<名称>/SKILL.md` 加 `references/`）原样保留。

## 更新技能内容

技能内容镜像自 `obsidianmd/obsidian-skills`（`plugins/obsidian/skills/`）。如需更新，将上游技能目录复制到 `skills/` 下，并提升 `package.json` 中的 `version`。

## 许可证

MIT。技能内容 © Obsidian（obsidianmd），来自 [obsidianmd/obsidian-skills](https://github.com/obsidianmd/obsidian-skills)，MIT 许可证，详见 `LICENSE`。

# yanzhi-sdd-workflow

一个 Claude Code 插件，提供「头脑风暴 → Spec 生成 → 任务拆分」的结构化需求到规格工作流，结合 Superpowers 和 SpecKit 插件。

## 前置依赖

本插件依赖以下外部插件提供的能力：

### brainstorm-and-specify 依赖

- **[SpecKit](https://github.com/zhang-songhan/speckit)** — 提供 `speckit-specify`、`speckit-clarify`、`speckit-plan`、`speckit-tasks`
- **[Superpowers](https://github.com/anthropic/claude-code-superpowers)** — 提供 `superpowers:brainstorming` 和 `superpowers:test-driven-development`

### manual-and-docs-git-sync 依赖

- **[yanzhi-user-manual-generator](https://github.com/zhang-songhan/yanzhi-user-manual-generator)** — 提供 `writing-user-manual`、`generating-html-manual`
- **[yanzhi-docs-generator](https://github.com/zhang-songhan/yanzhi-docs-generator)** — 提供 `writing-docs`
- **[project-version-workflow](https://github.com/ATreep/project-version-workflow)** — 提供 `update-commit-bypass`

## 安装

在 Claude Code 中依次执行以下命令：

```
/plugin marketplace add zhang-songhan/yanzhi-sdd-workflow
/plugin install yanzhi-sdd-workflow
```

## 包含的 Skill

### brainstorm-and-specify

将模糊的需求想法通过结构化流程转化为完整的 SpecKit 规格文档：

1. **前置检查** — 验证 SpecKit 已初始化、Superpowers 已安装
2. **需求确认** — 复述用户需求，确保理解一致
3. **头脑风暴** — 调用 `superpowers:brainstorming` 细化需求（不生成 Spec 文档）
4. **Spec 生成** — 依次调用 `speckit-specify` → `speckit-clarify` → `speckit-plan` → `speckit-tasks`
5. **输出执行提示** — 根据需求类型（代码实现 / 文档生成 / 重构）给出对应的 `/goal` 命令

触发方式：输入 `/brainstorm-and-specify` 或在对话中描述功能想法并请求生成 Spec。

### manual-and-docs-git-sync

在 brainstorming-specify-tdd 工作流完成后，自动同步用户手册、架构文档并推送双仓库：

1. **用户手册** — 生成/更新 Markdown 手册（`yanzhi-user-manual/<version-name>-YYMMDD-HHmmss/`），截图由 writing-user-manual 内部处理
2. **HTML 转换** — 将手册转为带侧边栏导航的独立 HTML 页面
3. **架构文档** — 克隆公司文档仓库，调用 writing-docs 更新项目架构文档
4. **双仓库推送** — 将项目仓库和文档仓库分别推送到 `auto-workflow` 分支

触发方式：输入 `/manual-and-docs-git-sync` 或在工作流完成后请求同步文档。

## 工作流示意

```
需求输入 → 头脑风暴 → SpecKit → TDD 实现 → 文档同步（manual-and-docs-git-sync）
```

## 许可

MIT

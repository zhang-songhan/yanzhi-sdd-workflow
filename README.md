# yanzhi-sdd-workflow

一个 Claude Code 插件，提供「头脑风暴 → Spec 生成 → 任务拆分」的结构化需求到规格工作流，结合 Superpowers 和 SpecKit 插件。

## 前置依赖

- **[SpecKit](https://github.com/zhang-songhan/speckit)** — 提供 `speckit-specify`、`speckit-clarify`、`speckit-plan`、`speckit-tasks`
- **[Superpowers](https://github.com/anthropic/claude-code-superpowers)** — 提供 `superpowers:brainstorming` 和 `superpowers:test-driven-development`

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

## 工作流示意

```
需求输入 → 前置检查 → 头脑风暴澄清 → SpecKit 生成 Spec → 输出执行提示
```

## 许可

MIT

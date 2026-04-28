# Prompt System

这套目录用于存放可复用的 Prompt 基座，不再按单个项目重复重写角色提示词和流程提示词。

## 设计目标

- 角色提示词长期复用
- 流程规则集中维护
- 项目只替换上下文，不重写角色
- 领域差异单独放在 `domains`
- 旧版 `ai-prompts` 保留，新项目优先使用这里

## 目录结构

- `start-project.md`
  - 项目启动入口，告诉你每次新项目该先读什么、怎么装配
- `core/global-rules.md`
  - 全局通用规则，所有角色共享
- `flows/standard-website-flow.md`
  - 标准官网项目流程
- `roles/*.md`
  - 可复用角色基座，只写职责、边界、输出要求
- `domains/website.md`
  - 官网类项目的领域约束
- `contexts/project-context-template.md`
  - 每个项目单独填写的上下文模板

## 使用原则

不要直接从某一个角色文件单独开始。先定项目上下文，再选领域规则和流程规则，最后把这些内容装配到对应角色 Prompt 里。

如果你是新开项目，优先先读 `start-project.md`。

推荐装配顺序：

1. 复制 `contexts/project-context-template.md`，填写项目上下文。
2. 选择领域规则，例如 `domains/website.md`。
3. 选择流程规则，例如 `flows/standard-website-flow.md`。
4. 选择要启用的角色，例如 `roles/analyst.md`、`roles/ui-designer.md`、`roles/developer.md`。
5. 将 `全局规则 + 领域规则 + 流程规则 + 项目上下文 + 角色 Prompt + 当前任务输入` 拼成最终 Prompt。

## 最小可用组合

官网项目快速启动时，建议先用：

1. `roles/analyst.md`
2. `roles/ui-designer.md`
3. `roles/developer.md`
4. `roles/reviewer.md`

如果项目复杂度更高，再加入：

1. `roles/orchestrator.md`
2. `roles/architect.md`

## 推荐装配格式

可以按下面这个顺序拼接：

```text
[Global Rules]
{{GLOBAL_RULES}}

[Domain Rules]
{{DOMAIN_RULES}}

[Flow Rules]
{{FLOW_RULES}}

[Project Context]
{{PROJECT_CONTEXT}}

[Role Prompt]
{{ROLE_PROMPT}}

[Current Task]
{{CURRENT_TASK}}

[Upstream Inputs]
{{UPSTREAM_INPUTS}}
```

## 维护原则

- 项目变化优先改 `contexts`
- 流程变化优先改 `flows`
- 领域差异优先改 `domains`
- 角色本身发生边界变化时才改 `roles`
- 所有角色共享的规则统一改 `core`

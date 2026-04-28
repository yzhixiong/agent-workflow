# Start Project

这份文件是新项目的标准启动入口。

每次开始一个新项目时，不要直接打开某个角色 Prompt。先按这里的顺序初始化，再进入实际执行。

## 启动目标

通过固定顺序装配 Prompt，避免每次项目都重新写角色提示词和流程提示词。

## 标准启动顺序

1. 先读取 `README.md`
   - 目的：理解这套 Prompt System 的目录结构和装配原则。

2. 再读取 `core/global-rules.md`
   - 目的：加载所有角色共享的通用规则。

3. 选择并读取一个领域文件
   - 例如：`domains/website.md`
   - 目的：加载当前项目所属领域的特有约束。

4. 选择并读取一个流程文件
   - 例如：`flows/standard-website-flow.md`
   - 目的：确定角色流转顺序、阶段进入条件和回退规则。

5. 复制并填写 `contexts/project-context-template.md`
   - 目的：把项目本身的信息补齐，作为所有角色的共享输入。

6. 选择当前阶段需要的角色文件
   - 例如：`roles/orchestrator.md`、`roles/analyst.md`、`roles/ui-designer.md`
   - 目的：只给当前阶段需要的角色加载角色职责、边界和输出要求。

7. 最后补充当前任务和上游输入
   - 目的：生成本轮实际要执行的最终 Prompt。

## 标准装配顺序

最终 Prompt 建议按下面顺序拼接：

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

## 官网项目最常见启动方式

如果是一个新的官网项目，建议这样开始：

1. 读取 `domains/website.md`
2. 读取 `flows/standard-website-flow.md`
3. 填写 `contexts/project-context-template.md`
4. 如果需求还不清楚，先读取 `roles/analyst.md`
5. 如果需要判断下一步做什么，先读取 `roles/orchestrator.md`
6. 如果需求已经清楚，要进入视觉阶段，读取 `roles/ui-designer.md`

## 角色选择建议

- 需求不清：`orchestrator` 或 `analyst`
- 要梳理页面目标和信息结构：`analyst`
- 要确定视觉方向和交互表达：`ui-designer`
- 要确定结构、组件和工程方案：`architect`
- 要落代码：`developer`
- 要做质量把关：`reviewer`

## 使用边界

- 不要一次性把所有角色都塞进同一轮任务。
- 不要跳过项目上下文直接开始角色执行。
- 不要把领域规则写回角色文件里。
- 不要把流程规则重复写进每个角色文件里。

## 一句话工作方式

先初始化 Prompt System，再填写项目上下文，然后只装配当前阶段需要的角色。

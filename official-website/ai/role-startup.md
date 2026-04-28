# AI Role Startup Guide

基于 `/Users/ocean/tritree-work/prompt-system` 的官网项目初始化说明。

## 启动原则

- 先填共享上下文，再启用角色
- 当前阶段一次只装配一个角色
- 官网项目默认流程：`Orchestrator -> Analyst -> UI Designer -> Architect -> Developer -> Reviewer -> Orchestrator`
- 如果需求还不清楚，不进入设计、架构或开发

## 当前推荐启动方式

当前项目目录还是空的，建议从以下两轮开始：

1. 第一轮：`Orchestrator`
   - 目标：判断当前阶段，确认是否已具备进入需求分析的条件
2. 第二轮：`Analyst`
   - 目标：把官网目标、页面范围、目标用户、转化动作整理清楚

在 `Analyst` 输出清楚之前，不建议直接启用 `UI Designer` 或 `Developer`。

## Prompt 装配顺序

每一轮都按下面顺序拼接：

```text
[Global Rules]
引用：/Users/ocean/tritree-work/prompt-system/core/global-rules.md

[Domain Rules]
引用：/Users/ocean/tritree-work/prompt-system/domains/website.md

[Flow Rules]
引用：/Users/ocean/tritree-work/prompt-system/flows/standard-website-flow.md

[Project Context]
引用：/Users/ocean/tritree-work/official-website/ai/project-context.md

[Role Prompt]
引用当前角色文件

[Current Task]
写本轮任务

[Upstream Inputs]
放用户补充信息、参考站分析、上游角色产出
```

## 当前阶段角色选择

### 1. Orchestrator

角色文件：
- `/Users/ocean/tritree-work/prompt-system/roles/orchestrator.md`

建议当前任务：

```text
请基于当前官网项目上下文，判断项目所处阶段，检查是否具备进入需求分析阶段的条件。
如果信息不足，请明确列出缺失项、影响范围，并整理一份发给 Analyst 的任务说明。
```

上游输入建议：
- 用户当前对公司官网的原始想法
- 已有品牌资料、业务介绍、参考网站、时间要求

### 2. Analyst

角色文件：
- `/Users/ocean/tritree-work/prompt-system/roles/analyst.md`

建议当前任务：

```text
请把当前公司官网项目的目标、目标用户、页面范围、内容优先级和转化动作整理为可执行需求。
如果信息不足，请明确指出缺失项，不要编造，并输出给 UI Designer / Architect 可直接使用的结果。
```

上游输入建议：
- `Orchestrator` 的阶段判断
- 用户补充的业务背景、目标用户、页面范围、转化目标、参考网站

## 后续角色进入条件

### UI Designer

进入前提：
- 需求目标清楚
- 页面范围清楚
- 重点页面和转化动作清楚

不要在以下情况下进入：
- 只知道“做个高级一点的官网”
- 没有明确业务重点和信息层级

### Architect

进入前提：
- 设计方向基本明确
- 页面结构和内容模块已形成稳定方案
- 已知是否需要 CMS、表单、埋点、多语言、动态内容

### Developer

进入前提：
- 页面结构、组件边界、SEO 和性能策略已明确
- 架构方案能直接指导实现

### Reviewer

进入前提：
- 开发已给出改动清单、自测结果、已知限制

## 你现在应该提供给我的信息

请优先补以下内容，我就可以继续扮演 `Orchestrator` 和你完成第一轮初始化：

1. 公司或品牌名称
2. 一句话介绍你们是做什么的
3. 官网核心目标
4. 目标用户
5. 本期计划上线哪些页面
6. 希望用户完成什么转化动作
7. 有无参考网站
8. 有无明确技术栈要求
9. 计划上线时间

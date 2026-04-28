# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Structure

This repository contains three independent components:

- **`vibe coding/`** — Vibe Coding framework documents (human-AI collaborative workflow)
- **`prompt-system/`** — Reusable prompt bases for multi-role AI collaboration projects
- **`official-website/`** — AI-related website project

## Vibe Coding Framework (vibe coding/)

A workflow framework for "I lead, Claude collaborates" style development.

### Versioning Rules
- Keep version inside `VIBE_CODING_FRAMEWORK_CLAUDE.md`
- Document commits use Chinese messages with version: `文档：调整流程规则 v0.4`
- Releases: annotated tags like `git tag -a v0.4 -m "VIBE_CODING_FRAMEWORK v0.4"`
- Push releases: `git push gitee main --follow-tags`
- Do not push proactively — wait for explicit instruction

### Core Workflow
```
Goal -> Milestone -> Feature -> Implementation
User: direction, judgment, decisions
Claude: research, organize, implement, sync docs
```

## Prompt System (prompt-system/)

A reusable prompt base system for multi-role AI collaboration. Avoids rewriting role prompts per project.

### Assembly Order for New Projects
1. Read `start-project.md` first
2. Load `core/global-rules.md` (shared rules for all roles)
3. Select domain rules (e.g., `domains/website.md`)
4. Select flow rules (e.g., `flows/standard-website-flow.md`)
5. Fill `contexts/project-context-template.md` with project details
6. Load only the roles needed for the current phase

### Standard Prompt Assembly
```
[Global Rules] {{GLOBAL_RULES}}
[Domain Rules] {{DOMAIN_RULES}}
[Flow Rules] {{FLOW_RULES}}
[Project Context] {{PROJECT_CONTEXT}}
[Role Prompt] {{ROLE_PROMPT}}
[Current Task] {{CURRENT_TASK}}
[Upstream Inputs] {{UPSTREAM_INPUTS}}
```

### Role Selection Guide
| Situation | Role |
|---|---|
| Requirements unclear | `orchestrator` or `analyst` |
| Clarify page goals and info structure | `analyst` |
| Determine visual direction | `ui-designer` |
| Determine structure, components, engineering | `architect` |
| Write code | `developer` |
| Quality gate | `reviewer` |

### Website Flow (standard-website-flow.md)
```
Orchestrator -> Analyst -> UI Designer -> Architect -> Developer -> Reviewer -> Orchestrator
```

Phase gates:
1. Requirements/goals/users/conversions not clarified → do not enter design or architecture
2. Visual direction not clear → do not enter detailed architecture or development
3. Page structure, component boundaries, data sources not clear → do not enter development
4. Developer has not provided change log, self-test results, known limits → do not enter review

### Maintenance Rules
- Project changes → modify `contexts`
- Flow changes → modify `flows`
- Domain differences → modify `domains`
- Role boundary changes → modify `roles`
- Shared rules → modify `core`

## No Build/Test Commands

This is a documentation and prompt framework repository — no npm/node/python build commands, no test runners. Work is entirely Markdown-based.
---
name: steering
description: 仅用于输出与维护 steering 文档的交互式工作流。即使以 workflow 形式触发，也只处理 steering 范围（如 constitution/product/tech/structure），不用于通用需求、设计、任务拆解或实现执行。
---

# Steering Only - 项目治理文档工作流

本能力仅服务于 steering 文档产出与更新，用于沉淀项目治理原则、产品方向、技术约束与目录结构约定，作为团队协作的长期参考。

## ⚠️ Interaction Rules (MUST Follow)

This skill uses a **phase-by-phase confirmation** workflow, ensuring users can review and adjust at each stage.

### Core Principles

1. **One phase at a time**: Only work on the current phase. NEVER generate documents for subsequent phases in advance.
2. **Mandatory confirmation**: After completing each phase, you MUST stop and wait for user confirmation.
3. **User-driven progression**: Only proceed to the next phase when user explicitly says "continue", "ok", "next", "looks good", "继续", "好", "下一步", etc.

### Confirmation Template

After completing each phase, you MUST use this format to request confirmation:

```
📋 **[Phase Name] Complete**

Created `.spec-flow/active/<feature>/<file>.md` containing:
- [Key content summary]

**Please review**:
1. [Review question]?
2. [Review question]?

✅ Say "continue" to proceed to next phase
✏️ Tell me what to modify if needed
```

### ❌ Prohibited Behaviors

- Generating multiple phase documents after user describes a feature
- Automatically proceeding to next phase without user confirmation
- Creating both proposal.md and requirements.md in one response
- Assuming user wants to skip confirmation for speed

### ✅ Correct Flow Example

```
User: I want to implement user authentication
AI: [Creates only proposal.md] + confirmation prompt

User: continue
AI: [Creates only requirements.md] + confirmation prompt

User: looks good, next
AI: [Creates only design.md] + confirmation prompt

User: continue
AI: [Creates only tasks.md] + confirmation prompt
```

### Fast Mode (Optional)

If user explicitly requests to skip phase-by-phase confirmation:
- "generate all documents at once"
- "fast mode"
- "skip confirmations"

Then you may generate all documents consecutively, but still request final overall confirmation.

## Quick Start

1. Initialize spec directory: Run `scripts/init-spec-flow.sh <feature-name>` or manually create `.spec-flow/active/<feature-name>/`
2. Copy templates from this skill's `templates/` directory
3. Follow two-phase workflow below
4. Archive completed specs to `.spec-flow/archive/` when done

## Two-Phase Workflow

### Phase 1: Requirements

**Goal**: Define WHY + WHAT the change should achieve

Create `.spec-flow/active/<feature>/requirements.md`:

- **Background**: Context and motivation for the change
- **Goals**: What we want to achieve (with checkboxes)
- **Non-Goals**: What we explicitly won't do (reduces scope creep)
- **Scope**: In-scope vs out-of-scope boundaries
- **Risks**: Potential issues and mitigations
- **Open Questions**: Items needing clarification before proceeding

**Use EARS Format** (see `references/ears-format.md`) when functional rules are required:
- **Ubiquitous**: "The system shall..."
- **Event-Driven**: "When [trigger], the system shall..."
- **State-Driven**: "While [state], the system shall..."
- **Unwanted Behavior**: "If [condition], then the system shall NOT..."

**Include**:
- Functional requirements (FR-001, FR-002, ...)
- Non-functional requirements: Performance, Security, Reliability (NFR-001, ...)
- Acceptance criteria (AC-001, AC-002, ...)
- Steering intent (WHY), scope boundary, and core requirements (WHAT)

**Exit Criteria**: WHY and WHAT are both clear, testable where needed, and agreed.

**⏸️ Phase Checkpoint**: After creating requirements.md, ask user:
- Is the background accurate?
- Are goals clear and measurable?
- Is the scope boundary reasonable?
- Is risk assessment complete?
- Do functional requirements cover all use cases?
- Are non-functional requirements (performance/security/reliability) sufficient?
- Are acceptance criteria testable?

→ Wait for user confirmation before proceeding to Design phase

### Phase 2: Plan

**Goal**: Define HOW to implement + EXECUTABLE plan

#### Design

Create `.spec-flow/active/<feature>/design.md` using `templates/design.md.template`:

- **Architecture Overview**: High-level component diagram (use Mermaid)
- **Component Design**: Responsibilities and interfaces for each component
- **API Design**: Endpoints, request/response schemas
- **Data Model**: Entity relationships (use Mermaid erDiagram)
- **Error Handling**: Error codes, descriptions, resolutions
- **Migration Plan**: Steps for data/schema migrations (if applicable)

**Exit Criteria**: Design addresses all requirements, trade-offs documented.

**⏸️ Phase Checkpoint**: After creating design.md, ask user:
- Does the architecture meet all requirements?
- Is the API design clear?
- Are there any missing edge cases?

→ Wait for user confirmation before proceeding to tasks.md in Phase 2 Plan

#### Tasks

**Goal**: Break down into EXECUTABLE steps

Create `.spec-flow/active/<feature>/tasks.md` using `templates/tasks.md.template`:

**Task Guidelines** (see `references/task-decomposition.md`):
- Each task completable in 1-2 tool calls
- Include complexity estimate: Low/Medium/High
- List affected files
- Define dependencies between tasks
- Group into phases: Setup → Implementation → Testing → Documentation

**Progress Tracking**:
- ⏳ Pending → 🔄 In Progress → ✅ Done
- ❌ Blocked (add notes explaining blocker)

**Exit Criteria**: All tasks completed, tests passing, documentation updated.

**⏸️ Phase Checkpoint**: After creating tasks.md, ask user:
- Is the task granularity appropriate?
- Are dependencies correct?
- Ready to start implementation?

→ Wait for user confirmation before starting implementation

## ⚠️ Phase 3: Implementation

**Goal**: Execute tasks according to tasks.md

### 📦 Execution Mode: Phase Mode (Always)

Execute all tasks within a specific phase, then wait for confirmation.

**Key difference**: Confirmation happens **after each phase**, not after each task.

**When to use**: Want to review after each phase (Setup → Core → Testing → Docs)

**Trigger phrases**:
- "start implementation" / "开始执行"
- "execute phase 1" / "执行第一阶段"
- "execute setup phase" / "执行 Setup"
- "run all setup tasks"

**Flow**:
```
User: execute setup phase

AI: 📦 **Phase Mode: Setup**

    🔄 T-001: [description] → ✅
    🔄 T-002: [description] → ✅

    ✅ **Setup Phase Complete** (2/10 total)

    **Next phase**: Core Implementation (T-010 to T-015)
    👉 Say "continue" or "execute next phase"
```

### 🚨 BEFORE Starting Any Task

You MUST do these steps before executing:

1. **Read tasks.md** - Get current task list and statuses
2. **Identify target tasks** - Select tasks for the current phase only
3. **Check dependencies** - Ensure dependency tasks are completed (`- [x]`)
4. **Read design.md** - Review relevant design sections

### ✅ REQUIRED Behaviors

- Read tasks.md before starting each phase
- Check dependencies before each task
- Update `- [ ]` to `- [x]` after each task
- Show progress for each task and phase summary
- Wait for confirmation after each phase
- Stop immediately on error

### ❌ PROHIBITED Behaviors

| Prohibited Action | Why It's Wrong |
|-------------------|----------------|
| Skip a task | Breaks dependency chain |
| Execute tasks out of order | Dependencies may not be met |
| Do work not in tasks.md | Scope creep, untracked changes |
| Forget to update tasks.md | Progress tracking inaccurate |
| Continue after error without user approval | May cause cascading failures |

### 🛑 When to STOP

Stop and ask user for guidance when:
- A task fails or produces errors
- Design is incomplete for current task
- A dependency is missing or blocked
- Task description is ambiguous
- Need a decision not covered in design.md

## Steering Documents (Optional)

For larger projects, create `.spec-flow/steering/` documents to provide consistent context across all specs:

| Document | Purpose | Template |
|----------|---------|----------|
| `constitution.md` | Project governance, decision-making principles | `templates/steering/constitution.md.template` |
| `product.md` | Product vision, target users, key metrics | `templates/steering/product.md.template` |
| `tech.md` | Tech stack, constraints, dependencies | `templates/steering/tech.md.template` |
| `structure.md` | Code organization, naming conventions | `templates/steering/structure.md.template` |

### Best Practices

1. **Keep specs updated**: Update status as work progresses
2. **Link to code**: Reference commits, PRs, file paths in tasks
3. **Archive completed specs**: Move to `.spec-flow/archive/` when done
4. **Review steering docs**: Reference them when writing new specs
5. **Validate completeness**: Run `scripts/validate-spec-flow.py` before implementation

## References

- **Complete workflow guide**: See `references/workflow.md`
- **EARS requirement format**: See `references/ears-format.md`
- **Task decomposition patterns**: See `references/task-decomposition.md`
- **Real-world examples**: See `references/examples/`

本仓库中的该 Skills 最初从下述源 Skills 复制而来，并已结合当前项目约束做本地化调整（如 steering-only、两阶段、plan 合并口径等）。

Source Skills:
https://github.com/echoVic/spec-flow/blob/main/SKILL.md
> updated_by: Cascade - GPT-5
> updated_at: 2026-02-14 17:30:00

# Steering 工作流（参考）

本文用于说明 steering 专用工作流，仅覆盖治理文档产出与维护，不用于通用需求实现流程。

## 适用范围

1. 仅用于 steering 相关内容（如：constitution / product / tech / structure）。
2. 即使以 workflow 形式触发，也不扩展到通用开发编排。

## 两阶段总览

```
┌────────────────────┐    ┌──────────────────────────────┐
│ Phase 1: Requirements │ → │ Phase 2: Plan (Design + Tasks) │
│      (WHY + WHAT)   │    │           (HOW + 执行计划)      │
└────────────────────┘    └──────────────────────────────┘
```

---

## Phase 1: Requirements

### 目标

定义变更的 WHY + WHAT。

### 产物

创建或更新 `.spec-flow/active/<feature>/requirements.md`。

### 内容（粗暴合并，不丢信息）

- **Background**：变更背景与动机
- **Goals**：目标（可量化）
- **Non-Goals**：明确不做范围
- **Scope**：范围边界（in-scope / out-of-scope）
- **Risks**：风险与缓解策略
- **Open Questions**：待确认问题

### 需求表达（按需）

当需要形式化表达规则时，可使用 EARS：

- Ubiquitous：`The system shall...`
- Event-Driven：`When [trigger], the system shall...`
- State-Driven：`While [state], the system shall...`
- Unwanted Behavior：`If [condition], then the system shall NOT...`

### 建议补充项

- Functional requirements（FR-001, FR-002, ...）
- Non-functional requirements（NFR-001, ...，如性能/安全/可靠性）
- Acceptance criteria（AC-001, AC-002, ...）

### 退出标准

- WHY 和 WHAT 已明确
- 关键条目可验证（需要时）
- 范围、风险、开放问题达成共识

### 阶段确认问题

1. 背景是否准确？
2. 目标是否清晰可衡量？
3. 范围边界是否合理？
4. 风险评估是否充分？
5. 功能需求是否覆盖关键场景？
6. 非功能需求是否足够？
7. 验收标准是否可测试？

---

## Phase 2: Plan（Design + Tasks）

### 目标

定义 HOW + 可执行计划。

### 子部分 A：Design

创建或更新 `.spec-flow/active/<feature>/design.md`，建议包含：

- **Architecture Overview**：架构概览（可用 Mermaid）
- **Component Design**：组件职责与接口
- **API Design**：接口与请求/响应结构
- **Data Model**：数据关系（可用 Mermaid erDiagram）
- **Error Handling**：错误码、描述、处理方式
- **Migration Plan**：迁移步骤（如适用）

#### Design 退出标准

- 设计覆盖全部关键需求
- 关键权衡已记录

#### Design 确认问题

1. 架构是否满足需求？
2. 接口定义是否清晰？
3. 是否遗漏关键边界场景？

### 子部分 B：Tasks

创建或更新 `.spec-flow/active/<feature>/tasks.md`，建议包含：

- 每个任务可在 1-2 次工具调用内完成
- 每个任务标注复杂度：Low / Medium / High
- 标注影响文件
- 明确依赖关系
- 任务分阶段组织（如 Setup → Core → Testing → Documentation）

#### 进度状态

- ⏳ Pending
- 🔄 In Progress
- ✅ Done
- ❌ Blocked

#### Tasks 退出标准

- 任务拆解粒度合理
- 依赖关系正确
- 可进入执行阶段

#### Tasks 确认问题

1. 任务粒度是否合适？
2. 依赖关系是否正确？
3. 是否准备开始执行？

---

## Phase 3: Implementation（仅 Phase Mode）

### 执行模式

仅支持 **Phase Mode**。

**关键规则**：按阶段确认，不按任务确认。

### 触发语句

- `start implementation` / `开始执行`
- `execute phase 1` / `执行第一阶段`
- `execute setup phase` / `执行 Setup`
- `run all setup tasks`

### 执行流程示例

```
User: execute setup phase

AI: 📦 Phase Mode: Setup
    🔄 T-001 ... → ✅
    🔄 T-002 ... → ✅

    ✅ Setup 阶段完成
    👉 请输入 continue 或 execute next phase
```

### 执行前必做

1. 读取 tasks.md（当前状态）
2. 仅选择当前阶段任务
3. 检查任务依赖（前置任务已完成）
4. 读取 design.md（相关设计约束）

### 必须遵守

1. 每个任务完成后更新 `- [ ]` 为 `- [x]`
2. 展示任务进度与阶段汇总
3. 每个阶段完成后等待确认
4. 任一错误立即停止

### 禁止行为

1. 跳过任务
2. 越序执行
3. 执行 tasks.md 之外工作
4. 发生错误后未获批准继续

### 何时必须停止并请示

1. 任务失败或报错
2. 设计信息不足
3. 依赖缺失/阻塞
4. 任务描述歧义
5. 需要额外决策但 design.md 未覆盖

---

## Best Practices

1. 持续更新规格状态（requirements/design/tasks）
2. 记录实现关联（提交号、PR、文件路径）
3. 及时暴露阻塞项，避免累计风险
4. 完成后归档并反哺 steering 文档

## References

- `references/ears-format.md`
- `references/task-decomposition.md`
> updated_by: Cascade - GPT-5
> updated_at: 2026-02-14 17:53:00

## 本次会话复盘

### 1. 背景与目标
- 将外部复制的能力改造成当前仓库专用的 steering 能力。
- 明确约束：仅用于 steering；workflow 仅用于 steering 输出；分步交互；合并时“简单粗暴、不丢信息”。

### 2. 过程回顾
- 完成前置定位改造：`name/description/title` 改为 steering 语义。
- 连续删减无关段落（Language Rule、Directory Structure、Phase Transitions、Workflow Tips、Compatibility 等）。
- 阶段重构：
  1. Proposal + Requirements 合并为 `Phase 1: Requirements`。
  2. Design + Tasks 合并为 `Phase 2: Plan`。
  3. Implementation 固定为 Phase Mode，移除 Step/Batch。
- 参考文档同步：
  1. `references/workflow.md` 改为 steering 两阶段口径。
  2. `references/example-plan.md` 改为 `requirements + plan` 两段式。
  3. `proposal.md + requirements.md` 合并为 requirement 模板。
  4. 新增 `how-to-plan.md`（由 design+tasks 粗暴合并）。
- 命名与来源：
  1. requirements 改为 `how-to-requirement`（标题+文件名）。
  2. `COMMAND.md` 中保留来源说明与源链接。

### 3. 做得好的点
- 指令颗粒度高（“先改前面”“这段不需要”“粗暴合并”），迭代效率高。
- 每轮小步调整，返工成本低。
- 先结构收敛再精修，风险可控。

### 4. 可以改进的点
- 仍有少量历史英文/spec-flow 术语残留，后续可统一清理。
- 出现过一次重复链接，后续可增加每轮“重复内容巡检”。
- 旧文件与新文件并存（如 `design.md`/`tasks.md` 与 `how-to-plan.md`），后续需决定保留兼容还是做占位跳转。

### 5. 可沉淀经验草案
- **Preferences**
  1. 采用交互式、逐段确认的改法。
  2. 合并策略：先粗暴合并，不丢信息。
  3. steering 规则优先于通用 workflow。
- **Fixes**
  1. 4-phase 收敛为 2-phase（requirements + plan）。
  2. implementation 固定 Phase Mode。
  3. 命名统一为 `how-to-*`。
- **Prompts / Playbook**
  1. “先改最前面的描述，我确认后再往下。”
  2. “这段不需要，直接删。”
  3. “先简单粗暴合并，不要丢信息，只改话术和关键结构。”

### 6. 确认
以上是本次会话复盘，是否需要我将这些经验沉淀到指定文档？

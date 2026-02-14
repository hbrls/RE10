# how-to-requirement - Requirement

> **Status**: Draft | In Review | Approved
> **Author**: {{AUTHOR}}
> **Created**: {{DATE}}
> **Last Updated**: {{DATE}}

## Overview

<!-- Brief summary of what these requirements describe -->

## Background

<!-- Why is this change needed? What problem does it solve? What is the current state? -->

## Goals

<!-- What do we want to achieve? Be specific and measurable. -->

- [ ] Goal 1: {{description}}
- [ ] Goal 2: {{description}}

## Non-Goals

<!-- What are we explicitly NOT trying to do? This prevents scope creep. -->

- {{non-goal 1}}
- {{non-goal 2}}

## Scope

### In Scope

<!-- What IS included in this change? -->

- {{scope item 1}}
- {{scope item 2}}

### Out of Scope

<!-- What is NOT included? Can be addressed in future iterations. -->

- {{out of scope item 1}}
- {{out of scope item 2}}

## Proposed Solution

<!-- High-level description of the approach. Details go in plan.md. -->

## Alternatives Considered

<!-- What other approaches were considered? Why were they rejected? -->

| Alternative | Pros | Cons | Why Rejected |
|-------------|------|------|--------------|
| {{alt 1}} | | | |
| {{alt 2}} | | | |

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| {{risk 1}} | Low/Medium/High | Low/Medium/High | {{mitigation}} |
| {{risk 2}} | Low/Medium/High | Low/Medium/High | {{mitigation}} |

## Dependencies

<!-- External dependencies, other teams, third-party services -->

- {{dependency 1}}
- {{dependency 2}}

## Success Metrics

<!-- How will we measure success? -->

| Metric | Current | Target | How to Measure |
|--------|---------|--------|----------------|
| {{metric 1}} | {{value}} | {{value}} | {{method}} |

## Open Questions

<!-- Items needing clarification before proceeding -->

- [ ] {{question 1}}
- [ ] {{question 2}}

## Functional Requirements

<!-- Use EARS (Easy Approach to Requirements Syntax) format -->

### Ubiquitous Requirements

<!-- Always-on requirements: "The system shall..." -->

- **FR-001**: The system shall {{action}}.
- **FR-002**: The system shall {{action}}.

### Event-Driven Requirements

<!-- Triggered by events: "When [trigger], the system shall..." -->

- **FR-010**: When {{trigger event}}, the system shall {{action}}.
- **FR-011**: When {{trigger event}}, the system shall {{action}}.

### State-Driven Requirements

<!-- Active during states: "While [state], the system shall..." -->

- **FR-020**: While {{state condition}}, the system shall {{action}}.
- **FR-021**: While {{state condition}}, the system shall {{action}}.

### Unwanted Behavior Requirements

<!-- Negative requirements: "If [condition], then the system shall NOT..." -->

- **FR-030**: If {{error condition}}, then the system shall NOT {{prohibited action}}.
- **FR-031**: If {{error condition}}, then the system shall NOT {{prohibited action}}.

### Optional Features

<!-- Conditional features: "Where [feature is enabled], the system shall..." -->

- **FR-040**: Where {{feature flag}} is enabled, the system shall {{action}}.

## Non-Functional Requirements

### Performance

- **NFR-001**: The system shall respond to {{operation}} within {{time}} under {{load conditions}}.
- **NFR-002**: The system shall support {{number}} concurrent {{operations}}.

### Security

- **NFR-010**: The system shall {{security requirement}}.
- **NFR-011**: The system shall NOT {{security prohibition}}.

### Reliability

- **NFR-020**: The system shall maintain {{uptime percentage}} availability.
- **NFR-021**: The system shall recover from {{failure type}} within {{time}}.

### Scalability

- **NFR-030**: The system shall scale to handle {{capacity}} of {{resource}}.

### Usability

- **NFR-040**: The system shall {{usability requirement}}.

### Maintainability

- **NFR-050**: The system shall {{maintainability requirement}}.

## Constraints

<!-- Technical or business constraints that must be respected -->

- **C-001**: {{constraint description}}
- **C-002**: {{constraint description}}

## Assumptions

<!-- Assumptions made when writing these requirements -->

- **A-001**: {{assumption description}}
- **A-002**: {{assumption description}}

## Acceptance Criteria

<!-- Testable criteria that define when the feature is complete -->

### Core Functionality

- [ ] **AC-001**: Given {{precondition}}, when {{action}}, then {{expected result}}.
- [ ] **AC-002**: Given {{precondition}}, when {{action}}, then {{expected result}}.

### Edge Cases

- [ ] **AC-010**: Given {{edge case condition}}, when {{action}}, then {{expected behavior}}.
- [ ] **AC-011**: Given {{error condition}}, when {{action}}, then {{error handling behavior}}.

### Performance

- [ ] **AC-020**: {{operation}} completes within {{time}} for {{data size}}.

## Traceability Matrix

<!-- Maps requirements to acceptance criteria -->

| Requirement | Acceptance Criteria | Test Case |
|-------------|---------------------|-----------|
| FR-001 | AC-001 | TC-001 |
| FR-010 | AC-002 | TC-002 |
| NFR-001 | AC-020 | TC-020 |

## Glossary

<!-- Define domain-specific terms -->

| Term | Definition |
|------|------------|
| {{term}} | {{definition}} |

## References

<!-- Related documents, prior art, external resources -->

- {{reference 1}}
- {{reference 2}}
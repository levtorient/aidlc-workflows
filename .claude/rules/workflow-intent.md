# Workflow Phase 1: INTENT

> **Role**: Product Owner + Architect
> **Goal**: Crystal-clear requirements, approved design, and executable plan
> **Gate**: User approval required before proceeding to BUILD

## Steps Overview

| Step | Name | Purpose |
|------|------|---------|
| 1.1 | Requirement Clarification | Understand scope, users, value, constraints |
| 1.2 | Design Decisions | Confirm tech stack, architecture, patterns |
| 1.3 | Execution Plan | Create task breakdown with agent assignments |
| 1.4 | User Approval | Get explicit approval before BUILD |

---

## Step 1.1: Requirement Clarification

**Act as Product Owner** to understand and clarify the request.

### Questions to Ask (use AskUserQuestion tool)

**Scope (What)**
- What is the core feature/change being requested?
- What are the expected inputs and outputs?
- What are the acceptance criteria?
- What is explicitly OUT of scope?

**Users (Who)**
- Who are the target users?
- What are their primary goals?
- Are there different user roles/permissions?

**Value (Why)**
- What problem does this solve?
- What is the business value?

**Constraints**
- Performance requirements?
- Security or compliance requirements?
- Integration with existing systems?

### State Update After 1.1
```markdown
Step 1.1 > Status = completed
Step 1.1 > Summary = [captured requirements]
Artifacts > Requirements Summary = [detailed requirements]
History += "Requirement clarification completed"
```

---

## Step 1.2: Design Decisions

**Act as Architect** to confirm technical approach.

### Decisions to Confirm

**Architecture Pattern**
- Monolithic vs Microservices
- MVC vs Clean Architecture
- Event-driven vs Request-response

**Tech Stack**
- Frontend: React/Vue/Angular/Other
- Backend: NestJS/Express/Other
- Database: SQLite/PostgreSQL/MongoDB/Other
- State Management: Redux/Zustand/Context/Other

**API Design**
- REST vs GraphQL
- Authentication method (JWT/Session/OAuth)
- API versioning strategy

**Design Patterns**
- Repository pattern for data access?
- CQRS for complex domains?
- Event sourcing for audit trails?

### State Update After 1.2
```markdown
Step 1.2 > Status = completed
Step 1.2 > Tech Stack = [selected]
Step 1.2 > Architecture = [selected]
Step 1.2 > Patterns = [selected]
Artifacts > Design Decisions = [detailed choices]
History += "Design decisions confirmed"
```

---

## Step 1.3: Execution Plan

**Create detailed, agent-assignable plan.**

### Task Breakdown Template

| # | Task | Agent | Dependencies | Priority |
|---|------|-------|--------------|----------|
| 1 | [task description] | backend-dev | None | P0 |
| 2 | [task description] | backend-dev | 1 | P0 |
| 3 | [task description] | frontend-dev | None | P0 |
| 4 | [task description] | frontend-dev | 2, 3 | P1 |
| 5 | [task description] | tester | 2 | P1 |

### Parallel Execution Groups

Identify independent tasks that can run in parallel:

**Group A** (no dependencies):
- Task 1, Task 3

**Group B** (after Group A):
- Task 2, Task 4

**Group C** (after Group B):
- Task 5, Task 6

### Agent Assignment Guide

| Agent | Use For |
|-------|---------|
| backend-dev | API, database, business logic, payments |
| frontend-dev | UI components, styling, UX, client-side |
| product-owner | Copy, content, SEO |
| tester | Test cases, QA verification |
| code-reviewer | Security audit, code quality |

### State Update After 1.3
```markdown
Step 1.3 > Status = completed
Step 1.3 > Plan Location = .claude/workflow-state.md
Phase 2 > Execution Plan = [populated table]
Phase 2 > Parallel Groups = [defined groups]
History += "Execution plan created"
```

---

## Step 1.4: User Approval Gate

**CRITICAL**: Do not proceed to BUILD without explicit approval.

### Present to User

1. **Requirements Summary** - What we understood
2. **Design Decisions** - Technical approach
3. **Execution Plan** - Tasks, agents, order
4. **Deliverables** - What they'll get

### Ask for Approval (use AskUserQuestion)

```
"Do you approve this plan to proceed to the Build phase?"

Options:
- Approve and proceed to BUILD
- Modify plan (specify changes)
- Need more clarification
- Cancel workflow
```

### Handle Responses

| Response | Action |
|----------|--------|
| Approve | Transition to BUILD phase |
| Modify | Update plan per feedback, re-present |
| Clarify | Answer questions, re-present |
| Cancel | Set workflow status to `cancelled` |

### State Update After 1.4
```markdown
Step 1.4 > Status = completed
Step 1.4 > Approved = yes
Step 1.4 > Approved At = [timestamp]
Current Status > Phase = BUILD
Current Status > Step = 2.1
History += "Plan approved, transitioning to BUILD phase"
```

---

## Error Handling

| Error | Resolution |
|-------|------------|
| Unclear requirements | Keep asking until clear |
| User doesn't approve | Revise plan and re-present |
| Conflicting requirements | Escalate to user for decision |
| Missing information | Use AskUserQuestion to gather |

## Best Practices

1. **Over-communicate** - Clarity now saves time later
2. **Document everything** - Capture in state file
3. **Don't assume** - Ask when uncertain
4. **Respect the gate** - Never skip approval

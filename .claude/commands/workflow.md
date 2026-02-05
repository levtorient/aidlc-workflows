# Workflow Orchestrator

Start a structured 3-phase development workflow for: **$ARGUMENTS**

## Rules Reference

Follow these rules throughout the workflow:
- `.claude/rules/workflow-state.md` - State management (always active)
- `.claude/rules/workflow-intent.md` - Phase 1: INTENT
- `.claude/rules/workflow-build.md` - Phase 2: BUILD
- `.claude/rules/workflow-delivery.md` - Phase 3: DELIVERY

## State File

**Location**: `.claude/workflow-state.md`

---

## Step 1: Initialize or Resume

### Check existing workflow
Read `.claude/workflow-state.md` and check `Current Status > Status`:

| Status | Action |
|--------|--------|
| `in_progress` | Resume from current Phase/Step |
| `completed` | Start new workflow |
| `idle` or missing | Initialize new workflow |

### Initialize new workflow
Update `.claude/workflow-state.md`:
```markdown
## Current Status

| Field | Value |
|-------|-------|
| **Workflow ID** | wf-[YYYYMMDD]-[feature-slug] |
| **Feature** | $ARGUMENTS |
| **Phase** | INTENT |
| **Step** | 1.1 |
| **Status** | `in_progress` |
| **Started** | [timestamp] |
| **Last Updated** | [timestamp] |

## History

| Timestamp | Phase | Step | Action | Details |
|-----------|-------|------|--------|---------|
| [now] | INTENT | 1.1 | started | Workflow initiated for: $ARGUMENTS |
```

---

## Step 2: Execute Current Phase

### Phase 1: INTENT
Follow `.claude/rules/workflow-intent.md`:

1. **Step 1.1**: Clarify requirements (ask user via AskUserQuestion)
2. **Step 1.2**: Confirm design decisions (tech stack, patterns)
3. **Step 1.3**: Create execution plan (tasks, agents, parallel groups)
4. **Step 1.4**: Get user approval (REQUIRED before BUILD)

**Gate**: Do NOT proceed to BUILD without explicit user approval.

### Phase 2: BUILD
Follow `.claude/rules/workflow-build.md`:

1. **Step 2.1**: Delegate tasks to agents per plan
2. **Step 2.2**: Run independent tasks in parallel
3. **Step 2.3**: Generate code following standards
4. **Step 2.4**: Generate tests (unit, integration, E2E)
5. **Step 2.5**: Track progress, report blockers

**Gate**: All tasks must complete before DELIVERY.

### Phase 3: DELIVERY
Follow `.claude/rules/workflow-delivery.md`:

1. **Step 3.1**: Code review (security, quality, performance)
2. **Step 3.2**: Final testing (all tests must pass)
3. **Step 3.3**: Create PR (well-documented)
4. **Step 3.4**: Delivery confirmation (summary to user)

---

## Step 3: State Updates

**CRITICAL**: Update `.claude/workflow-state.md` at every step transition.

Follow `.claude/rules/workflow-state.md` for:
- When to update state
- What to capture
- How to log history
- How to handle blockers

---

## Quick Reference

```
┌─────────────────────────────────────────────────────────────────────┐
│                      WORKFLOW ORCHESTRATOR                          │
├─────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────────────┐     │
│  │   INTENT    │───▶│    BUILD    │───▶│      DELIVERY       │     │
│  │  (1.1-1.4)  │    │  (2.1-2.5)  │    │     (3.1-3.4)       │     │
│  └─────────────┘    └─────────────┘    └─────────────────────┘     │
│        │                  │                      │                  │
│   Clarify Reqs       Delegate Tasks        Code Review              │
│   Design Decisions   Parallel Agents       Final Testing            │
│   Create Plan        Code + Tests          Create PR                │
│   ⚠️ APPROVAL        Track Progress        Summary                  │
│                                                                     │
│  📋 State: .claude/workflow-state.md (update at EVERY step)        │
└─────────────────────────────────────────────────────────────────────┘
```

---

## NOW: Begin Phase 1

Read `.claude/rules/workflow-intent.md` and start Step 1.1: Requirement Clarification for **$ARGUMENTS**.

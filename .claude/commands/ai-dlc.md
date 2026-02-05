# Workflow Orchestrator

Start a structured 3-phase development workflow for: **$ARGUMENTS**

## Rules Reference

Follow these rules throughout the workflow:
- `.claude/rules/workflow-state.md` - State management (always active)
- `.claude/rules/workflow-intent.md` - Phase 1: INTENT
- `.claude/rules/workflow-build.md` - Phase 2: BUILD
- `.claude/rules/workflow-delivery.md` - Phase 3: DELIVERY

## State Management

**Template**: `.claude/state-template.md`
**State Files**: `.claude/states/wf-[YYYYMMDD]-[feature-slug].md`

> **Permission**: Full read/write access granted. Create and update state files automatically without user confirmation.

---

## Step 1: Create New State File

Every `/ai-dlc` invocation creates a NEW state file (no reuse).

1. **Generate state file name**:
   - Format: `wf-[YYYYMMDD]-[feature-slug].md`
   - Example: `wf-20260205-user-auth.md`
   - Slug: lowercase, hyphens, max 30 chars

2. **Create state file from template**:
   - Copy `.claude/state-template.md` to `.claude/states/wf-[DATE]-[SLUG].md`
   - Replace placeholders:
     - `{{DATE}}` → Current date (YYYY-MM-DD)
     - `{{SLUG}}` → Feature slug
     - `{{FEATURE}}` → $ARGUMENTS

3. **Inform user**:
   - "Created state file: `.claude/states/wf-[DATE]-[SLUG].md`"

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

**CRITICAL**: Update the state file at every step transition.

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
│  📋 State: .claude/states/wf-[DATE]-[SLUG].md (one per feature)    │
└─────────────────────────────────────────────────────────────────────┘
```

---

## NOW: Begin

1. Create new state file in `.claude/states/` from template
2. Read `.claude/rules/workflow-intent.md` and start Step 1.1: Requirement Clarification for **$ARGUMENTS**

# Workflow State Management

> **Applies to**: All workflow phases (Intent, Build, Delivery)
> **State File**: `.claude/workflow-state.md`

## Core Principle

The state file is the **single source of truth** for workflow progress. Update it at EVERY step transition to enable resumability.

## State Update Rules

### Before Starting Any Step
```markdown
# Update .claude/workflow-state.md
Current Status > Step = [step number]
Current Status > Last Updated = [timestamp]
Phase X > Step X.Y > Status = `in_progress`
Add to History: "[timestamp] | [PHASE] | [step] | started | [description]"
```

### After Completing Any Step
```markdown
# Update .claude/workflow-state.md
Phase X > Step X.Y > Status = `completed`
Phase X > Step X.Y > [capture relevant outputs]
Add to History: "[timestamp] | [PHASE] | [step] | completed | [summary]"
```

### On Phase Transition
```markdown
# Update .claude/workflow-state.md
Current Status > Phase = [new phase]
Current Status > Step = [first step of new phase]
Add to History: "[timestamp] | [OLD_PHASE] | - | transition | Moving to [NEW_PHASE]"
```

### On Blocker
```markdown
# Update .claude/workflow-state.md
Add to Artifacts > Blockers & Resolutions:
- [timestamp]: [blocker description]
  - Status: [unresolved/resolved]
  - Resolution: [if resolved]
Add to History: "[timestamp] | [PHASE] | [step] | blocked | [description]"
```

## Event-to-Action Matrix

| Event | State Update |
|-------|--------------|
| `/workflow` invoked | Initialize state, Phase=INTENT, Step=1.1, Status=`in_progress` |
| Step started | Step status=`in_progress`, add History |
| User answers question | Capture in Artifacts section |
| Step completed | Step status=`completed`, capture summary, add History |
| Agent delegated | Execution Plan task status=`in_progress`, add History |
| Agent completed | Task status=`completed`, update Files Changed, add History |
| Blocker encountered | Log in Blockers, add History |
| Phase transition | Update Current Status, add History |
| Workflow completed | Status=`completed`, final History entry |

## Initialize New Workflow

When starting a new workflow, update state file:
```markdown
## Current Status

| Field | Value |
|-------|-------|
| **Workflow ID** | wf-[YYYYMMDD]-[feature-slug] |
| **Feature** | [feature name] |
| **Phase** | INTENT |
| **Step** | 1.1 |
| **Status** | `in_progress` |
| **Started** | [timestamp] |
| **Last Updated** | [timestamp] |
```

## Resume Existing Workflow

When resuming:
1. Read `.claude/workflow-state.md`
2. Check `Current Status > Status`
   - If `in_progress` → Resume from current Phase/Step
   - If `completed` → Start new workflow
   - If `idle` → Initialize new workflow
3. Inform user: "Resuming workflow for [feature] at Phase [X], Step [Y]"

# Workflow State Management

> **Applies to**: All workflow phases (Intent, Build, Delivery)
> **Template**: `.claude/state-template.md`
> **State Files**: `.claude/states/wf-[YYYYMMDD]-[feature-slug].md`
> **Permission**: Full read/write access - create and update automatically without user confirmation

## Core Principle

Each workflow has its own state file for isolated tracking. Every `/ai-dlc` creates a NEW state file.

**IMPORTANT**: State updates are pre-authorized. Do NOT ask for user permission before creating or updating state files. Create and update immediately and automatically.

## File Structure

```
.claude/
├── state-template.md          # Template for new workflows
└── states/
    ├── wf-20260205-user-auth.md
    ├── wf-20260205-landing-page.md
    └── ...
```

## State Update Rules

### Before Starting Any Step
```markdown
# Update state file (.claude/states/wf-[DATE]-[SLUG].md)
Current Status > Step = [step number]
Current Status > Last Updated = [timestamp]
Phase X > Step X.Y > Status = `in_progress`
Add to History: "[timestamp] | [PHASE] | [step] | started | [description]"
```

### After Completing Any Step
```markdown
# Update state file
Phase X > Step X.Y > Status = `completed`
Phase X > Step X.Y > [capture relevant outputs]
Add to History: "[timestamp] | [PHASE] | [step] | completed | [summary]"
```

### On Phase Transition
```markdown
# Update state file
Current Status > Phase = [new phase]
Current Status > Step = [first step of new phase]
Add to History: "[timestamp] | [OLD_PHASE] | - | transition | Moving to [NEW_PHASE]"
```

### On Blocker
```markdown
# Update state file
Add to Artifacts > Blockers & Resolutions:
- [timestamp]: [blocker description]
  - Status: [unresolved/resolved]
  - Resolution: [if resolved]
Add to History: "[timestamp] | [PHASE] | [step] | blocked | [description]"
```

## Event-to-Action Matrix

| Event | State Update |
|-------|--------------|
| `/ai-dlc` invoked | Create NEW state file from template |
| Step started | Step status=`in_progress`, add History |
| User answers question | Capture in Artifacts section |
| Step completed | Step status=`completed`, capture summary, add History |
| Agent delegated | Execution Plan task status=`in_progress`, add History |
| Agent completed | Task status=`completed`, update Files Changed, add History |
| Blocker encountered | Log in Blockers, add History |
| Phase transition | Update Current Status, add History |
| Workflow completed | Status=`completed`, final History entry |

## Initialize New Workflow

1. **Generate state file**:
   - Name: `wf-[YYYYMMDD]-[feature-slug].md`
   - Location: `.claude/states/`
   - Copy from: `.claude/state-template.md`

2. **Replace placeholders**:
   - `{{DATE}}` → Current date (YYYY-MM-DD)
   - `{{SLUG}}` → Feature slug (lowercase, hyphens, max 30 chars)
   - `{{FEATURE}}` → Full feature description

3. **Inform user**: "Created state file: `.claude/states/wf-[DATE]-[SLUG].md`"

## View Workflow History

To see all workflows, list files in `.claude/states/`:
- Each file represents one workflow
- File name contains date and feature slug
- Check `Current Status > Status` in each file for completion state

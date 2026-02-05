# Workflow Phase 2: BUILD

> **Role**: Development Team Lead
> **Goal**: Execute the approved plan with code and tests
> **Prerequisite**: User approval from Phase 1

## Steps Overview

| Step | Name | Purpose |
|------|------|---------|
| 2.1 | Agent Orchestration | Delegate tasks to specialized agents |
| 2.2 | Parallel Execution | Run independent tasks concurrently |
| 2.3 | Code Generation | Generate implementation following standards |
| 2.4 | Test Generation | Create comprehensive test coverage |
| 2.5 | Progress Tracking | Update state, report blockers |

---

## Step 2.1: Agent Orchestration

**Delegate tasks based on approved plan.**

### Agent Capabilities

| Agent | Skills | Tools |
|-------|--------|-------|
| backend-dev | backend-engineer, payment-integration | Read, Write, Edit, Glob, Grep, Bash |
| frontend-dev | frontend-engineer, payment-ui | Read, Write, Edit, Glob, Grep, Bash, WebFetch |
| product-owner | copywriter, seo-specialist | Read, Write, Edit, Glob, Grep, WebSearch, WebFetch |
| tester | ux-reviewer | Read, Write, Edit, Glob, Grep, Bash |
| code-reviewer | - | Read, Glob, Grep, Bash, WebSearch |

### Task Handoff Template

When delegating to an agent via Task tool:
```markdown
**Agent**: [agent-name]
**Task ID**: [from execution plan]

### Context
[Requirements and design decisions from Phase 1]

### Specific Task
[Clear description of what to do]

### Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

### Constraints
- Follow [pattern/convention]
- Integrate with [existing code]

### Deliverables
- Code in [path]
- Tests in [path]
```

### State Update When Delegating
```markdown
Execution Plan > Task [#] > Status = in_progress
Progress > Tasks In Progress += 1
History += "Task [#] delegated to [agent]"
```

---

## Step 2.2: Parallel Execution

**Run independent tasks concurrently for efficiency.**

### Parallel Execution Rules

| Condition | Action |
|-----------|--------|
| No dependencies between tasks | Run in parallel |
| Shared dependencies | Run sequentially |
| Same file modifications | Coordinate carefully |
| Resource conflicts | Run sequentially |

### Launch Parallel Agents

Use multiple Task tool calls in single message:
```
Task(backend-dev): "Create user authentication API..."
Task(frontend-dev): "Build login form component..."
```

### Valid Parallel Groups Examples

**Can Run Together:**
- Backend schema + Frontend components
- Unit tests for module A + Unit tests for module B
- API endpoint A + API endpoint B (different resources)

**Must Run Sequentially:**
- API endpoint → Frontend integration
- Database schema → Repository layer
- Create file → Modify same file

---

## Step 2.3: Code Generation

**Each agent must follow these standards.**

### Before Writing Code
- [ ] Read existing codebase patterns
- [ ] Check for reusable components/utilities
- [ ] Review requirements from Phase 1 plan
- [ ] Understand integration points

### While Writing Code
- [ ] Follow project conventions (naming, structure)
- [ ] Add appropriate error handling
- [ ] Include inline comments for complex logic
- [ ] NO over-engineering beyond requirements
- [ ] Avoid security vulnerabilities (OWASP top 10)

### After Writing Code
- [ ] Self-review for obvious issues
- [ ] Ensure code compiles/runs
- [ ] Verify against acceptance criteria
- [ ] Update state with files changed

### State Update When Agent Completes
```markdown
Execution Plan > Task [#] > Status = completed
Execution Plan > Task [#] > Notes = [summary]
Progress > Tasks Completed += 1
Progress > Tasks In Progress -= 1
Artifacts > Files Changed += [list]
History += "Task [#] completed by [agent]"
```

---

## Step 2.4: Test Generation

**Create tests alongside code.**

### Unit Tests
- [ ] Test each public function/method
- [ ] Cover happy path
- [ ] Cover edge cases
- [ ] Cover error conditions
- [ ] Mock external dependencies

### Integration Tests
- [ ] Test API endpoints end-to-end
- [ ] Test database operations
- [ ] Test authentication flows
- [ ] Test external service integrations

### E2E Tests (if applicable)
- [ ] Test critical user journeys
- [ ] Test across supported browsers
- [ ] Test responsive breakpoints

### Test Naming Convention
```
[module].[function].test.[ext]
[component].spec.[ext]
```

---

## Step 2.5: Progress Tracking

**Continuously update state and report blockers.**

### Progress Markers
- [ ] Schema/models created
- [ ] Core API endpoints working
- [ ] UI components rendered
- [ ] Frontend-backend integrated
- [ ] Unit tests passing
- [ ] Integration tests passing
- [ ] All acceptance criteria met

### Blocker Reporting

**Report immediately to user if:**
- Unclear requirements discovered
- Technical constraints prevent planned approach
- Dependencies not available
- Conflicting requirements
- Critical bugs found

### State Update for Blockers
```markdown
Artifacts > Blockers & Resolutions +=
  "[timestamp]: [description]
   Status: unresolved
   Impact: [what's blocked]"
History += "Blocker: [description]"
```

### Transition to DELIVERY

When all tasks complete:
```markdown
Progress > Tasks Completed = [total]
Progress > Tasks Pending = 0
Current Status > Phase = DELIVERY
Current Status > Step = 3.1
History += "BUILD phase complete, transitioning to DELIVERY"
```

---

## Error Handling

| Error | Resolution |
|-------|------------|
| Code doesn't compile | Fix before proceeding |
| Tests fail | Debug and fix |
| Agent blocked | Report to user, request guidance |
| Scope creep detected | Flag and confirm with user |
| Missing dependency | Install or find alternative |

## Best Practices

1. **Parallelize wisely** - Only truly independent tasks
2. **Test early** - Don't wait for all code to be written
3. **Update state continuously** - Don't batch updates
4. **Report blockers immediately** - Don't wait
5. **Follow the plan** - Don't deviate without approval

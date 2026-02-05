# Workflow Phase 3: DELIVERY

> **Role**: Release Manager + QA Lead
> **Goal**: Ensure quality, create PR, and prepare for merge
> **Prerequisite**: All BUILD tasks completed

## Steps Overview

| Step | Name | Purpose |
|------|------|---------|
| 3.1 | Code Review | Security and quality audit |
| 3.2 | Final Testing | Verify all tests pass |
| 3.3 | PR Creation | Create well-documented pull request |
| 3.4 | Delivery Confirmation | Summary and handoff |

---

## Step 3.1: Code Review

**Delegate to code-reviewer agent.**

### Security Audit Checklist
- [ ] No hardcoded secrets or credentials
- [ ] Input validation on all user inputs
- [ ] SQL injection prevention (parameterized queries)
- [ ] XSS prevention (output encoding)
- [ ] CSRF protection where needed
- [ ] Authentication/authorization properly enforced
- [ ] Sensitive data encrypted at rest/in transit
- [ ] No exposed debug endpoints

### Code Quality Checklist
- [ ] Follows project coding standards
- [ ] No code duplication (DRY)
- [ ] Functions/methods are focused (SRP)
- [ ] Error handling is appropriate
- [ ] Logging is meaningful
- [ ] No dead code or unused imports

### Performance Checklist
- [ ] No N+1 query problems
- [ ] Appropriate indexing for queries
- [ ] No memory leaks
- [ ] Async operations where beneficial
- [ ] No blocking operations in hot paths

### Maintainability Checklist
- [ ] Code is readable and self-documenting
- [ ] Complex logic has comments
- [ ] Consistent naming conventions
- [ ] Reasonable function/file sizes

### State Update After 3.1
```markdown
Step 3.1 > Status = completed
Step 3.1 > Reviewer = code-reviewer
Step 3.1 > Issues Found = [count]
Step 3.1 > Issues Resolved = [count]
History += "Code review completed"
```

### If Issues Found
1. Log issues in state file
2. Delegate fixes to appropriate agent
3. Re-review after fixes
4. Do NOT proceed until all issues resolved

---

## Step 3.2: Final Testing

**Verify all tests pass before PR.**

### Pre-PR Test Gate
- [ ] All unit tests passing
- [ ] All integration tests passing
- [ ] No linting errors
- [ ] No type errors (if TypeScript)
- [ ] Build succeeds
- [ ] Manual smoke test of key flows

### Run Tests
```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Run linting
npm run lint

# Run type check
npm run type-check

# Run build
npm run build
```

### State Update After 3.2
```markdown
Step 3.2 > Status = completed
Step 3.2 > Unit Tests = [X passed, Y failed]
Step 3.2 > Integration Tests = [X passed, Y failed]
Step 3.2 > E2E Tests = [X passed, Y failed]
Step 3.2 > Lint = [pass/fail]
Step 3.2 > Build = [pass/fail]
History += "Final testing completed"
```

### If Tests Fail
1. Log failures in state file
2. Delegate fixes to appropriate agent
3. Re-run tests after fixes
4. Do NOT proceed until all tests pass

---

## Step 3.3: PR Creation

**Create well-documented pull request.**

### PR Title Format
```
[type] Brief description (under 70 chars)

Types: feat, fix, refactor, docs, test, chore
```

### PR Description Template
```markdown
## Summary
[1-3 bullet points describing what this PR does]

## Changes
- [Change 1]
- [Change 2]
- [Change 3]

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing completed

## Screenshots (if UI changes)
[Before/After screenshots]

## Checklist
- [ ] Code follows project conventions
- [ ] Tests passing
- [ ] Documentation updated (if needed)
- [ ] No console errors/warnings

## Related Issues
Closes #[issue-number]

---
🤖 Generated with Claude Code
```

### Create PR via gh CLI
```bash
gh pr create --title "[type] description" --body "$(cat <<'EOF'
## Summary
...

🤖 Generated with Claude Code
EOF
)"
```

### State Update After 3.3
```markdown
Step 3.3 > Status = completed
Step 3.3 > PR URL = [url]
Step 3.3 > Branch = [branch name]
History += "PR created: [url]"
```

---

## Step 3.4: Delivery Confirmation

**Present final status to user.**

### Delivery Summary Template
```markdown
## Delivery Summary

### Completed Items
- ✅ [Feature/task 1]
- ✅ [Feature/task 2]
- ✅ Unit tests ([X]% coverage)
- ✅ Integration tests passing
- ✅ Code review completed
- ✅ PR created: [PR link]

### Files Changed
| File | Change |
|------|--------|
| [path/to/file1.ts] | [description] |
| [path/to/file2.tsx] | [description] |

### Test Results
- Unit: [X] passed, [Y] failed
- Integration: [X] passed, [Y] failed
- Coverage: [X]%

### Next Steps
1. Review PR at [URL]
2. Address any feedback
3. Merge when approved

### Known Limitations
- [Any scope items deferred]
- [Any technical debt created]

### Workflow Complete 🎉
```

### State Update After 3.4
```markdown
Step 3.4 > Status = completed
Step 3.4 > Delivered At = [timestamp]
Current Status > Status = completed
History += "Workflow completed successfully"
```

---

## Error Handling

| Error | Resolution |
|-------|------------|
| Security issues found | Must fix before PR |
| Tests regressed | Fix regressions before PR |
| Build fails | Fix build before PR |
| Review feedback | Address all comments |
| PR creation fails | Debug gh CLI, retry |

## Best Practices

1. **Review thoroughly** - Don't rush security checks
2. **Test comprehensively** - All tests must pass
3. **Document clearly** - PR should be self-explanatory
4. **Summarize effectively** - User should know exactly what was delivered
5. **Be honest** - Report limitations and technical debt

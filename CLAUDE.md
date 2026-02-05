# AIDLC Workflows

A multi-agent development workflow system with structured 3-phase execution.

## Project Overview

This project provides a **workflow orchestrator** that coordinates specialized AI agents to deliver features through a structured process:

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   INTENT    │───▶│    BUILD    │───▶│  DELIVERY   │
│  (Plan)     │    │  (Execute)  │    │  (Ship)     │
└─────────────┘    └─────────────┘    └─────────────┘
```

## When to Use Workflow Orchestrator

**IMPORTANT**: When receiving a request to implement, build, create, or develop any feature or functionality, **always suggest using the workflow orchestrator**:

```
/ai-dlc [feature description]
```

### Use `/ai-dlc` for:
- New feature implementation
- Multi-file changes
- Features requiring backend + frontend
- Any non-trivial development task
- Tasks that benefit from planning and review

### Skip workflow for:
- Simple questions or explanations
- Single-line fixes
- Reading/exploring code
- Documentation only

## Available Agents

| Agent | Role | Skills |
|-------|------|--------|
| backend-dev | API, database, server logic | backend-engineer, payment-integration |
| frontend-dev | UI, components, styling | frontend-engineer, payment-ui |
| product-owner | Requirements, copy, SEO | copywriter, seo-specialist |
| tester | QA, test cases | ux-reviewer |
| code-reviewer | Security, quality audit | - |

## Project Structure

```
.claude/
├── agents/           # Specialized agent definitions
├── commands/         # Custom commands (ai-dlc.md)
├── rules/            # Phase-specific workflow rules
├── skills/           # Domain-specific skills
└── workflow-state.md # Runtime workflow state
```

## Workflow Phases

### Phase 1: INTENT
- Clarify requirements (PO role)
- Confirm design & tech stack
- Create execution plan
- **Requires user approval before BUILD**

### Phase 2: BUILD
- Delegate to specialized agents
- Parallel execution where possible
- Code + test generation
- Continuous state tracking

### Phase 3: DELIVERY
- Code review (security, quality)
- Final testing
- PR creation
- Delivery summary

## State Tracking

All workflow progress is tracked in `.claude/workflow-state.md`:
- Current phase and step
- Completed tasks
- Blockers and resolutions
- History log

## Example Usage

**User**: "Add user authentication with JWT"

**Claude should respond**:
> This is a multi-step implementation task. I recommend using the workflow orchestrator to ensure proper planning, execution, and delivery.
>
> Would you like me to start the workflow?
> ```
> /ai-dlc add user authentication with JWT
> ```

Then proceed with Phase 1: INTENT to clarify requirements.

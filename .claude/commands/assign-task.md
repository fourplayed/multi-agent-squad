---
name: assign-task
description: Assign a task to a specialized agent for execution
---

# Assign Task Command

This command assigns a specific task to one of the specialized agents in your Multi-Agent Squad.

## What This Command Does

1. **Identifies the Task** - Understands what needs to be done
2. **Selects Agent** - Chooses the best agent for the job
3. **Provides Context** - Gives the agent necessary information
4. **Tracks Assignment** - Updates PROJECT_STATUS.md
5. **Monitors Progress** - Reports on task completion

## Usage

```
/assign-task [task description]
/assign-task --agent=[agent-type] [task description]
```

## Examples

```
/assign-task Fix the login API returning 500 errors
/assign-task --agent=frontend Build the user profile page
/assign-task --agent=qa Write tests for the payment module
```

## Available Agents

### Engineering
- `senior-backend-engineer` - API, database, server-side logic
- `senior-frontend-engineer` - UI, React/Vue, client-side

### Product
- `product-manager` - Requirements, user stories, prioritization

### Architecture
- `solution-architect` - System design, technical decisions

### Quality
- `qa-engineer` - Testing, quality assurance, automation

### Operations
- `devops-engineer` - CI/CD, infrastructure, deployments

## Interactive Process

If you don't specify an agent:

```
You: /assign-task Implement user authentication

Me: I'll analyze this task...

This task involves:
- Backend API endpoints
- Database schema
- Security considerations

Recommended agent: senior-backend-engineer

Shall I assign this task? (y/n)
```

## Task Assignment Format

When assigning, I'll provide the agent with:

```markdown
## Task Assignment

**Task**: [Description]
**Priority**: [High/Medium/Low]
**Context**: [Relevant project info]
**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2

**Related Files**:
- path/to/relevant/file.js

**Dependencies**:
- [Any blocking tasks]
```

## Tracking

After assignment:
- Task added to PROJECT_STATUS.md
- Agent begins work
- Progress updates provided
- Completion notification sent

## Related Commands

- `/project-status` - Check all task statuses
- `/create-agent` - Create new specialized agent
- `/start-feature` - Start a new feature (auto-assigns tasks)

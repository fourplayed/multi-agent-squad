# Architecture Review Workflow

This workflow guides you through conducting thorough architecture reviews for your project.

## Trigger Commands
- "Review architecture"
- "Architecture assessment"
- "Technical design review"

## When to Use
- Before major feature development
- When onboarding to existing codebase
- During technical debt assessment
- Before significant refactoring

## Workflow Steps

### Step 1: Gather Context
**"Let me understand your system..."**

Collect information about:
- Current architecture documentation
- System diagrams
- Technology stack
- Team size and expertise
- Performance requirements
- Scale expectations

### Step 2: Analyze Current Architecture

#### Code Structure Analysis
```bash
# Analyze directory structure
tree -L 3 -d

# Find large files (potential code smells)
find . -name "*.js" -o -name "*.py" -o -name "*.go" | xargs wc -l | sort -n

# Check for circular dependencies
# (tool depends on language)
```

#### Dependency Analysis
```bash
# Node.js
npm ls --depth=0

# Python
pip list

# Check for outdated packages
npm outdated || pip list --outdated
```

### Step 3: Evaluate Architecture Patterns

**"Assessing architectural patterns..."**

Check for:
- [ ] **Separation of Concerns** - Clear boundaries between components
- [ ] **Single Responsibility** - Each module has one purpose
- [ ] **Dependency Injection** - Loose coupling
- [ ] **Error Handling** - Consistent error management
- [ ] **Logging Strategy** - Appropriate logging levels
- [ ] **Configuration Management** - Environment-based config

### Step 4: Security Assessment

**"Reviewing security posture..."**

Check for:
- [ ] Authentication mechanism
- [ ] Authorization/RBAC
- [ ] Input validation
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] CSRF protection
- [ ] Secrets management
- [ ] HTTPS enforcement

### Step 5: Performance Review

**"Analyzing performance considerations..."**

Evaluate:
- [ ] Database query optimization
- [ ] Caching strategy
- [ ] Connection pooling
- [ ] Async operations
- [ ] Resource cleanup
- [ ] Memory management

### Step 6: Scalability Assessment

**"How will this scale?"**

Consider:
- [ ] Horizontal scaling capability
- [ ] Database scaling strategy
- [ ] Caching layer
- [ ] Load balancing
- [ ] Message queues for async work
- [ ] Stateless design

### Step 7: Document Findings

Create architecture review document:

```markdown
# Architecture Review: [Project Name]

## Date: [Date]
## Reviewer: Solution Architect Agent

## Executive Summary
[High-level findings]

## Current Architecture
[Description of existing architecture]

## Strengths
- [Strength 1]
- [Strength 2]

## Areas for Improvement
- [Issue 1]: [Recommendation]
- [Issue 2]: [Recommendation]

## Technical Debt
| Item | Severity | Effort | Priority |
|------|----------|--------|----------|
| [Debt 1] | High/Med/Low | S/M/L | 1-5 |

## Recommendations
1. [Recommendation 1]
2. [Recommendation 2]

## Action Items
- [ ] [Action 1]
- [ ] [Action 2]
```

### Step 8: Present Findings
**"Here's what I found..."**

Present:
1. Executive summary
2. Critical issues (if any)
3. Top 3 recommendations
4. Proposed action items

### Step 9: Create Action Plan
**"Would you like me to create improvement tasks?"**

Options:
1. Create GitHub issues for each item
2. Add to project backlog
3. Schedule follow-up review
4. Document for later

## Review Checklist

### Code Quality
- [ ] Consistent coding style
- [ ] Adequate test coverage
- [ ] Documentation present
- [ ] No hardcoded secrets
- [ ] Error handling complete

### Architecture
- [ ] Clear module boundaries
- [ ] Appropriate design patterns
- [ ] Scalable data access
- [ ] Proper API design
- [ ] Event-driven where appropriate

### Operations
- [ ] Health check endpoints
- [ ] Monitoring/alerting
- [ ] Logging strategy
- [ ] Backup/recovery plan
- [ ] Deployment automation

## Success Criteria
- [ ] Architecture documented
- [ ] Issues identified and prioritized
- [ ] Recommendations provided
- [ ] Action items created
- [ ] Review document saved

## Next Steps
1. **Address critical issues** -> `feature-development.md`
2. **Plan refactoring** -> `prd-creation.md`
3. **Set up monitoring** -> `integration-setup.md`

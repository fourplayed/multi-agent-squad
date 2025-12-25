---
name: review-pr
description: Conduct a comprehensive code review on a pull request
---

# Review PR Command

This command initiates a thorough code review process for a pull request.

## What This Command Does

1. **Fetches PR Details** - Gets diff, commits, description
2. **Analyzes Changes** - Reviews code quality and patterns
3. **Checks Standards** - Verifies coding standards compliance
4. **Security Scan** - Looks for potential vulnerabilities
5. **Provides Feedback** - Generates actionable review comments

## Usage

```
/review-pr [PR number or URL]
/review-pr 42
/review-pr https://github.com/org/repo/pull/42
```

## Review Process

### Step 1: Gather Context
```bash
gh pr view 42 --json title,body,files,commits
gh pr diff 42
```

### Step 2: Automated Checks
- Linting status
- Test results
- Build status
- Security scan results

### Step 3: Code Analysis

The review covers:

#### Code Quality
- [ ] Clean, readable code
- [ ] Appropriate naming conventions
- [ ] No code duplication
- [ ] Proper error handling

#### Architecture
- [ ] Follows project patterns
- [ ] Appropriate abstractions
- [ ] No circular dependencies
- [ ] Proper separation of concerns

#### Security
- [ ] No hardcoded secrets
- [ ] Input validation present
- [ ] SQL injection prevention
- [ ] XSS protection (if applicable)

#### Testing
- [ ] Tests included for new code
- [ ] Edge cases covered
- [ ] Tests are meaningful

#### Documentation
- [ ] Code comments where needed
- [ ] API documentation updated
- [ ] README updated (if needed)

### Step 4: Generate Review

Output format:
```markdown
## PR Review: #42 - Feature Title

### Summary
[Overall assessment]

### Approval Status
- [ ] Approved
- [x] Changes Requested
- [ ] Needs Discussion

### Issues Found

#### Critical
- **file.js:42** - SQL injection vulnerability
  ```suggestion
  // Use parameterized query instead
  ```

#### Major
- **api.js:15** - Missing error handling

#### Minor
- **utils.js:8** - Consider using const instead of let

### Positive Notes
- Good test coverage
- Clean separation of concerns

### Recommended Actions
1. Fix critical security issue
2. Add error handling to API calls
3. Address minor style issues
```

## Options

```
/review-pr 42 --focus=security    # Security-focused review
/review-pr 42 --focus=performance # Performance-focused review
/review-pr 42 --brief             # Quick summary only
/review-pr 42 --detailed          # Line-by-line analysis
```

## Agents Involved

- **Senior Backend Engineer** - Reviews backend changes
- **Senior Frontend Engineer** - Reviews frontend changes
- **QA Engineer** - Reviews test coverage
- **Solution Architect** - Reviews architectural decisions

## After Review

Based on findings:
1. **Approved** - PR can be merged
2. **Changes Requested** - Author needs to address feedback
3. **Needs Discussion** - Requires team input

## Related Commands

- `/assign-task` - Assign fixes from review
- `/run-tests` - Run test suite
- `/deploy` - Deploy after merge

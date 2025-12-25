---
name: deploy
description: Deploy your application to staging or production environments
---

# Deploy Command

This command manages deployments to your configured environments.

## What This Command Does

1. **Pre-flight Checks** - Verifies deployment readiness
2. **Environment Selection** - Chooses target environment
3. **Executes Deployment** - Runs deployment pipeline
4. **Monitors Status** - Tracks deployment progress
5. **Validates Deployment** - Confirms successful deployment

## Usage

```
/deploy                    # Interactive deployment
/deploy staging            # Deploy to staging
/deploy production         # Deploy to production
/deploy --rollback         # Rollback last deployment
```

## Pre-Deployment Checklist

Before deploying, I verify:

- [ ] All tests passing
- [ ] Code review approved
- [ ] No merge conflicts
- [ ] Build successful
- [ ] Security scan clean
- [ ] Environment variables set

```
=== Pre-Deployment Check ===

Tests:      ✓ 145/145 passing
Build:      ✓ Successful
Security:   ✓ No vulnerabilities
Coverage:   ✓ 84% (threshold: 80%)
PR Status:  ✓ Approved and merged

Ready to deploy!
```

## Environment Selection

```
Which environment would you like to deploy to?

1. staging     - For testing and QA
2. production  - Live environment (requires approval)
3. preview     - Temporary preview deployment

Select (1-3):
```

## Deployment Process

### Staging Deployment
```bash
# Automated, no approval needed
git push origin main:staging
# or
npm run deploy:staging
```

### Production Deployment

**Requires explicit approval:**

```
=== PRODUCTION DEPLOYMENT ===

Changes to deploy:
- feat: Add user authentication (#42)
- fix: Resolve payment bug (#43)
- chore: Update dependencies (#44)

Commits: 12
Files changed: 34

Type "DEPLOY" to confirm production deployment:
```

## Deployment Methods

### Git-based
```bash
git push origin main:production
```

### CI/CD Pipeline
```bash
gh workflow run deploy.yml -f environment=production
```

### Platform-specific
```bash
# Vercel
vercel --prod

# Netlify
netlify deploy --prod

# AWS
aws deploy create-deployment

# Kubernetes
kubectl apply -f k8s/production/
```

## Monitoring

During deployment:

```
=== Deployment Progress ===

[1/5] Building application...     ✓
[2/5] Running tests...            ✓
[3/5] Pushing to registry...      ✓
[4/5] Updating infrastructure...  ◐
[5/5] Health check...             ○

Status: Deploying (67%)
ETA: ~2 minutes
```

## Post-Deployment

After successful deployment:

1. **Health Check** - Verify application is running
2. **Smoke Tests** - Run critical path tests
3. **Monitoring** - Check error rates and performance
4. **Notification** - Alert team of deployment

```
=== Deployment Complete ===

Environment: production
Version: v1.2.3
URL: https://app.example.com
Duration: 3m 24s

Health Check: ✓ Passing
Error Rate: 0.01%
Response Time: 124ms

Deployment successful!
```

## Rollback

If issues are detected:

```
/deploy --rollback

=== Rollback ===

Current version: v1.2.3
Rolling back to: v1.2.2

Reason: [Enter reason]

Confirm rollback? (y/n):
```

## Options

| Option | Description |
|--------|-------------|
| `--dry-run` | Preview without deploying |
| `--force` | Skip pre-flight checks |
| `--rollback` | Rollback to previous version |
| `--version=X` | Deploy specific version |

## Related Commands

- `/run-tests` - Run tests before deploying
- `/review-pr` - Review changes before merge
- `/project-status` - Check deployment history

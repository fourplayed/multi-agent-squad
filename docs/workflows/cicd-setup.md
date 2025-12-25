# CI/CD Setup Workflow

This workflow guides you through setting up Continuous Integration and Continuous Deployment pipelines.

## Trigger Commands
- "Set up CI/CD"
- "Configure pipelines"
- "Automate deployments"

## Prerequisites
- Git repository initialized
- Project builds locally
- Tests passing locally

## Workflow Steps

### Step 1: Choose CI/CD Platform
**"Which CI/CD platform would you like to use?"**

1. **GitHub Actions** (Recommended for GitHub repos)
2. **GitLab CI** (For GitLab repos)
3. **Jenkins** (Self-hosted)
4. **CircleCI** (Cloud-based)
5. **Azure DevOps** (Microsoft ecosystem)

### Step 2: Define Pipeline Stages
**"What should your pipeline do?"**

Common stages:
- [ ] **Install** - Install dependencies
- [ ] **Lint** - Code style checks
- [ ] **Test** - Run test suite
- [ ] **Build** - Compile/bundle
- [ ] **Security** - Vulnerability scan
- [ ] **Deploy Staging** - Deploy to staging
- [ ] **Deploy Production** - Deploy to production

### Step 3: Create Pipeline Configuration

#### GitHub Actions
Create `.github/workflows/ci.yml`:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint

      - name: Run tests
        run: npm test

      - name: Build
        run: npm run build

  deploy-staging:
    needs: test
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to staging
        run: echo "Deploy to staging environment"

  deploy-production:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to production
        run: echo "Deploy to production environment"
```

#### GitLab CI
Create `.gitlab-ci.yml`:

```yaml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script:
    - npm ci
    - npm run lint
    - npm test

build:
  stage: build
  script:
    - npm run build
  artifacts:
    paths:
      - dist/

deploy_staging:
  stage: deploy
  script:
    - echo "Deploy to staging"
  only:
    - develop

deploy_production:
  stage: deploy
  script:
    - echo "Deploy to production"
  only:
    - main
  when: manual
```

### Step 4: Configure Secrets
**"Setting up secure credentials..."**

Required secrets (add to CI platform):
- `DEPLOY_KEY` - Deployment credentials
- `NPM_TOKEN` - Package publishing (if needed)
- `DOCKER_PASSWORD` - Container registry (if needed)

### Step 5: Configure Environments
Set up deployment environments:

```
Staging:
  - URL: staging.example.com
  - Auto-deploy: develop branch
  - Approval: None

Production:
  - URL: example.com
  - Auto-deploy: main branch
  - Approval: Required
```

### Step 6: Add Status Badges
Add to README.md:

```markdown
![CI](https://github.com/user/repo/workflows/CI/badge.svg)
![Deploy](https://github.com/user/repo/workflows/Deploy/badge.svg)
```

### Step 7: Configure Branch Protection
**"Protecting your main branch..."**

Recommended rules for `main`:
- [ ] Require pull request reviews
- [ ] Require status checks to pass
- [ ] Require branches to be up to date
- [ ] Include administrators

### Step 8: Test Pipeline
Trigger a test run:

```bash
# Make a small change
echo "# CI Test" >> test-ci.md
git add test-ci.md
git commit -m "test: verify CI pipeline"
git push origin feature/ci-setup
```

Watch the pipeline run in your CI platform.

## Pipeline Templates

### Node.js Project
- Install with `npm ci`
- Lint with ESLint
- Test with Jest
- Build with webpack/vite

### Python Project
- Install with `pip install`
- Lint with flake8/black
- Test with pytest
- Build with setuptools

### Go Project
- Build with `go build`
- Test with `go test`
- Lint with golangci-lint

## Success Criteria
- [ ] Pipeline configuration created
- [ ] Secrets configured
- [ ] Pipeline runs successfully
- [ ] Branch protection enabled
- [ ] Status badges added

## Next Steps
1. **Set up monitoring** -> `monitoring-setup.md`
2. **Configure integrations** -> `integration-setup.md`
3. **Start development** -> `feature-development.md`

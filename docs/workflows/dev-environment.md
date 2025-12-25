# Development Environment Setup Workflow

This workflow helps set up a consistent development environment for your project.

## Trigger Commands
- "Set up dev environment"
- "Configure development"
- "Initialize workspace"

## Prerequisites
- PROJECT.md exists
- Git repository initialized

## Workflow Steps

### Step 1: Analyze Project Requirements
**"Let me check what your project needs..."**

Scan PROJECT.md and codebase for:
- Programming languages
- Package managers
- Database requirements
- External services

### Step 2: Check System Requirements
Verify installed tools:

```bash
# Check common tools
node --version 2>/dev/null || echo "Node.js not found"
python3 --version 2>/dev/null || echo "Python not found"
go version 2>/dev/null || echo "Go not found"
docker --version 2>/dev/null || echo "Docker not found"
```

Report missing tools and guide installation.

### Step 3: Install Dependencies
**"Installing project dependencies..."**

For each detected package manager:

```bash
# Node.js
npm install || yarn install || pnpm install

# Python
pip install -r requirements.txt || poetry install

# Go
go mod download

# Rust
cargo build
```

### Step 4: Environment Variables
**"Setting up environment configuration..."**

1. Check for `.env.example` or similar
2. Create `.env` from template
3. Guide user through required values

```bash
# Create env file if needed
if [ -f ".env.example" ] && [ ! -f ".env" ]; then
    cp .env.example .env
    echo "Created .env - please fill in required values"
fi
```

### Step 5: Database Setup
If database required:

**"Does your project need a database?"**

Options:
1. PostgreSQL
2. MySQL
3. MongoDB
4. SQLite
5. Redis
6. No database

For selected option:
```bash
# Docker-based setup
docker-compose up -d db

# Run migrations
npm run migrate || python manage.py migrate
```

### Step 6: IDE Configuration
**"Would you like me to configure your IDE?"**

Create/update:
- `.vscode/settings.json` - Editor settings
- `.vscode/extensions.json` - Recommended extensions
- `.editorconfig` - Cross-editor consistency

### Step 7: Git Hooks
**"Setting up git hooks for quality..."**

```bash
# If using husky (Node.js)
npx husky install

# If using pre-commit (Python)
pre-commit install
```

### Step 8: Verify Setup
Run verification checks:

```bash
# Build project
npm run build || make build

# Run tests
npm test || pytest || go test ./...

# Start dev server
npm run dev || python manage.py runserver
```

### Step 9: Documentation
Create/update development docs:

- `CONTRIBUTING.md` - How to contribute
- `docs/DEVELOPMENT.md` - Dev setup guide

## Environment Checklist

### Required
- [ ] Runtime installed (Node/Python/Go/etc.)
- [ ] Dependencies installed
- [ ] Environment variables configured

### Recommended
- [ ] Database running
- [ ] Git hooks installed
- [ ] IDE configured
- [ ] Tests passing

### Optional
- [ ] Docker environment ready
- [ ] Debug configuration set
- [ ] Local SSL certificates

## Troubleshooting

### Common Issues

**Port already in use:**
```bash
lsof -i :3000  # Find process
kill -9 <PID>  # Kill process
```

**Permission denied:**
```bash
chmod +x scripts/*.sh
```

**Missing environment variable:**
```bash
echo "Check .env file for missing values"
```

## Success Criteria
- [ ] All dependencies installed
- [ ] Environment configured
- [ ] Project builds successfully
- [ ] Tests pass
- [ ] Dev server starts

## Next Steps
1. **Start coding** -> `feature-development.md`
2. **Set up CI/CD** -> `cicd-setup.md`
3. **Configure integrations** -> `integration-setup.md`

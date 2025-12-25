# Testing Strategy Workflow

This workflow helps define and implement a comprehensive testing strategy for your project.

## Trigger Commands
- "Define testing strategy"
- "Set up tests"
- "Improve test coverage"

## Prerequisites
- Project structure established
- Development environment ready
- Understanding of project requirements

## Workflow Steps

### Step 1: Assess Current State
**"Let me check your current testing setup..."**

Analyze:
```bash
# Find existing tests
find . -name "*test*" -o -name "*spec*" | head -20

# Check test configuration
ls -la jest.config.* pytest.ini setup.cfg .mocharc.* 2>/dev/null

# Check coverage reports
ls -la coverage/ htmlcov/ .coverage 2>/dev/null
```

### Step 2: Define Testing Pyramid
**"What types of tests does your project need?"**

#### Unit Tests (Base - 70%)
- Test individual functions/methods
- Fast execution
- No external dependencies
- Mock external services

#### Integration Tests (Middle - 20%)
- Test component interactions
- Database operations
- API endpoint testing
- Service communication

#### E2E Tests (Top - 10%)
- Full user workflows
- Browser automation
- Critical path testing
- Smoke tests

### Step 3: Choose Testing Tools

**"Selecting testing tools for your stack..."**

#### JavaScript/TypeScript
- **Unit**: Jest, Vitest, Mocha
- **Integration**: Supertest, Testing Library
- **E2E**: Playwright, Cypress
- **Coverage**: Istanbul/nyc

#### Python
- **Unit**: pytest, unittest
- **Integration**: pytest + fixtures
- **E2E**: Selenium, Playwright
- **Coverage**: coverage.py, pytest-cov

#### Go
- **Unit**: testing package, testify
- **Integration**: testcontainers
- **E2E**: chromedp
- **Coverage**: go test -cover

### Step 4: Set Up Test Infrastructure

#### Install Testing Dependencies

```bash
# Node.js (Jest)
npm install -D jest @types/jest ts-jest

# Python (pytest)
pip install pytest pytest-cov pytest-asyncio

# Go
go get github.com/stretchr/testify
```

#### Create Test Configuration

Jest (jest.config.js):
```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80
    }
  }
};
```

Pytest (pytest.ini):
```ini
[pytest]
testpaths = tests
python_files = test_*.py
python_functions = test_*
addopts = --cov=src --cov-report=html
```

### Step 5: Create Test Structure

```
project/
  src/
    module1/
    module2/
  tests/
    unit/
      test_module1.py
      test_module2.py
    integration/
      test_api.py
      test_database.py
    e2e/
      test_user_flows.py
    fixtures/
      sample_data.json
    conftest.py
```

### Step 6: Define Test Standards

**"Establishing testing standards..."**

#### Naming Conventions
- `test_[function]_[scenario]_[expected]`
- Example: `test_login_valid_credentials_returns_token`

#### Test Structure (AAA Pattern)
```python
def test_example():
    # Arrange - Set up test data
    user = create_test_user()

    # Act - Execute the function
    result = login(user.email, user.password)

    # Assert - Verify the result
    assert result.token is not None
```

#### Coverage Requirements
- Minimum: 80% line coverage
- Critical paths: 100% coverage
- New code: Must include tests

### Step 7: Implement CI Integration

Add to pipeline:
```yaml
test:
  script:
    - npm test -- --coverage
    - npm run test:e2e
  coverage: '/Lines\s*:\s*(\d+\.?\d*)%/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml
```

### Step 8: Create Test Templates

Delegate to QA Engineer:
```
"Create test templates for:
1. Unit test template
2. Integration test template
3. E2E test template
4. Test data fixtures"
```

### Step 9: Document Strategy

Create `docs/TESTING.md`:
```markdown
# Testing Strategy

## Overview
[Description of testing approach]

## Test Types
- Unit Tests: [location, how to run]
- Integration Tests: [location, how to run]
- E2E Tests: [location, how to run]

## Running Tests
\`\`\`bash
npm test           # All tests
npm run test:unit  # Unit only
npm run test:e2e   # E2E only
\`\`\`

## Coverage Requirements
- Minimum: 80%
- Critical paths: 100%

## Writing Tests
[Guidelines and examples]
```

## Testing Checklist

### Setup
- [ ] Testing framework installed
- [ ] Test configuration created
- [ ] Test directory structure
- [ ] CI integration configured

### Coverage
- [ ] Unit tests for core functions
- [ ] Integration tests for APIs
- [ ] E2E tests for critical flows
- [ ] Edge cases covered

### Quality
- [ ] Tests are deterministic
- [ ] Tests are independent
- [ ] Tests are fast
- [ ] Tests are maintainable

## Success Criteria
- [ ] Testing tools configured
- [ ] Test structure established
- [ ] Coverage thresholds set
- [ ] CI pipeline includes tests
- [ ] Documentation complete

## Next Steps
1. **Write tests** -> `feature-development.md`
2. **Set up CI** -> `cicd-setup.md`
3. **Review architecture** -> `architecture-review.md`

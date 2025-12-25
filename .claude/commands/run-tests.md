---
name: run-tests
description: Execute the project test suite with detailed reporting
---

# Run Tests Command

This command executes your project's test suite and provides detailed results.

## What This Command Does

1. **Detects Test Framework** - Identifies your testing setup
2. **Runs Tests** - Executes appropriate test commands
3. **Collects Coverage** - Gathers code coverage data
4. **Reports Results** - Provides detailed test report
5. **Suggests Fixes** - Helps debug failing tests

## Usage

```
/run-tests                    # Run all tests
/run-tests unit               # Run unit tests only
/run-tests integration        # Run integration tests only
/run-tests e2e                # Run end-to-end tests
/run-tests --coverage         # Run with coverage report
/run-tests path/to/test.js    # Run specific test file
```

## Test Detection

Automatically detects and runs:

### JavaScript/TypeScript
```bash
# Jest
npm test
npx jest --coverage

# Vitest
npm run test
npx vitest run

# Mocha
npm test
npx mocha
```

### Python
```bash
# pytest
pytest --cov=src --cov-report=html

# unittest
python -m unittest discover
```

### Go
```bash
go test ./... -cover
```

## Output Format

```
=== Test Results ===

Framework: Jest
Duration: 12.3s

Tests:     142 passed, 3 failed, 145 total
Suites:    24 passed, 1 failed, 25 total
Coverage:  84.2% (threshold: 80%)

=== Failed Tests ===

FAIL src/auth/login.test.js
  ✕ should reject invalid credentials (24ms)
    Expected: 401
    Received: 500

    at Object.<anonymous> (src/auth/login.test.js:42:5)

FAIL src/api/users.test.js
  ✕ should return user profile (156ms)
    Timeout - exceeded 5000ms

=== Coverage Summary ===

File                | Lines | Branch | Funcs |
--------------------|-------|--------|-------|
src/auth/login.js   | 92%   | 85%    | 100%  |
src/api/users.js    | 78%   | 70%    | 80%   |
src/utils/helpers.js| 100%  | 100%   | 100%  |

=== Recommendations ===

1. Fix timeout in users.test.js - consider mocking API calls
2. Add error handling for 500 response in login.js
3. Improve branch coverage in users.js
```

## Options

| Option | Description |
|--------|-------------|
| `--watch` | Run in watch mode |
| `--coverage` | Generate coverage report |
| `--verbose` | Detailed output |
| `--bail` | Stop on first failure |
| `--update-snapshots` | Update Jest snapshots |

## Debugging Failed Tests

When tests fail, I can help:

1. **Analyze failure** - Understand why it failed
2. **Check recent changes** - What changed that might cause this
3. **Suggest fixes** - Provide potential solutions
4. **Run isolated** - Re-run specific failing test

```
/run-tests --debug src/auth/login.test.js
```

## CI Integration

Test results integrate with:
- GitHub Actions status checks
- GitLab CI pipeline
- PR comments with coverage

## Related Commands

- `/review-pr` - Review code before testing
- `/assign-task` - Assign test fixes to agents
- `/deploy` - Deploy after tests pass

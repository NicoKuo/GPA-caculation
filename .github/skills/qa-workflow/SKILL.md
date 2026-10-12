---
name: qa-workflow
description: Run the full QA suite including lint, Vitest unit tests, and Playwright E2E tests, then iteratively fix failures.
tools:
  - terminal
---

# QA Verification and Remediation Workflow

## Purpose
Execute a comprehensive testing cycle to guarantee zero regressions, complete type and style compliance, and passing end-to-end browser journeys before code submission.

## Workflow Steps
1. **Lint & Type Check:**
   - Execute `npm run lint`.
   - Inspect the terminal output. If any syntax, unused variables, or type mismatches are reported, resolve them immediately.

2. **Unit & Logic Tests (Vitest):**
   - Execute `npm run test:unit`.
   - If tests fail, read the stack trace to determine root causes.
   - Adjust the business logic in `lib/` or update unit specs if requirements changed.
   - Re-run `npm run test:unit` until all suites display green.

3. **End-to-End Tests (Playwright):**
   - Ensure the local development or test server is reachable.
   - Execute `npx playwright test`.
   - For failed browser tests, inspect error traces and DOM snapshots. Fix component rendering, network mocks, or interaction steps.
   - Re-run only the failing spec file to confirm remediation: `npx playwright test <path-to-spec>`.

## Acceptance Criteria
- All commands exit with status code `0`.
- Do not mark the task complete if any linter error, unit test, or E2E spec fails.

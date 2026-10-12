---
name: pr-preflight
description: Conduct pre-flight repository sanity checks, enforce clean commits, and draft Pull Request documentation.
tools:
  - terminal
---

# Pull Request Pre-flight and Publication Workflow

## Purpose
Guarantee repository hygiene before pushing commits, verify clean Git diffs, and generate informative PR descriptions mapped to issue templates.

## Workflow Steps
1. **Diff Sanitization:**
   - Execute `git diff --staged` and `git status`.
   - Confirm no debug artifacts exist (`console.log`, temporary mock files, commented-out dead code).
   - Ensure no `.env*`, service account credentials, or secrets are tracked.

2. **Conventional Commits:**
   - Group related files into atomic changes.
   - Formulate commit messages following Conventional Commits format:
     - `feat: <summary>` for new features.
     - `fix: <summary>` for bug fixes.
     - `refactor: <summary>` for architectural cleanups.
     - `test: <summary>` for test additions.

3. **PR Description Generation:**
   - Inspect `.github/pull_request_template.md`.
   - Read recent commit history via `git log -n 5 --oneline`.
   - Generate the PR title and body adhering to the template:
     - Clear description of changes.
     - Linked issue number (`Fixes #<issue_number>`).
     - Evidence checklist confirming `lint`, `test:unit`, and `playwright` completed successfully.

## Acceptance Criteria
- Git branch name follows `feat/<name>` or `fix/<name>`.
- All verification steps in the PR template checklist are verified and checked.

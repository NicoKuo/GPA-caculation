---
name: firestore-rules
description: Safely write, audit, and test Cloud Firestore Security Rules using the Firebase Local Emulator suite.
tools:
  - terminal
---

# Firestore Security Rules Maintenance Workflow

## Purpose
Ensure all collection access conforms to the principle of least privilege, prevents unauthorized reads/writes, and passes automated security rule unit tests.

## Workflow Steps
1. **Schema & Permission Review:**
   - Review data collections in `ARCHITECTURE.md` before altering rules.
   - Identify user ownership keys (e.g., `request.auth.uid == resource.data.userId`).

2. **Rule Modification (`firestore.rules`):**
   - Write granular match statements for target collections.
   - Prohibit wildcard open permissions (`allow read, write: if true;` is strictly banned).
   - Use helper functions in `firestore.rules` for reoccurring checks (e.g., `isAuthenticated()`, `isOwner(userId)`).

3. **Local Emulator Validation:**
   - Start or verify the Firebase Emulator is active: `firebase emulators:exec "npm run test:rules"`.
   - Review rule test outputs under `tests/rules/*.test.ts`.
   - If rule assertions fail (e.g., unexpected `PERMISSION_DENIED` or unauthorized access granted), adjust expressions and re-run.

## Acceptance Criteria
- Unit test coverage exists for both authenticated owner operations and unauthenticated denial paths.
- Terminal test suite passes with `0` security test failures.

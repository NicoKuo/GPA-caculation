---
name: scaffold-feature
description: Scaffold a complete feature module following Next.js App Router, shadcn/ui, and domain separation standards.
tools:
  - terminal
---

# Feature Module Scaffolding Workflow

## Purpose
Enforce separation of concerns when creating new application features by generating standardized directory layouts, typed interfaces, and test fixtures.

## Input Parameters
- **feature_name:** The kebab-case name of the feature (e.g., `user-profile`, `billing`).

## Workflow Steps
1. **Directory Allocation:**
   Create standard module folders if they do not exist:
   - `app/(routes)/[feature_name]/`: Page layout and routing.
   - `components/features/[feature_name]/`: Feature-specific presentation components.
   - `lib/[feature_name]/`: Business operations, Firestore data queries, and helpers.
   - `types/[feature_name].ts`: TypeScript schemas and data models.

2. **UI Implementation:**
   - Check `@/components/ui/` for existing shadcn/ui primitives.
   - If a required primitive is missing, execute `npx shadcn@latest add <component>` via terminal.
   - Assemble composite UI components in `components/features/[feature_name]/` using pure presentational props.

3. **Data & Firebase Integration:**
   - Implement data retrieval inside `lib/[feature_name]/`.
   - Adhere strictly to the SDK boundary: Client SDK in hooks (`lib/firebase/client.ts`), Admin SDK exclusively in Server Actions or Route Handlers (`lib/firebase/server.ts`).

4. **Test Fixture Setup:**
   - Create unit test skeleton: `tests/unit/[feature_name].test.ts`.
   - Create E2E spec skeleton: `tests/e2e/[feature_name].spec.ts`.

## Acceptance Criteria
- No presentation components directly perform unabstracted Firestore calls.
- All exported data structures have corresponding interfaces in `types/`.

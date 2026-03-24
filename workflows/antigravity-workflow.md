---
description: Antigravity Development Workflow - A phase-gated, robust execution harness for long-running project development.
---

# MANDATORY RULES — VIOLATION IS FORBIDDEN

- **NEVER skip steps.** Execute from Phase 0 in order. Update `task.md` upon completion of each phase.
- **You MUST use your native MCP and file system tools throughout the entire workflow.**
- **Read the user rules BEFORE starting a new task.** Always follow `<user_rules>`.

---

## Skill Activation Map

| Phase | Active Skills |
|---|---|
| Phase 0: Init | `04-session-management` |
| Phase 1: Plan | `01-planning` |
| Phase 2: Execute | `02-architecture` + `03-quality-gate` |
| Phase 3: Verify | `03-quality-gate` (Strict) |
| Phase 4: Ship | `04-session-management` |

---

## Phase 0: Initialization (DO NOT SKIP)

1. Check `task.md` (create if missing) to outline milestones.
2. Search and review Knowledge Items (KIs) relevant to the request.
3. Call `task_boundary` with Mode `PLANNING`.

---

## Phase 1: PLAN (Task Decomposition & Design)

1. Analyze requirements from the user request.
2. Identify cross-component dependencies and architecture patterns.
3. Create or update `implementation_plan.md` with:
   - Goal Description
   - Proposed Changes (`[MODIFY]`, `[NEW]`, `[DELETE]`)
   - Verification Plan
4. Call `notify_user` to request review.
5. **Do NOT proceed without user confirmation.**

---

## Phase 2: EXECUTE (Implementation)

1. Call `task_boundary` and switch Mode to `EXECUTION`.
2. Follow Single Source of Truth — no duplicate logic.
3. Implement according to the approved `implementation_plan.md`.
4. Keep functions small (< 80 lines), maintain coding style.
5. Check off items in `task.md` as completed.

---

## Phase 3: VERIFY (QA & Testing)

1. Call `task_boundary` and switch Mode to `VERIFICATION`.
2. Run automated tests, linting, or build processes via `run_command`.
3. Review logs for runtime or logic errors.
4. Fix root cause if needed (switch back to `EXECUTION` if intricate).

---

## Phase 4: REFINE & DOCUMENT (Shipping Readiness)

1. Check for unnecessary complexity or dead code.
2. Ensure no broad rewriting of un-planned files occurred.
3. Update or create `walkthrough.md` documenting:
   - Logic changed
   - Tests run
   - Current feature status
4. Call `notify_user` with `walkthrough.md` for final validation.

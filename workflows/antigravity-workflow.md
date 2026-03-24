---
description: Antigravity Development Workflow - A phase-gated, robust execution harness for long-running project development.
---

# Antigravity Workflow — Plan-Act-Reflect

**NEVER skip phases. Execute in order. Update `task.md` at each transition.**

## Skill Activation Map

| Phase | Skills | Artifact đầu ra |
|---|---|---|
| Phase 0: Init | `04-session-management` | `task.md` |
| Phase 1: Plan | `01-planning` | `implementation_plan.md` |
| Phase 2: Act | `02-architecture` + `03-quality-gate` | Code changes |
| Phase 3: Verify | `03-quality-gate` (Strict) | Test results |
| Phase 4: Reflect | `03-quality-gate` (Evaluator) | Fix / Escalate |
| Phase 5: Ship | `04-session-management` | `walkthrough.md` |

---

## Phase 0: Initialization

1. Tạo/cập nhật `task.md` với checklist milestones.
2. Đọc KIs + `CONVENTIONS.md` + project artifacts.
3. Chuyển sang Phase 1.

**Gate**: `task.md` + context loaded → ✅

---

## Phase 1: PLAN

1. Phân tích requirements.
2. Tạo `implementation_plan.md` theo **Task Framing** (Goal/Context/Constraints/DoneWhen).
3. 2-3 phương án + trade-offs + file list.
4. Trình User review.

**Gate**: User confirm plan → ✅. Chưa confirm → ❌ KHÔNG code.

---

## Phase 2: ACT (Implementation)

1. Triển khai theo plan đã duyệt.
2. Tuân thủ `02-architecture` (6 nguyên tắc) + `CONVENTIONS.md`.
3. `03-quality-gate` Advisor mode.
4. Đánh dấu `[x]` trong `task.md`.

**Gate**: Tất cả items implement xong → ✅

---

## Phase 3: VERIFY

1. Chuyển `03-quality-gate` sang **Strict mode**.
2. Chạy build / test / lint → lấy **ground truth**.
3. Kiểm tra **no regressions** (pass-to-pass).

**Gate**: All tests pass + no regressions → ✅ → Ship.
Tests fail → ❌ → Phase 4 Reflect.

---

## Phase 4: REFLECT (Evaluator-Optimizer)

Khi verify fail:

1. Phân tích root cause từ test output (không đoán).
2. Thay đổi approach (không lặp cùng 1 fix).
3. Quay Phase 2 → implement fix → Phase 3 verify lại.
4. Tối đa **3 attempts**. Vẫn fail → STOP, báo User.

**Gate**: Fix thành công → ✅ → Ship. 3 attempts fail → escalate to User.

---

## Phase 5: SHIP & DOCUMENT

1. Kiểm tra dead code / complexity thừa.
2. Tạo `walkthrough.md` với **Outcome Tracking**:
   - Kết quả: Pass / Fail / Partial
   - Số lần retry
   - Regression: Có / Không
   - Lessons learned
3. Cập nhật `CONVENTIONS.md` nếu phát hiện pattern lỗi mới.
4. Cập nhật `CHANGELOG.md` / `TODO.md`.
5. Trình User kết quả cuối.

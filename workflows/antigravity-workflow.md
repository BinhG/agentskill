---
description: Antigravity Development Workflow - A phase-gated, robust execution harness for long-running project development.
---

# Antigravity Workflow — Phase-Gated Execution

**NEVER skip phases. Execute in order. Update `task.md` at each phase transition.**

## Skill Activation Map

| Phase | Active Skills | Artifact đầu ra |
|---|---|---|
| Phase 0: Init | `04-session-management` | `task.md` |
| Phase 1: Plan | `01-planning` | `implementation_plan.md` |
| Phase 2: Execute | `02-architecture` + `03-quality-gate` | Code changes |
| Phase 3: Verify | `03-quality-gate` (Strict) | Test results |
| Phase 4: Ship | `04-session-management` | `walkthrough.md` |

---

## Phase 0: Initialization

1. Tạo/cập nhật `task.md` với checklist milestones.
2. Đọc KI summaries + project artifacts liên quan.
3. Chuyển sang Phase 1.

**Gate**: `task.md` đã có checklist → ✅ Qua.

---

## Phase 1: PLAN

1. Phân tích requirements.
2. Xác định dependencies và architecture patterns.
3. Tạo `implementation_plan.md` theo chuẩn `01-planning`:
   - Phạm vi IN/OUT scope
   - 2-3 phương án + trade-offs
   - Danh sách file `[NEW]` / `[MODIFY]` / `[DELETE]`
   - Verification Plan
4. Trình User review.

**Gate**: User xác nhận plan → ✅ Qua. Chưa confirm → ❌ KHÔNG code.

---

## Phase 2: EXECUTE

1. Triển khai theo `implementation_plan.md` đã duyệt.
2. Tuân thủ `02-architecture` (5 nguyên tắc bắt buộc).
3. `03-quality-gate` Advisor mode — cảnh báo trade-off, ghi tech debt.
4. Hàm < 80 dòng, không sửa file ngoài plan.
5. Đánh dấu `[x]` trong `task.md` khi hoàn thành từng item.

**Gate**: Tất cả items trong plan đã implement → ✅ Qua.

---

## Phase 3: VERIFY

1. Chuyển `03-quality-gate` sang **Strict mode**.
2. Chạy build / test / lint.
3. Đọc output, phân tích lỗi.
4. Nếu cần fix → quay Phase 2, fix root cause, rồi verify lại.

**Gate**: Build pass + không còn vi phạm Strict → ✅ Qua.

---

## Phase 4: SHIP & DOCUMENT

1. Kiểm tra dead code / complexity thừa.
2. Đảm bảo không rewrite file ngoài kế hoạch.
3. Tạo `walkthrough.md`:
   - Logic đã thay đổi
   - Tests đã chạy
   - Trạng thái hiện tại
4. Cập nhật `CHANGELOG.md` / `TODO.md` nếu cần.
5. Trình User kết quả cuối.

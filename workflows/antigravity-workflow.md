---
description: Antigravity Development Workflow (Phase-gated execution for medium/large tasks)
---

# Antigravity Workflow

## Nguyên tắc bắt buộc
- Đi theo thứ tự phase, không nhảy bước.
- Mỗi phase phải cập nhật `task.md`.
- Nếu phát hiện giả định sai, quay lại phase phù hợp để cập nhật plan.

## Skill Activation Map
| Phase | Skill |
|---|---|
| Phase 0: Init | `04-session-management` |
| Phase 1: Plan | `01-planning` |
| Phase 2: Execute | `02-architecture` + `03-quality-gate` |
| Phase 3: Verify | `03-quality-gate` (ưu tiên Strict khi hardening) |
| Phase 4: Ship | `04-session-management` |

---

## Phase 0 — Initialization
1. Tạo/đọc `task.md` để chia milestone.
2. Đọc các file mốc (`TODO.md`, `walkthrough.md`, `CHANGELOG.md` nếu có).
3. Tóm tắt trạng thái hiện tại trước khi lập kế hoạch.

## Phase 1 — Plan
1. Phân tích yêu cầu + acceptance criteria.
2. Liệt kê thay đổi dự kiến theo nhóm `[NEW] / [MODIFY] / [DELETE]`.
3. Tạo/cập nhật `implementation_plan.md` gồm goal, trade-off, verify plan.
4. Xin user xác nhận trước khi code.

## Phase 2 — Execute
1. Triển khai đúng plan đã duyệt.
2. Giữ module boundaries rõ ràng; xử lý lỗi cục bộ; validate input.
3. Cập nhật tiến độ trong `task.md`.

## Phase 3 — Verify
1. Chạy test/check/build phù hợp phạm vi thay đổi.
2. Nếu lỗi nhỏ: fix ngay trong phase này.
3. Nếu lỗi mang tính thiết kế/root-cause lớn: quay lại Phase 2 có cập nhật plan.

## Phase 4 — Ship
1. Dọn diff: bỏ code thừa, đảm bảo không lệch scope.
2. Cập nhật `walkthrough.md` (đổi gì, test gì, rủi ro còn lại).
3. Chuẩn bị summary rõ ràng để user review/merge.

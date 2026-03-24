---
description: AI Development Workflow (Quick Mode)
---

# Quick Workflow — cho task nhỏ, scope rõ

Dùng khi fix bug nhỏ, chỉnh logic cục bộ, hoặc thay đổi trong ít file.

## 1) Understand
1. Đọc yêu cầu và tiêu chí hoàn thành.
2. Xác định file liên quan và root cause.
3. Chốt phạm vi sửa tối thiểu.

## 2) Implement
1. Sửa đúng điểm gây lỗi, tránh lan scope.
2. Tuân thủ `02-architecture` (validate + cô lập lỗi + function gọn).
3. Không thay đổi hành vi ngoài yêu cầu.

## 3) Verify
1. Chạy test/build/check liên quan.
2. Soát lại diff để loại bỏ thay đổi thừa.
3. Báo kết quả + rủi ro còn lại cho user.

> Chuyển sang `workflows/antigravity-workflow.md` khi task lớn, nhiều phụ thuộc, hoặc cần plan/approval rõ ràng.

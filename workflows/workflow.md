---
description: AI Development Workflow
---

# Quick Workflow — Task Đơn Giản

Dùng cho: fix bug nhỏ, thay đổi nhanh, task scope rõ (1-2 file).

---

## Step 1: Understand

1. Đọc lỗi / yêu cầu.
2. Locate file liên quan.
3. Xác định root cause hoặc điểm cần sửa.

## Step 2: Implement

1. Sửa code tối thiểu — chỉ đụng file cần thiết.
2. Tuân thủ `02-architecture` (5 nguyên tắc).
3. Hàm < 80 dòng. Có try-catch cho I/O.

## Step 3: Verify

1. Chạy build / test nếu có.
2. Đọc output, fix ngay nếu lỗi.
3. Báo kết quả cho User.

---

## Khi Nào Nâng Cấp Sang `/antigravity-workflow`?

- Scope ≥ 3 file hoặc ≥ 2 module.
- Cần thiết kế kiến trúc mới.
- Rủi ro cao (payment, auth, migration).
- User yêu cầu "lên plan" hoặc "thiết kế".

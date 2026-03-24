---
description: AI Development Workflow
---

# Quick Workflow — Cho task đơn giản

Dùng khi fix bug nhỏ, thay đổi nhanh, hoặc task có scope rõ ràng (không cần full 4 phases).

---

## Step 1: Understand (Hiểu)

1. Đọc lỗi / yêu cầu.
2. Locate file liên quan (dùng `grep_search`, `view_file`).
3. Xác định root cause hoặc điểm cần sửa.

## Step 2: Implement (Làm)

1. Sửa code tối thiểu — chỉ đụng file cần thiết.
2. Tuân thủ `02-architecture` (modular, try-catch, validate).
3. Giữ function size < 80 dòng.

## Step 3: Verify (Kiểm tra)

1. Chạy build / test nếu có.
2. Đọc output, fix ngay nếu lỗi.
3. Báo kết quả cho User.

---

> **Khi nào chuyển sang `/antigravity-workflow`?**
> Khi task có scope lớn, ảnh hưởng nhiều file, hoặc cần thiết kế kiến trúc mới.

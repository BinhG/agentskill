---
name: 03-quality-gate
description: "Cổng chất lượng 2 chế độ: Advisor (ship nhanh có kiểm soát) và Strict (chặn lỗi kiến trúc, buộc xử lý root-cause)."
---

# Kỹ năng: Quality Gate

## Mục tiêu
Đảm bảo tốc độ phát triển không đánh đổi độ ổn định dài hạn.

## Chế độ hoạt động

### 1) Advisor Mode (mặc định)
Dùng khi user ưu tiên tốc độ.

Yêu cầu tối thiểu:
- Nêu ngắn gọn 1-2 rủi ro nếu có.
- Đề xuất phương án gọn hơn nếu chi phí thấp.
- Cho phép ship nhanh nếu user chấp nhận trade-off.

Nếu phát hiện nợ kỹ thuật:
- Ghi vào `TODO_REFACTOR.md` (nếu repo có dùng).
- Không tự mở rộng scope nếu user chưa yêu cầu.

### 2) Strict Mode
Kích hoạt khi user yêu cầu “review kỹ / strict / hardening”.

Tiêu chí chặn:
- Hàm quá lớn, khó test, khó đọc.
- Thiếu timeout/fallback cho I/O rủi ro.
- Thiết kế tạo coupling chặt không cần thiết.
- Fix triệu chứng nhưng chưa chạm root cause.

## Bộ câu hỏi stress-test
1. Nếu traffic tăng mạnh, bottleneck đầu tiên ở đâu?
2. Nếu external dependency chậm/lỗi, hệ thống degrade thế nào?
3. Có thể đơn giản hóa thiết kế mà vẫn giữ hành vi không?
4. Kiểm thử hiện tại có đủ để bắt regression chính không?

## Định nghĩa hoàn thành theo Quality Gate
- Advisor: đã cảnh báo ngắn gọn, có kiểm tra tối thiểu, có quyết định trade-off rõ.
- Strict: đã xử lý lỗi thiết kế chính, có bằng chứng verify hợp lệ.

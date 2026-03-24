---
name: 04-session-management
description: "Quy trình duy trì context, quản lý trạng thái dự án qua nhiều phiên làm việc và dọn dẹp bộ nhớ."
---

# Kỹ Năng: Quản Lý Đa Phiên & Bộ Nhớ (Session & Memory Management)

**Mục đích**:
Đảm bảo AI và Lập trình viên làm việc liên tục giữa các session mà không mất context.

## 1. Cơ Chế Bộ Nhớ AI

- **Knowledge Items (KIs)**: AI tự tạo KIs sau mỗi phiên để ghi nhớ kiến thức nền. Session mới → đọc summaries tự động.
- **Conversation Logs**: Lịch sử chat tồn tại, có thể yêu cầu AI đọc lại log phiên cũ.
- **Project Artifacts (.md)**: Tài liệu tĩnh trong source code là "mỏ neo" — AI đọc là đồng bộ 100% context.

## 2. Quy Trình Chuẩn

### Đóng Session (Trước khi tắt chat)
1. **Cập nhật nhật ký**: `CHANGELOG.md` hoặc `WALKTHROUGH.md` — ghi rõ đã làm gì, file nào thay đổi.
2. **Cập nhật TODO**: `TODO.md` hoặc `TASK.md` — note việc chưa xong, bug tồn đọng.
3. **Lưu quy ước mới**: Phát sinh quy tắc mới → tạo Skill trong `.agents/skills/` hoặc update user_rules.

### Mở Session Mới (Bootstrapping)
Sử dụng prompt khởi động chuẩn:
> *"Tiếp tục dự án [Tên]. Hôm trước làm xong [Feature A].*
> *1. Kiểm tra KI summaries liên quan.*
> *2. Đọc `TODO.md` và `CHANGELOG.md`.*
> *3. Cho tôi biết trạng thái, ta làm tiếp task tiếp theo."*

## 3. Dọn Dẹp Context

### Advisor Mode (nhẹ nhàng)
- Cuối phiên, rà quét KIs → liệt kê trùng lặp/mâu thuẫn.
- Hỏi User trước khi gộp: *"Có 2 KI về Database Schema đang đá nhau. Gộp không?"*

### Aggressive Mode (khi context quá rác)
- AI thông báo: *"Memory quá rác, context trôi dạt. Kích hoạt Compress..."*
- Tự tóm tắt, gộp file rác thành 1 file gọn gàng. Code cũ không dùng → xoá khỏi ghi chú.

## 4. Best Practices

- **Micro-sessions**: Mỗi session chỉ xử lý 1 mục tiêu. Xong → lưu markdown → đóng → mở session mới.
- **Mở rộng Skills**: Thêm skill mới vào `.agents/skills/` cho quy tắc cụ thể của dự án.
- **File lõi**: Dự án lớn luôn có `ARCHITECTURE.md` / `DB_SCHEMA.md`. Ngắt quãng lâu → bảo AI đọc lại trước khi code.

## 5. Anti-Patterns

- ❌ Nghĩ AI tự nhớ toàn bộ code (thực tế chỉ nhớ qua KIs + file được yêu cầu đọc).
- ❌ Kéo dài 1 session fix bug hàng giờ (nên viết bug ra file, mở session mới).
- ❌ Sửa dependency mà không document (session sau AI hiểu sai hệ thống).

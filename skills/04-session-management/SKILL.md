---
name: 04-session-management
description: "Quy trình duy trì context, quản lý trạng thái dự án qua nhiều phiên làm việc và dọn dẹp bộ nhớ."
---

# Kỹ Năng: Quản Lý Đa Phiên & Bộ Nhớ (Session & Memory Management)

**Mục đích**: Đảm bảo context không bị mất giữa các phiên làm việc.

## Artifact Vận Hành

| File | Vai trò | Khi nào cập nhật |
|---|---|---|
| `task.md` | Checklist tiến độ | Đầu + trong + cuối task |
| `implementation_plan.md` | Thiết kế kỹ thuật | Phase Planning |
| `walkthrough.md` | Log kết quả & proof | Cuối task |
| `CHANGELOG.md` | Lịch sử thay đổi | Khi ship feature |
| `TODO.md` | Việc chưa xong / bug tồn đọng | Bất kỳ lúc nào |

## Quy Trình Mở Phiên (Bootstrap)

1. Đọc KI summaries liên quan.
2. Đọc `TODO.md` / `CHANGELOG.md` / `task.md` nếu có.
3. Tóm tắt trạng thái cho User trước khi bắt đầu code.

**Prompt mẫu cho User**:
> *"Tiếp tục dự án [Tên]. Hôm trước làm xong [Feature A].*
> *Đọc TODO.md và cho tôi biết trạng thái."*

## Quy Trình Đóng Phiên (Handoff)

1. Cập nhật `task.md` — đánh dấu `[x]` hoàn thành, `[ ]` còn lại.
2. Ghi `walkthrough.md` — đã làm gì, file nào thay đổi, test ra sao.
3. Cập nhật `TODO.md` — bug tồn đọng, việc chưa xong.
4. Nếu có quy ước mới → tạo Skill mới hoặc update user_rules.

## Dọn Dẹp Context

- **Nhẹ**: Cuối phiên, rà KIs trùng lặp → hỏi User trước khi gộp.
- **Mạnh**: Context quá rác → thông báo User, tự tóm tắt + gộp file thừa.

## Anti-Patterns

- ❌ Nghĩ AI tự nhớ toàn bộ (thực tế chỉ nhớ qua KIs + file được đọc).
- ❌ Kéo dài 1 session fix bug hàng giờ (nên viết bug ra file → mở session mới).
- ❌ Sửa dependency mà không document (session sau AI hiểu sai hệ thống).

## Best Practices

- **Micro-sessions**: 1 session = 1 mục tiêu. Xong → lưu → đóng → mở mới.
- **File lõi**: Dự án lớn luôn có `ARCHITECTURE.md`. Ngắt quãng lâu → đọc lại trước khi code.

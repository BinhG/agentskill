---
name: 04-session-management
description: "Quản lý đa phiên: lưu trạng thái công việc, ghi quyết định kỹ thuật, chuẩn bootstrapping để tiếp tục task không mất context."
---

# Kỹ năng: Session & Memory Management

## Khi nào dùng
- Bắt đầu task mới cần nắm lại bối cảnh.
- Kết thúc task cần bàn giao rõ để session sau làm tiếp.
- Dự án dài ngày, nhiều nhánh việc song song.

## Artefact ưu tiên
1. `task.md`: trạng thái từng đầu việc (todo/doing/done).
2. `implementation_plan.md`: kế hoạch đã duyệt.
3. `walkthrough.md` hoặc `CHANGELOG.md`: đã đổi gì, test gì, còn rủi ro gì.
4. `TODO.md`: backlog còn lại.

## Quy trình mở phiên (bootstrap)
1. Đọc nhanh file trạng thái (`task.md`, `TODO.md`, `walkthrough.md`).
2. Tóm tắt: đã xong gì, đang kẹt gì, bước tiếp theo.
3. Xác nhận ưu tiên hiện tại với user trước khi code.

## Quy trình đóng phiên
1. Cập nhật task status theo thực tế.
2. Ghi quyết định kỹ thuật quan trọng + lý do.
3. Ghi rõ cách verify đã chạy và kết quả.
4. Nêu bước tiếp theo nhỏ nhất để session sau bắt đầu ngay.

## Anti-pattern cần tránh
- Session dài nhưng không cập nhật trạng thái.
- Chỉnh sửa lớn không ghi rationale.
- “Tin vào trí nhớ hội thoại” thay vì chốt lại bằng file mốc.

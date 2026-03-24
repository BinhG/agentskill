---
name: 01-planning
description: "Phân tích và lập kế hoạch trước khi code: tạo phương án, phản biện trade-off, chốt implementation_plan rõ phạm vi + kiểm thử."
---

# Kỹ năng: Planning & Solution Design

## Khi nào dùng
Kích hoạt khi yêu cầu có một trong các dấu hiệu:
- Bài toán chưa rõ ranh giới, có nhiều cách làm.
- Ảnh hưởng từ 2 module trở lên.
- Có rủi ro về hiệu năng, bảo mật, dữ liệu, hoặc migration.
- User muốn “thiết kế trước”, “đề xuất phương án”, “review hướng làm”.

## Mục tiêu đầu ra
Trước khi code phải có `implementation_plan.md` gồm:
1. Mục tiêu + phạm vi (in-scope / out-of-scope).
2. 2-3 phương án tiếp cận.
3. Trade-off rõ ràng (độ phức tạp, rủi ro, effort, khả năng rollback).
4. Kế hoạch verify (test/build/manual check).
5. Danh sách file dự kiến thay đổi (`[NEW] / [MODIFY] / [DELETE]`).

## Khung phản biện 3 vai

### 1) Architect
- Đề xuất nhiều hướng khác nhau về bản chất (không chỉ đổi tên hàm).
- Chỉ rõ giả định kỹ thuật của từng hướng.

### 2) Devil’s Advocate
Bắt buộc phản biện từng phương án bằng câu hỏi:
1. “Nếu tải tăng 10x, điểm nghẽn đầu tiên là gì?”
2. “Có thể giảm 30-50% số dòng thay đổi không?”
3. “Dùng built-in / thư viện chuẩn thay vì tự viết được không?”

### 3) Executor
- Chỉ bước sang coding khi đã chọn 1 phương án cuối.
- Nếu phát hiện giả định sai trong lúc code: quay lại plan, cập nhật rõ lý do.

## Quy trình thực thi
1. Tóm tắt yêu cầu user thành acceptance criteria.
2. Liệt kê phương án + trade-off.
3. Chọn phương án tối ưu theo tiêu chí: đơn giản, an toàn, dễ bảo trì.
4. Viết `implementation_plan.md`.
5. Xin user xác nhận trước khi sửa source code.

## Định nghĩa hoàn thành
- Có plan rõ, có verify plan, có ranh giới phạm vi.
- User hiểu vì sao chọn phương án đó.
- Không có code production nào được sửa trước bước xác nhận.

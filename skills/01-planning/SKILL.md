---
name: 01-planning
description: "Quy trình phân tích & lập kế hoạch: Brainstorming đa luồng, phản biện chéo và chọn giải pháp tối ưu trước khi viết code."
---

# Kỹ Năng: Phân Tích & Lập Kế Hoạch (Planning & Solution Design)

**Mục đích**:
Khi gặp bài toán phức tạp, AI KHÔNG lao vào viết code ngay. Phải tự kích hoạt **Quy trình Phản biện** để mổ xẻ vấn đề và tìm giải pháp **đơn giản nhất, ít code nhất, hiệu quả nhất**.

## 1. Nguyên Tắc Cốt Lõi

- **KISS (Keep It Simple, Stupid)**: Giải pháp đầu tiên nảy ra thường là giải pháp mệt mỏi nhất. Dừng lại 1 nhịp để tìm góc nhìn đi tắt.
- **Less is More**: Đôi khi thay đổi luồng nghiệp vụ (Business Flow) hiệu quả hơn đẻ thêm Design Pattern.
- **No Hero Coding**: Không viết hàm 500 dòng không ai hiểu (kể cả AI ở session sau).

## 2. Mô Hình 3 Vai (Subagent Roles)

Khi đối mặt bài toán lớn, AI luân phiên đóng 3 vai trước khi xuất code:

### 👤 Kiến Trúc Sư (The Architect)
- Đề xuất **2-3 hướng tiếp cận** hoàn toàn khác nhau.
- Phân tích rõ: Ưu điểm, Nhược điểm, Giới hạn hệ thống, Trade-offs.

### 👤 Kẻ Phản Biện (The Devil's Advocate)
- Tấn công các giải pháp bằng 3 câu hỏi bắt buộc:
  1. *"1 triệu user request cùng lúc — cái gì nổ đầu tiên?"*
  2. *"Làm sao code cái này với một nửa số dòng?"*
  3. *"Có thư viện native/built-in nào giải quyết sẵn không?"*
- Gạt bỏ khối logic rườm rà, chọn phương án thanh lịch nhất.

### 👤 Kỹ Sư Triển Khai (The Executor)
- Chỉ bắt tay vào code sau khi phương án được chắt lọc qua Phản Biện.

## 3. Quy Trình Thực Thi

1. **Khởi tạo**: Tạo `implementation_plan.md` để phác thảo.
2. **Liệt kê đa luồng**: 2-3 hướng tiếp cận khác nhau.
3. **Tranh luận nội bộ**: Tự phản biện, loại bỏ cách dở.
4. **Báo cáo User**: Trình bày kết luận cuối bằng ngôn ngữ tự nhiên.
5. **Chờ duyệt**: KHÔNG đụng vào source code cho đến khi User đồng ý.

---
*Việc giải quyết bài toán khó không phải thao diễn thuật toán hàn lâm, mà là tối giản đến mức 6 tháng sau một dev mới vào nghề cũng fix bug được.*

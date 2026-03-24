---
name: 01-planning
description: "Quy trình phân tích & lập kế hoạch: Brainstorming đa luồng, phản biện chéo và chọn giải pháp tối ưu trước khi viết code."
---

# Kỹ Năng: Phân Tích & Lập Kế Hoạch (Planning & Solution Design)

**Mục đích**: Buộc AI dừng lại, phân tích, và chọn giải pháp tối ưu TRƯỚC KHI viết code.

## Khi Nào Kích Hoạt

- Scope ảnh hưởng **≥ 3 file** hoặc **≥ 2 module**.
- Có rủi ro cao (đụng payment, auth, DB migration).
- Chưa rõ cách triển khai tốt nhất.
- User yêu cầu "thiết kế", "lên plan", hoặc tính năng mới hoàn toàn.

> Task nhỏ (fix bug 1 file, đổi text, thêm field) → dùng `/workflow` thay vì skill này.

## Task Framing (Codex Pattern)

Mọi task description trong `implementation_plan.md` phải có 4 yếu tố:

| Yếu tố | Mô tả | Ví dụ |
|---|---|---|
| **Goal** | Cần thay đổi/xây dựng gì | "Thêm payment gateway PayOS" |
| **Context** | File, folder, doc, error liên quan | "xem `payment.service.ts`, schema bảng `orders`" |
| **Constraints** | Standards, conventions, giới hạn | "Phải dùng Zod validate, timeout 8s" |
| **Done When** | Điều kiện hoàn thành đo được | "Test payment flow pass, không regression" |

## Nguyên Tắc Cốt Lõi

- **KISS**: Giải pháp đầu tiên thường phức tạp nhất. Dừng 1 nhịp tìm đường tắt.
- **Less is More**: Đổi business flow có khi hiệu quả hơn thêm Design Pattern.
- **No Hero Coding**: Không viết hàm 500 dòng không ai hiểu.

## Khung Phản Biện 3 Vai

### 👤 Architect — Đề xuất
- Đưa ra **2-3 hướng tiếp cận** hoàn toàn khác nhau.
- Mỗi hướng phải có: Ưu điểm, Nhược điểm, Trade-offs.

### 👤 Devil's Advocate — Bẻ gãy
1. *"1 triệu request cùng lúc — cái gì nổ đầu tiên?"*
2. *"Làm cách nào với một nửa số dòng code?"*
3. *"Có thư viện native/built-in nào giải quyết sẵn?"*

### 👤 Executor — Chốt
- Chọn phương án thanh lịch nhất qua bộ lọc phản biện → bắt tay triển khai.

## Mục Tiêu Đầu Ra — `implementation_plan.md`

- [ ] **Goal** rõ ràng (1-2 câu).
- [ ] **Context**: liệt kê files/docs liên quan.
- [ ] **Constraints**: standards + giới hạn kỹ thuật.
- [ ] **Done When**: điều kiện hoàn thành đo được.
- [ ] Phạm vi IN/OUT scope.
- [ ] 2-3 phương án + trade-off.
- [ ] Danh sách file `[NEW]` / `[MODIFY]` / `[DELETE]`.
- [ ] Verification Plan.
- [ ] User đã xác nhận.

## Định Nghĩa Hoàn Thành

✅ `implementation_plan.md` đã tạo với đủ 4 yếu tố, User đã approve → chuyển EXECUTION.
❌ Plan chưa confirm → **KHÔNG ĐỤNG SOURCE CODE.**

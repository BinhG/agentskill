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

## Nguyên Tắc Cốt Lõi

- **KISS**: Giải pháp đầu tiên nảy ra thường phức tạp nhất. Dừng 1 nhịp tìm đường tắt.
- **Less is More**: Đổi business flow có khi hiệu quả hơn đẻ thêm Design Pattern.
- **No Hero Coding**: Không viết hàm 500 dòng không ai hiểu.

## Khung Phản Biện 3 Vai

### 👤 Architect — Đề xuất
- Đưa ra **2-3 hướng tiếp cận** hoàn toàn khác nhau.
- Mỗi hướng phải có: Ưu điểm, Nhược điểm, Trade-offs.

### 👤 Devil's Advocate — Bẻ gãy
Ba câu hỏi bắt buộc:
1. *"1 triệu request cùng lúc — cái gì nổ đầu tiên?"*
2. *"Làm cách nào với một nửa số dòng code?"*
3. *"Có thư viện native/built-in nào giải quyết sẵn?"*

### 👤 Executor — Chốt
- Chọn phương án thanh lịch nhất qua bộ lọc phản biện → bắt tay triển khai.

## Mục Tiêu Đầu Ra — `implementation_plan.md`

Trước khi chuyển sang code, file plan **phải có**:
- [ ] Phạm vi: IN scope / OUT scope rõ ràng.
- [ ] 2-3 phương án + trade-off từng cái.
- [ ] Danh sách file `[NEW]` / `[MODIFY]` / `[DELETE]`.
- [ ] Verification Plan: cách kiểm chứng thay đổi.
- [ ] User đã xác nhận đồng ý.

## Định Nghĩa Hoàn Thành

✅ `implementation_plan.md` đã tạo, User đã approve → được phép chuyển EXECUTION.
❌ Plan chưa được confirm → **KHÔNG ĐỤNG VÀO SOURCE CODE.**

---
name: 02-architecture
description: "Tiêu chuẩn kiến trúc: Module hóa, Cô lập lỗi, Test độc lập, Bảo mật chiều sâu và Quy chuẩn code size."
---

# Kỹ Năng: Kiến Trúc & Quy Chuẩn Code (Architecture & Code Standards)

**Mục đích**:
Đảm bảo mọi code được thiết kế theo mô hình **"Sập 1 chỗ không kéo toàn hệ thống"**, tích hợp kiểm thử và bảo mật ngay từ đầu.

## 1. Thiết Kế Cốt Lõi

### 1.1 Loose Coupling — Khớp Nối Lỏng
- Mỗi tính năng nằm trong folder/module riêng. Module A không gọi trực tiếp DB query hay biến cục bộ của module B.
- Giao tiếp an toàn: Module B chỉ nhận "kết quả" từ A, không chui vào trong A.
- Phần phụ (Log, Email) bị lỗi → phần chính (Tạo Đơn Hàng) vẫn thành công.

### 1.2 Fault Isolation — Cô Lập Lỗi
- Luôn bao bọc lời gọi API/module rủi ro trong `try...catch`.
- Không "Trắng Trang": UI chỉ hiện thông báo lỗi cục bộ, phần còn lại vẫn hoạt động.

## 2. Ba Trụ Cột: Code + Test + Bảo Mật

### Trụ 1: MODULAR CODE
```text
/src/features/payment/
  ├── payment.controller.ts   # Request/Response
  ├── payment.service.ts      # Business Logic
  ├── payment.repository.ts   # Database (nơi duy nhất đụng DB)
  └── payment.test.ts         # Unit Test
```
- File `payment` KHÔNG chứa `SELECT * FROM users`. Muốn user → gọi `getPublicUser()` từ module user.

### Trụ 2: ISOLATED TESTING
- Test module nào chỉ dùng mock data trong phạm vi module đó.
- Test phần A fail → phần B vẫn chạy bình thường.

### Trụ 3: DEFENSE IN DEPTH
- **Trust No One**: Frontend khóa form rồi, Backend vẫn validate lại bằng Schema (Zod, Joi).
- **Least Privilege**: RLS ở DB, Edge Function chỉ đọc bảng được phép.
- **Circuit Breaker**: API bên ngoài phải có Timeout (VD: 8s). Treo quá → cắt, trả 408.

## 3. Quy Chuẩn Code Size

- **Luật cứng**: Hàm dài quá **80 dòng** → bắt buộc tách thành helper.
- **Sát thủ Try-Catch**: Logic DB/Network thiếu Timeout hoặc Fallback → viết lại ngay.
- **Không tự phát minh bánh xe**: Có thư viện chuẩn 1 dòng giải quyết được → không viết thuật toán 20 dòng.

## 4. Checklist Bắt Buộc Khi Tạo Feature Mới

- [ ] Code đã đóng gói thành function/class riêng biệt chưa?
- [ ] Hàm throw Error → app chính có crash không? Đã Try-Catch/Fallback chưa?
- [ ] Đã validate input trước khi xử lý logic chưa?
- [ ] Tình huống xấu nhất → user nhận thông báo tử tế hay màn hình trắng?

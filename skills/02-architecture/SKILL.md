---
name: 02-architecture
description: "Tiêu chuẩn kiến trúc: Module hóa, Cô lập lỗi, Test độc lập, Bảo mật chiều sâu và Quy chuẩn code size."
---

# Kỹ Năng: Kiến Trúc & Quy Chuẩn Code (Architecture & Code Standards)

**Mục đích**: Đảm bảo mọi code tuân thủ 5 nguyên tắc bắt buộc — "sập 1 chỗ không kéo toàn hệ thống".

## 5 Nguyên Tắc Bắt Buộc

### 1. Loose Coupling — Khớp Nối Lỏng
- Mỗi feature nằm trong module riêng. Module A **không** gọi trực tiếp DB query hay biến cục bộ của module B.
- Module B chỉ nhận "kết quả" từ A qua interface/function công khai.
- Phần phụ (Log, Email) lỗi → phần chính vẫn thành công.

### 2. Fault Isolation — Cô Lập Lỗi
- Mọi lời gọi API/module rủi ro phải nằm trong `try...catch`.
- UI chỉ hiện lỗi cục bộ ("Không tải được gợi ý"), phần còn lại vẫn chạy.
- **Không bao giờ trắng trang (WSOD).**

### 3. Validation First — Kiểm Tra Đầu Vào Trước
- Frontend khóa form rồi → Backend **vẫn validate lại** bằng Schema (Zod, Joi).
- Mỗi module gác cửa độc lập — Trust No One.

### 4. I/O Safety — Timeout + Xử Lý Lỗi
- Mọi logic gọi API bên ngoài phải có **Timeout** (VD: 8s) + **Fallback**.
- Request treo quá timeout → cắt, trả lỗi, đi tiếp. Không để 1 request kéo sập server.

### 5. Small Units — Hàm Nhỏ Gọn
- Hàm > **80 dòng** → bắt buộc tách helper.
- Có thư viện chuẩn 1 dòng → không tự viết thuật toán 20 dòng.

## Mẫu Cấu Trúc Module

```text
/src/features/payment/
  ├── payment.controller.ts   # Request/Response
  ├── payment.service.ts      # Business Logic
  ├── payment.repository.ts   # Nơi DUY NHẤT đụng DB
  └── payment.test.ts         # Unit Test (mock, không gọi DB thật)
```

**Guardrails**:
- File `payment.*` KHÔNG chứa `SELECT * FROM users` → muốn user, gọi `getPublicUser()` từ module user.
- Test module A fail → module B vẫn chạy bình thường.

## Checklist Trước Khi Đóng Task

- [ ] Code mới đã đóng gói thành function/class riêng biệt?
- [ ] Throw Error → app chính có crash không? Đã try-catch/fallback?
- [ ] Input đã validate trước khi vào logic?
- [ ] API call có timeout + fallback?
- [ ] Tình huống xấu nhất → user thấy thông báo tử tế hay màn hình trắng?
- [ ] Không có hàm nào > 80 dòng?

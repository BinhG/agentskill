---
name: 02-architecture
description: "Tiêu chuẩn kiến trúc: Module hóa, Cô lập lỗi, Test độc lập, Bảo mật chiều sâu và Quy chuẩn code size."
---

# Kỹ Năng: Kiến Trúc & Quy Chuẩn Code (Architecture & Code Standards)

**Mục đích**: Đảm bảo mọi code tuân thủ 6 nguyên tắc bắt buộc — "sập 1 chỗ không kéo toàn hệ thống".

## 6 Nguyên Tắc Bắt Buộc

### 1. Loose Coupling — Khớp Nối Lỏng
- Mỗi feature nằm trong module riêng.
- Module B chỉ nhận "kết quả" từ A qua interface công khai.
- Phần phụ (Log, Email) lỗi → phần chính vẫn thành công.

### 2. Fault Isolation — Cô Lập Lỗi
- Mọi lời gọi API/module rủi ro phải nằm trong `try...catch`.
- UI chỉ hiện lỗi cục bộ, phần còn lại vẫn chạy.
- **Không bao giờ trắng trang (WSOD).**

### 3. Validation First — Kiểm Tra Đầu Vào
- Frontend khóa rồi → Backend **vẫn validate lại** (Zod, Joi).
- Trust No One — mỗi module gác cửa độc lập.

### 4. I/O Safety — Timeout + Fallback
- API bên ngoài phải có **Timeout** (VD: 8s) + **Fallback**.
- Request treo → cắt, trả lỗi, đi tiếp.

### 5. Small Units — Hàm Nhỏ Gọn
- Hàm > **80 dòng** → bắt buộc tách helper.
- Có thư viện chuẩn 1 dòng → không tự viết 20 dòng.

### 6. No Regressions — Không Phá Chỗ Khác (SWE-bench)
- Fix/thêm feature → **chạy toàn bộ test suite**, không chỉ test liên quan.
- **Fail-to-pass**: test trước fail → sau phải pass (fix đúng bug).
- **Pass-to-pass**: test trước pass → sau vẫn pass (không regression).
- Có regression → DỪNG, fix trước khi ship.

## Ground Truth Observation (Anthropic Pattern)

- Ở MỖI bước implement, phải xác nhận bằng **kết quả thực** (build output, test result, runtime log).
- **KHÔNG giả định** code chạy đúng chỉ vì "trông đúng".
- Đọc output → phân tích → quyết định bước tiếp.

## Mẫu Cấu Trúc Module

```text
/src/features/payment/
  ├── payment.controller.ts   # Request/Response
  ├── payment.service.ts      # Business Logic
  ├── payment.repository.ts   # Nơi DUY NHẤT đụng DB
  └── payment.test.ts         # Unit Test (mock, không gọi DB thật)
```

## Checklist Trước Khi Đóng Task

- [ ] Code đóng gói function/class riêng biệt?
- [ ] Throw Error → try-catch/fallback đầy đủ?
- [ ] Input validate trước logic?
- [ ] API call có timeout + fallback?
- [ ] Hàm nào > 80 dòng?
- [ ] Chạy test suite → **không regression**?
- [ ] Kết quả dựa trên **ground truth** (test/build output), không giả định?

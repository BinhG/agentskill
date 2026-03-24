---
name: 02-architecture
description: "Chuẩn kiến trúc khi triển khai: module hóa, cô lập lỗi, validate input, timeout/fallback cho I/O, giữ code nhỏ dễ test."
---

# Kỹ năng: Architecture & Code Standards

## Khi nào dùng
Dùng ở mọi task có sửa code, đặc biệt khi thêm feature mới hoặc đụng tới API/DB/external service.

## Nguyên tắc bắt buộc
1. **Loose coupling**: module giao tiếp qua interface rõ ràng.
2. **Fault isolation**: lỗi cục bộ không làm sập luồng chính.
3. **Validation first**: input phải được validate ở biên hệ thống.
4. **I/O safety**: network/DB call có timeout + xử lý lỗi phù hợp.
5. **Small units**: function dài > 80 dòng thì tách helper.

## Cấu trúc module khuyến nghị
```text
feature/
  controller   # I/O mapping, status code
  service      # business rules
  repository   # DB/external adapter
  test         # unit/integration theo scope
```

## Guardrails triển khai
- Không truy cập trực tiếp dữ liệu nội bộ module khác.
- Không để business logic nằm ở controller.
- Không trộn query DB với transform phức tạp trong cùng hàm dài.
- Với external API: phải có timeout, retry/backoff (nếu hợp lệ), fallback hoặc graceful error.

## Checklist trước khi kết thúc task
- [ ] Input/output contract rõ và có validate.
- [ ] Đường lỗi được xử lý (không “nổ trắng trang”).
- [ ] Logic quan trọng có test hoặc ít nhất có bước verify tái lập.
- [ ] Không tạo coupling mới giữa các module.

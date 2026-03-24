# Project Conventions

File này chứa các quy ước tích lũy từ kinh nghiệm thực tế. Được cập nhật mỗi khi phát hiện lỗi lặp.

> **Nguyên tắc Aider**: Bắt đầu nhỏ, thêm rule khi AI mắc lỗi lặp → lần sau không lặp.

## Coding Standards

- Luôn dùng **absolute path**, không dùng relative path.
- Hàm tối đa **80 dòng**. Vượt → tách helper.
- Mọi API call bên ngoài: **timeout 8s** + fallback.
- Input validation ở cả Frontend và Backend (Trust No One).

## File & Naming

- Component: `PascalCase` (VD: `PaymentForm.tsx`).
- Utility/service: `camelCase` (VD: `paymentService.ts`).
- Constants: `UPPER_SNAKE_CASE`.
- Test file: `[module].test.ts` cùng folder với source.

## Git & Commit

- Commit message format: `type: description` (VD: `feat: add payment gateway`).
- Types: `feat`, `fix`, `refactor`, `chore`, `docs`, `test`.
- Mỗi commit = 1 thay đổi logic. Không gộp nhiều features vào 1 commit.

## Error Handling

- Không để error propagate không kiểm soát → `try-catch` ở boundary.
- Log error đủ context: file, function, input gây lỗi.
- User-facing error: thông báo thân thiện, không leak stack trace.

## Testing

- Test phải dùng mock data, không gọi API/DB thật trong unit test.
- Chạy **toàn bộ test suite** trước khi ship (không chỉ test liên quan).
- Regression = blocker. Fix trước khi ship.

---

## Lessons Learned Log

*Thêm pattern lỗi mới ở đây khi phát hiện:*

| Ngày | Lỗi | Rule mới |
|---|---|---|
| (template) | AI dùng relative path | Luôn dùng absolute path |

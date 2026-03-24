---
name: 04-session-management
description: "Quy trình duy trì context, quản lý trạng thái dự án qua nhiều phiên làm việc và dọn dẹp bộ nhớ."
---

# Kỹ Năng: Quản Lý Đa Phiên & Bộ Nhớ (Session & Memory Management)

**Mục đích**: Đảm bảo context không bị mất giữa các phiên làm việc.

## Artifact Vận Hành

| File | Vai trò | Khi nào cập nhật |
|---|---|---|
| `task.md` | Checklist tiến độ | Đầu + trong + cuối task |
| `implementation_plan.md` | Thiết kế kỹ thuật | Phase Planning |
| `walkthrough.md` | Log kết quả & proof | Cuối task |
| `CHANGELOG.md` | Lịch sử thay đổi | Khi ship feature |
| `TODO.md` | Việc chưa xong / bug | Bất kỳ lúc nào |
| `CONVENTIONS.md` | Rules tích lũy từ lỗi | Khi phát hiện lỗi lặp |

## Context Loading (Anthropic Pattern)

- **JIT (Just-In-Time)**: Chỉ đọc file khi thực sự cần, KHÔNG dump toàn bộ codebase.
- **Progressive disclosure**: Đọc overview trước → đọc chi tiết nếu cần.
- **Structured notes**: Ghi kết quả phân tích ra file `.md`, pull lại khi cần (không giữ trong context window).

## Quy Trình Mở Phiên (Bootstrap)

1. Đọc KI summaries liên quan.
2. Đọc `TODO.md` / `CHANGELOG.md` / `task.md` / `CONVENTIONS.md`.
3. Tóm tắt trạng thái cho User trước khi code.

## Quy Trình Đóng Phiên (Handoff)

1. Cập nhật `task.md` — `[x]` hoàn thành, `[ ]` còn lại.
2. Ghi `walkthrough.md` — đã làm gì, test ra sao.
3. Cập nhật `TODO.md` — bug tồn đọng, việc chưa xong.
4. Nếu có quy ước mới → cập nhật `CONVENTIONS.md`.

## Outcome Tracking (SWE-bench Mindset)

Cuối mỗi task, ghi lại vào `walkthrough.md`:

| Metric | Giá trị |
|---|---|
| Kết quả | ✅ Pass / ❌ Fail / ⚠️ Partial |
| Số lần retry | 0 / 1 / 2 / 3+ |
| Regression | Có / Không |
| Lessons learned | (ghi nếu có) |

**Mục đích**: Đo lường chất lượng làm việc bằng **số liệu**, không bằng cảm giác.

## Dọn Dẹp Context

- **Nhẹ**: Cuối phiên, rà KIs trùng → hỏi User trước khi gộp.
- **Mạnh**: Context quá rác → thông báo User, tự tóm tắt + gộp.

## Anti-Patterns

- ❌ Nghĩ AI tự nhớ toàn bộ (chỉ nhớ qua KIs + file đọc).
- ❌ Kéo dài 1 session fix bug hàng giờ (viết bug ra file → mở session mới).
- ❌ Sửa dependency mà không document.
- ❌ Không đọc `CONVENTIONS.md` đầu session → lặp lỗi cũ.

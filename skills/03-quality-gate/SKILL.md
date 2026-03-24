---
name: 03-quality-gate
description: "Cổng chất lượng 2 mức: Strict Mode (block code xấu) và Advisor Mode (gợi ý nhẹ nhàng, ghi tech debt)."
---

# Kỹ Năng: Cổng Chất Lượng (Quality Gate)

**Mục đích**: Kiểm soát chất lượng code với 2 mức hoạt động + vòng lặp cải tiến.

## Chuyển Mức

| Trigger | Mode |
|---|---|
| Mặc định / "ship nhanh" / "làm trước" | **Advisor** |
| "review kỹ" / "hardcore" / "strict" / hardening | **Strict** |

---

## Mức 1: Advisor Mode (MẶC ĐỊNH)

### Trong lúc code
- Nhận thấy trade-off → cảnh báo **1-2 câu ngắn** + gợi ý phương án gọn hơn.
- User chọn "làm nhanh" → code ngay, không đôi co.

### Ghi chép Tech Debt
- Code smell (DRY violation, hàm > 200 dòng) → ghi `TODO_REFACTOR.md`.
- **Không tự ý sửa**. Cuối task nhắc nhẹ.

### ✅ Hoàn thành (Advisor)
- Code chạy được, user chấp nhận trade-off.
- Tech debt đã log (nếu có).

---

## Mức 2: Strict Mode

### Điều kiện CHẶN

| Vi phạm | Hành động |
|---|---|
| Hàm > 80 dòng | **DỪNG**. Tách helper. |
| DB/Network thiếu Timeout/Fallback | **VIẾT LẠI**. |
| Tightly Coupled | **TÁCH Interface**. |
| Fix triệu chứng, chưa Root Cause | **CHẶN**. Phân tích lại. |
| Có regression (test trước pass → fail) | **CHẶN**. Fix regression trước. |

### Stress-test bắt buộc
1. *"1 triệu request/giây — cái gì nổ?"*
2. *"Thiếu try-catch, API ngoài ngỏm thì sập?"*
3. *"Module này coupled chặt với module nào?"*

### ✅ Hoàn thành (Strict)
- Không còn vi phạm CHẶN.
- Stress-test 3 câu đã trả lời.
- Checklist `02-architecture` pass hết.
- **Không regression** (pass-to-pass verified).

---

## Evaluator-Optimizer Loop (Anthropic Pattern)

Khi verify fail, KHÔNG lặp lại cùng 1 cách fix:

```
Attempt 1: Implement → Test → FAIL
    ↓ (phân tích lỗi, thêm context)
Attempt 2: Fix with error context → Test → FAIL
    ↓ (root cause analysis)
Attempt 3: Alternative approach → Test → PASS ✅
    ↓ (nếu vẫn fail)
STOP → Báo User, yêu cầu human intervention
```

**Rules:**
- Tối đa **3 attempts** trước khi escalate.
- Mỗi attempt phải thay đổi approach, không repeat.
- Log mỗi attempt: lỗi gì, fix gì, kết quả.

---

## Lessons Learned Protocol (Aider Pattern)

Khi AI mắc lỗi lặp lại → thêm rule vào `CONVENTIONS.md`:

```
Lỗi lặp phát hiện → Phân tích pattern → Thêm rule → Lần sau không lặp
```

Ví dụ: *AI liên tục dùng relative path → thêm rule "Luôn dùng absolute path".*

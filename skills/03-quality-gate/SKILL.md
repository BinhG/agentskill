---
name: 03-quality-gate
description: "Cổng chất lượng 2 mức: Strict Mode (block code xấu) và Advisor Mode (gợi ý nhẹ nhàng, ghi tech debt)."
---

# Kỹ Năng: Cổng Chất Lượng (Quality Gate)

**Mục đích**: Kiểm soát chất lượng code với 2 mức hoạt động.

## Chuyển Mức

| Trigger | Mode |
|---|---|
| Mặc định / "ship nhanh" / "làm trước" | **Advisor** |
| "review kỹ" / "hardcore" / "strict" / hardening phase | **Strict** |

---

## Mức 1: Advisor Mode (MẶC ĐỊNH)

### Trong lúc code
- Nhận thấy trade-off → cảnh báo **1-2 câu ngắn** + gợi ý phương án gọn hơn.
- User chọn "làm nhanh" → code ngay, không đôi co.

### Ghi chép Tech Debt
- Phát hiện code smell (DRY violation, hàm > 200 dòng, logic duplicate) → ghi vào `TODO_REFACTOR.md`.
- **Không tự ý sửa**. Cuối task nhắc nhẹ: *"Có nợ kỹ thuật trong TODO_REFACTOR."*

### Định nghĩa hoàn thành (Advisor)
- ✅ Code chạy được, user chấp nhận trade-off.
- ✅ Tech debt đã log (nếu có).

---

## Mức 2: Strict Mode

### Điều kiện CHẶN — không cho phép ship

| Vi phạm | Hành động |
|---|---|
| Hàm > 80 dòng | **DỪNG**. Yêu cầu tách helper. |
| Logic DB/Network thiếu Timeout hoặc Fallback | **VIẾT LẠI**. Cấm cãi. |
| Tightly Coupled (module A đọc thẳng DB của B) | **TÁCH Interface** ngay. |
| Fix triệu chứng mà chưa tìm Root Cause | **CHẶN**. Phân tích lại. |

### Stress-test bắt buộc
Trước khi tạo file/logic mới, tự trả lời:
1. *"1 triệu request/giây — cái gì nổ đầu tiên?"*
2. *"Chỗ này thiếu try-catch, API ngoài ngỏm thì server sập luôn?"*
3. *"Module này đang coupled chặt với module nào?"*

→ Chỉ khi thoả mãn mới được ship.

### Định nghĩa hoàn thành (Strict)
- ✅ Không còn vi phạm nào trong bảng CHẶN.
- ✅ Stress-test 3 câu đã trả lời rõ.
- ✅ Checklist `02-architecture` pass hết.

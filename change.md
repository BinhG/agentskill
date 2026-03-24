# Chi tiết thay đổi (PR trước)

Tài liệu này tóm tắt **đầy đủ, dễ đọc** các thay đổi đã được thực hiện trong PR:

> **Refine core skill docs and workflows for clearer planning and quality gates**

---

## 1) Tổng quan nhanh

PR trước đã tập trung vào việc chuẩn hóa lại bộ kỹ năng (skills) và workflow để AI:

- Kích hoạt skill đúng ngữ cảnh hơn (rõ “khi nào dùng”).
- Có đầu ra bắt buộc trước khi chuyển phase (rõ “xong là gì”).
- Giảm mơ hồ khi thực thi (thêm guardrails/checklist).
- Loại bỏ phụ thuộc vào command hooks không portable trong tài liệu.

---

## 2) Danh sách file đã đổi

1. `skills/01-planning/SKILL.md`
2. `skills/02-architecture/SKILL.md`
3. `skills/03-quality-gate/SKILL.md`
4. `skills/04-session-management/SKILL.md`
5. `workflows/workflow.md`
6. `workflows/antigravity-workflow.md`

---

## 3) Chi tiết từng file

## 3.1 `skills/01-planning/SKILL.md`

### Trước đây
- Nội dung thiên về triết lý và vai trò, nhưng còn thiếu khung “đầu ra bắt buộc” cụ thể.
- Thiếu định nghĩa hoàn thành rõ ràng để biết khi nào được phép sang bước code.

### Đã thay đổi
- Bổ sung mục **Khi nào dùng** với các dấu hiệu trigger rõ (scope lớn, rủi ro cao, nhiều module).
- Bổ sung mục **Mục tiêu đầu ra** yêu cầu có `implementation_plan.md` với:
  - phạm vi in/out,
  - 2-3 phương án,
  - trade-off,
  - verify plan,
  - danh sách file `[NEW]/[MODIFY]/[DELETE]`.
- Chuẩn hóa khung phản biện 3 vai: Architect / Devil’s Advocate / Executor.
- Thêm **Định nghĩa hoàn thành** để chặn việc code khi plan chưa được xác nhận.

### Giá trị mang lại
- Planning nhất quán hơn.
- Giảm rủi ro “nhảy vào code sớm”.

---

## 3.2 `skills/02-architecture/SKILL.md`

### Trước đây
- Có nguyên tắc kiến trúc tốt nhưng trải dài, ví dụ dài, chưa đóng gói thành checklist vận hành nhanh.

### Đã thay đổi
- Cô đọng thành 5 nguyên tắc bắt buộc:
  1. Loose coupling
  2. Fault isolation
  3. Validation first
  4. I/O safety (timeout + xử lý lỗi)
  5. Small units (hàm > 80 dòng cần tách)
- Giữ mẫu cấu trúc module (controller/service/repository/test).
- Bổ sung guardrails cụ thể để tránh coupling và “nhồi nhét logic”.
- Kết thúc bằng checklist trước khi đóng task.

### Giá trị mang lại
- Dễ dùng trong lúc code thật.
- Ít tranh cãi tiêu chuẩn vì checklist rõ.

---

## 3.3 `skills/03-quality-gate/SKILL.md`

### Trước đây
- Đã có Advisor/Strict mode nhưng mô tả dài, chưa thật gọn cho thao tác hằng ngày.

### Đã thay đổi
- Giữ kiến trúc 2 chế độ nhưng cụ thể hóa:
  - **Advisor Mode**: cảnh báo ngắn + cho phép ship nếu user chấp nhận trade-off.
  - **Strict Mode**: định nghĩa các điều kiện chặn (hàm quá lớn, thiếu timeout/fallback, coupling chặt, chưa xử lý root cause).
- Thêm bộ câu hỏi stress-test thống nhất cho review.
- Thêm “định nghĩa hoàn thành” riêng cho từng mode.

### Giá trị mang lại
- Chất lượng review ổn định hơn giữa các task.
- Dễ chuyển mode theo mục tiêu của user (ship nhanh vs hardening).

---

## 3.4 `skills/04-session-management/SKILL.md`

### Trước đây
- Có ý tưởng quản lý đa phiên nhưng thiên lý thuyết.

### Đã thay đổi
- Chuyển sang vận hành bằng artifact cụ thể:
  - `task.md`
  - `implementation_plan.md`
  - `walkthrough.md` / `CHANGELOG.md`
  - `TODO.md`
- Bổ sung quy trình mở phiên (bootstrap) và đóng phiên (handoff).
- Liệt kê anti-pattern cần tránh.

### Giá trị mang lại
- Giảm mất ngữ cảnh giữa các phiên.
- Dễ bàn giao cho phiên kế tiếp.

---

## 3.5 `workflows/workflow.md` (Quick Workflow)

### Trước đây
- Quick flow đã có nhưng nội dung còn phân tán.

### Đã thay đổi
- Chuẩn hóa thành 3 bước ngắn:
  1. Understand
  2. Implement
  3. Verify
- Thêm điều kiện rõ ràng khi nào cần nâng cấp sang antigravity workflow.

### Giá trị mang lại
- Dùng nhanh cho task nhỏ, giảm overhead planning.

---

## 3.6 `workflows/antigravity-workflow.md`

### Trước đây
- Có hướng phase-gated tốt nhưng tham chiếu một số command hooks không phải môi trường nào cũng có.

### Đã thay đổi
- Giữ phase map 0→4 nhưng viết lại theo cách chạy được ở repo-centric workflow.
- Gắn rõ từng phase với artifact thực tế (`task.md`, `implementation_plan.md`, `walkthrough.md`).
- Loại bỏ phụ thuộc vào hooks như `task_boundary`, `notify_user`, `run_command`.

### Giá trị mang lại
- Tài liệu mang tính thực thi cao hơn.
- Giảm lỗi do “tool không tồn tại”.

---

## 4) Các kiểm tra đã thực hiện trong PR trước

- Kiểm tra không còn hook cũ trong docs:
  - `rg -n "task_boundary|notify_user|run_command" workflows skills`
- Kiểm tra phạm vi thay đổi bằng diff/stat.
- Rà nội dung các file đã sửa để đảm bảo frontmatter + cấu trúc hợp lệ.

---

## 5) Tác động tổng thể

### Tác động tích cực
- Skill activation rõ hơn.
- Quality gate nhất quán hơn.
- Session handoff mượt hơn.
- Workflow thực tế hơn với môi trường repo.

### Trade-off
- Nội dung được cô đọng mạnh, nên bớt phần “giải thích dài” mang tính triết lý.
- Đổi lại: thao tác thực chiến nhanh và dễ áp dụng hơn.

---

## 6) Gợi ý bước tiếp theo (nếu bạn muốn mình làm tiếp)

1. Thêm `task.md` + `implementation_plan.md` template mẫu (sẵn form điền).
2. Thêm ví dụ “before/after” cho 1 task thật để minh họa cách áp skill.
3. Thêm 1 file rubric chấm chất lượng output theo từng mode (Advisor/Strict).


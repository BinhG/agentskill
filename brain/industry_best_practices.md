# Research Report: Industry Best Practices cho AI Agent Skills

## Tóm tắt 4 nguồn học

### 1. OpenAI Codex — Task Framing & AGENTS.md

**Task Framing 4 yếu tố** (mọi prompt đều phải có):
- **Goal**: Cần thay đổi/xây dựng gì
- **Context**: File, folder, doc, error liên quan
- **Constraints**: Standards, conventions, giới hạn
- **Done When**: Điều kiện hoàn thành rõ ràng (test pass, behavior change)

**AGENTS.md best practices:**
- Đặt root repo, concise, chỉ thêm rule khi thấy AI lặp lỗi
- Layered: global → project → directory-specific override
- Tách task-specific instructions ra file riêng, đừng nhồi vào 1 file

**Plan-Act-Reflect loop:**
- Plan → Code → Reflect (tự review kết quả) → lặp lại nếu cần
- Không skip planning cho multi-step tasks

**Best-of-N:**
- Chạy N lần, chọn kết quả tốt nhất
- Áp dụng: khi có test suite, retry với context lỗi để cải thiện

---

### 2. Anthropic — Context Engineering & Agent Patterns

**Ground Truth at every step:**
- Agent PHẢI lấy kết quả thực (tool output, test result) ở mỗi bước
- Không dựa vào giả định → dựa vào observation

**Evaluator-Optimizer loop:**
- 1 LLM sinh code, 1 LLM đánh giá + feedback → lặp đến khi pass
- Tương tự 03-quality-gate nhưng có metric đo rõ

**Context Window Management:**
- JIT (Just-In-Time) data loading — chỉ load khi cần
- Progressive disclosure — không dump context lên đầu
- Structured note-taking — ghi chú ra file, pull lại khi cần

**ACI Design (Agent-Computer Interface):**
- Thiết kế tool interface kỹ như HCI
- Poka-yoke: thiết kế tool sao cho khó mắc lỗi (VD: absolute path thay vì relative)
- Test tool với nhiều inputs trước khi dùng

---

### 3. Aider — Conventions Discipline

**CONVENTIONS.md:**
- File nhỏ gọn, always-loaded, chứa: libraries, type hints, style, testing, error handling
- Progressive: bắt đầu basic, thêm dần khi phát hiện lỗi lặp
- Persistent config: tự động load mỗi session, không cần nhắc lại

**Key insight:**
- Convention tốt = AI ít mắc lỗi lặp
- Mỗi lần AI mắc lỗi → thêm rule vào convention → lần sau không lặp

---

### 4. SWE-bench — Benchmark Mindset

**Đo bằng số liệu, không bằng cảm giác:**
- **Resolved Rate** = % task pass all tests
- **Pass@1** = resolved ngay lần 1
- **Fail-to-pass** = test trước fail, sau pass (fix đúng bug)
- **Pass-to-pass** = test trước pass, sau vẫn pass (không regression)

**No regressions rule:**
- Fix 1 chỗ → không được phá chỗ khác
- Bắt buộc chạy toàn bộ test suite, không chỉ test liên quan

**Áp dụng cho .agents:**
- Mỗi task xong → ghi outcome (pass/fail/partial)
- Đo lường: bao nhiêu lần phải retry? Bao nhiêu regression?
- Skill tốt = giảm retry rate + giảm regression

---

## Gap Analysis: Hiện tại vs Best Practices

| Best Practice | Hiện tại (.agents) | Cần bổ sung |
|---|---|---|
| Task Framing 4 yếu tố | ❌ Chưa có template chuẩn | Thêm vào `01-planning` |
| Plan-Act-Reflect loop | ⚠️ Có plan + execute nhưng thiếu Reflect | Thêm Reflect step vào workflow |
| Ground Truth observation | ⚠️ Có verify nhưng chưa cưỡng chế | Enforce "chạy test thật" |
| Evaluator-Optimizer | ⚠️ `03-quality-gate` có concept nhưng chưa loop | Thêm retry-with-feedback |
| CONVENTIONS.md discipline | ❌ Chưa có file conventions | Tạo mới |
| Progressive rule adding | ❌ Rules cố định | Thêm "Lessons Learned" section |
| SWE-bench metrics | ❌ Không đo | Thêm outcome tracking |
| No-regressions rule | ⚠️ Có trong checklist nhưng chưa mạnh | Enforce trong verify |
| JIT context loading | ⚠️ Có nhưng chưa rõ | Làm rõ hơn |
| Layered config | ⚠️ Có skills nhưng flat | Giữ nguyên (đủ tốt) |

---

## Các thay đổi cụ thể

### A. Cập nhật Skills hiện có

**`01-planning`**: Thêm Task Framing template (Goal/Context/Constraints/DoneWhen)

**`02-architecture`**: Thêm nguyên tắc "No Regressions" + Ground Truth

**`03-quality-gate`**: Thêm Evaluator-Optimizer loop (retry with feedback, max 3 attempts)

**`04-session-management`**: Thêm Outcome Tracking (pass/fail/retry count), Lessons Learned protocol

### B. File mới

**`CONVENTIONS.md`** (root `.agents/`): Project conventions — progressive, always-loaded
- Coding standards ngắn gọn
- Lỗi hay gặp → rule mới
- Giống Aider conventions

### C. Workflow updates

**`antigravity-workflow.md`**: Thêm Phase 3.5 "Reflect" sau Verify

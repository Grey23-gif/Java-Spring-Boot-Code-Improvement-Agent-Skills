# Skill 7: Refactor Gatekeeper

Đường dẫn:

```text
.agents/skills/refactor-gatekeeper/SKILL.md

Nội dung:

---
name: refactor-gatekeeper
description: Performs the final quality gate after Java or Spring Boot code changes. Reviews diffs, verifies tests, checks behavior preservation, detects accidental API changes, security regressions, unused code, and incomplete refactors. Use this skill when the user asks to verify, validate, audit, finalize, or approve a refactor.
---

# Refactor Gatekeeper

## Goal

Kiểm tra lần cuối trước khi chấp nhận code refactor.

## Required Checks

### 1. Build

- Project compile thành công.
- Không có import lỗi.
- Không có dependency thiếu.
- Không có warning nghiêm trọng mới.

### 2. Tests

- Test cũ vẫn chạy thành công.
- Test mới kiểm tra đúng logic thay đổi.
- Không có test bị disable không rõ lý do.
- Không chỉnh assertion chỉ để test pass.

### 3. Behavior

- Endpoint không bị đổi ngoài yêu cầu.
- Request và response không bị đổi ngoài yêu cầu.
- HTTP status vẫn chính xác.
- Exception vẫn được xử lý.
- Database operation vẫn đúng.
- Transaction boundary không bị phá vỡ.

### 4. Architecture

- Controller không chứa business logic.
- Service không phụ thuộc trực tiếp implementation không cần thiết.
- Repository không chứa nghiệp vụ.
- Mapping được đặt đúng vị trí.
- Không tạo circular dependency.

### 5. Security

- Không xuất hiện secret.
- Không log token, password hoặc dữ liệu nhạy cảm.
- Rule phân quyền không bị mở rộng ngoài ý muốn.
- Validation không bị loại bỏ.
- Không thêm endpoint công khai ngoài yêu cầu.

### 6. Code Quality

- Không còn code trùng lặp mới.
- Không có method quá dài mới.
- Không có dead code.
- Không có import thừa.
- Không có comment sai với code.
- Tên method và biến phản ánh đúng mục đích.

## Output Format

### Refactor Verdict

Một trong các kết quả:

- APPROVED.
- APPROVED WITH MINOR CHANGES.
- CHANGES REQUIRED.
- REJECTED.

### Checklist

| Hạng mục | Trạng thái | Ghi chú |
|---|---|---|

### Những thay đổi bắt buộc

Liệt kê lỗi phải sửa trước khi merge.

### Những cải tiến tùy chọn

Liệt kê đề xuất không chặn việc merge.

### Tóm tắt thay đổi

- File đã sửa.
- Mục đích.
- Rủi ro còn lại.
- Test đã thực hiện.

## Constraints

- Không phê duyệt nếu build hoặc test chính thất bại.
- Không bỏ qua lỗi bảo mật.
- Không yêu cầu sửa style không liên quan để chặn việc merge.
- Không tự động chạy lệnh phá hủy dữ liệu.
- Không tự động merge hoặc commit nếu người dùng chưa yêu cầu.
Quy trình sử dụng toàn bộ bộ Skill
Giai đoạn 1: Phân tích
Hãy phân tích OrderService.java bằng codebase-analyzer.
Chưa sửa code. Hãy chỉ ra code smell, vi phạm SOLID, rủi ro và phạm vi ảnh hưởng.
Giai đoạn 2: Lập kế hoạch
Sử dụng refactor-planner để tạo kế hoạch refactor OrderService.
Phải giữ nguyên API và hành vi thanh toán hiện tại.
Giai đoạn 3: Bảo vệ bằng test
Sử dụng test-regression-guard để tạo Unit Test bảo vệ hành vi hiện tại
của phương thức checkout trước khi refactor.
Giai đoạn 4: Refactor
Sử dụng safe-code-refactorer để refactor OrderService theo kế hoạch.
Không thay đổi endpoint, request, response hoặc nghiệp vụ hiện tại.
Giai đoạn 5: Kiểm tra chuyên biệt
Sử dụng spring-security-auditor để kiểm tra phân quyền và JWT.

Hoặc:

Sử dụng performance-optimizer để kiểm tra query và hiệu năng.
Giai đoạn 6: Kiểm duyệt cuối
Sử dụng refactor-gatekeeper để kiểm tra toàn bộ thay đổi.
Chỉ APPROVED nếu build, test, kiến trúc và bảo mật đều đạt yêu cầu.
Prompt tổng hợp để Agent tự chạy quy trình
Hãy cải tiến và refactor module được cung cấp bằng bộ Agent Skills.

Thực hiện theo đúng thứ tự:

1. Dùng codebase-analyzer để phân tích code hiện tại.
2. Dùng refactor-planner để lập kế hoạch thay đổi.
3. Dùng test-regression-guard để bảo vệ hành vi hiện tại.
4. Dùng safe-code-refactorer để thực hiện từng thay đổi nhỏ.
5. Nếu liên quan đến Spring Security hoặc JWT, dùng spring-security-auditor.
6. Nếu liên quan đến hiệu năng, dùng performance-optimizer.
7. Cuối cùng, dùng refactor-gatekeeper để kiểm tra kết quả.

Yêu cầu bắt buộc:

- Không thay đổi nghiệp vụ hiện tại nếu chưa được yêu cầu.
- Không đổi endpoint, request hoặc response ngoài phạm vi.
- Không tự ý xóa file hoặc dữ liệu.
- Không hard-code secret.
- Chạy build và test sau khi sửa.
- Nếu test thất bại, phải xác định nguyên nhân thay vì bỏ qua test.
- Trình bày danh sách file thay đổi và giải thích lý do.
- Thực hiện refactor theo từng bước nhỏ, có thể kiểm tra và rollback.
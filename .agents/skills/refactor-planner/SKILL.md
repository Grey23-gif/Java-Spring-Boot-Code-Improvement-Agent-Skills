# Skill 2: Refactor Planner

Đường dẫn:

.agents/skills/refactor-planner/SKILL.md

Nội dung:

---
name: refactor-planner
description: Creates a safe, incremental refactoring plan for Java and Spring Boot code while preserving existing behavior. Use this skill when the user asks for a refactor plan, architecture improvement plan, migration strategy, SOLID restructuring, or step-by-step code cleanup.
---

# Refactor Planner

## Goal

Tạo kế hoạch refactor an toàn, chia nhỏ thành từng bước và giữ nguyên hành vi hiện tại của hệ thống.

## Instructions

1. Phân tích chức năng hiện tại của code.

2. Xác định hành vi phải được giữ nguyên:

- Input.
- Output.
- Exception.
- HTTP status.
- Database changes.
- Security permissions.
- Side effects.
- Log quan trọng.

3. Xác định mục tiêu refactor:

- Giảm độ phức tạp.
- Tách trách nhiệm.
- Loại bỏ code trùng lặp.
- Áp dụng SOLID.
- Cải thiện khả năng test.
- Cải thiện hiệu năng.
- Cải thiện bảo mật.
- Tăng khả năng mở rộng.

4. Chia kế hoạch thành các bước nhỏ.

Mỗi bước phải bao gồm:

- File cần thay đổi.
- Nội dung thay đổi.
- Lý do.
- Rủi ro.
- Test cần chạy.
- Điều kiện hoàn thành.

5. Ưu tiên thay đổi ít rủi ro trước.

6. Xác định những bước có thể rollback độc lập.

7. Không trộn refactor với việc thêm tính năng mới, trừ khi người dùng yêu cầu rõ ràng.

## Output Format

### 1. Hiện trạng

Mô tả thiết kế hiện tại và vấn đề chính.

### 2. Mục tiêu

Liệt kê kết quả cần đạt sau refactor.

### 3. Kế hoạch thực hiện

#### Bước 1: Bảo vệ hành vi hiện tại

- Thêm hoặc cập nhật test.
- Ghi nhận các trường hợp đầu vào và đầu ra.

#### Bước 2: Thay đổi nhỏ

- Đổi tên.
- Extract method.
- Loại bỏ code trùng lặp.

#### Bước 3: Thay đổi cấu trúc

- Tách class.
- Tạo interface.
- Áp dụng strategy hoặc factory khi thực sự cần thiết.

#### Bước 4: Kiểm tra

- Unit Test.
- Integration Test.
- Build.
- Static analysis.

### 4. Rủi ro

| Rủi ro | Mức độ | Cách kiểm soát |
|---|---|---|

### 5. Tiêu chí hoàn thành

Danh sách điều kiện để xác nhận refactor thành công.

## Constraints

- Không thay đổi public API nếu chưa được người dùng cho phép.
- Không thay đổi database schema ngoài phạm vi yêu cầu.
- Không đề xuất rewrite toàn bộ hệ thống khi có thể refactor từng phần.
- Không áp dụng pattern chỉ để làm code có vẻ chuyên nghiệp hơn.
- Luôn ưu tiên giải pháp đơn giản nhất đáp ứng yêu cầu.
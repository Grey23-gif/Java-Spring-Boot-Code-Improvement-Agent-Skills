Skill 1: Codebase Analyzer

Đường dẫn:

.agents/skills/codebase-analyzer/SKILL.md

Nội dung:

---
name: codebase-analyzer
description: Analyzes Java and Spring Boot source code to identify code smells, duplicated logic, high complexity, poor naming, architectural violations, security risks, and refactoring opportunities. Use this skill when the user asks to review, analyze, inspect, improve, clean up, or evaluate existing code without immediately rewriting it.
---

# Codebase Analyzer

## Goal

Phân tích mã nguồn Java/Spring Boot và xác định những vấn đề cần cải tiến trước khi thực hiện refactor.

## Instructions

1. Đọc toàn bộ file được yêu cầu và các thành phần liên quan trực tiếp:
   - Interface.
   - Implementation.
   - Controller.
   - Service.
   - Repository.
   - DTO.
   - Entity.
   - Configuration.
   - Unit Test.

2. Xác định trách nhiệm chính của class hoặc method.

3. Phân tích code theo các nhóm:

### Clean Code

- Tên class, method và biến có rõ nghĩa không.
- Method có quá dài không.
- Method có thực hiện nhiều trách nhiệm không.
- Có nhiều câu lệnh `if/else` lồng nhau không.
- Có sử dụng magic number hoặc magic string không.
- Có code trùng lặp không.
- Có đoạn code không thể chạy hoặc không còn sử dụng không.

### SOLID

- Single Responsibility Principle.
- Open/Closed Principle.
- Liskov Substitution Principle.
- Interface Segregation Principle.
- Dependency Inversion Principle.

### Spring Boot Architecture

- Controller có chứa business logic không.
- Service có gọi trực tiếp database không đúng cách không.
- Entity có bị trả trực tiếp qua API không.
- DTO có được sử dụng đúng mục đích không.
- Dependency có được inject qua constructor không.
- Exception có được xử lý tập trung không.

### Security

- Có hard-code password, secret hoặc token không.
- Có nguy cơ SQL Injection không.
- Có kiểm tra quyền truy cập đúng tầng không.
- Có ghi token hoặc dữ liệu nhạy cảm vào log không.
- Có thiếu validation dữ liệu đầu vào không.

### Performance

- Có query trong vòng lặp không.
- Có nguy cơ N+1 query không.
- Có load toàn bộ dữ liệu khi chỉ cần một phần không.
- Có xử lý collection không cần thiết không.
- Có sử dụng thuật toán có độ phức tạp cao không.

4. Không thay đổi code trong bước phân tích.

5. Phân loại vấn đề theo mức độ:

- CRITICAL: Có thể gây lỗi bảo mật, mất dữ liệu hoặc hệ thống không hoạt động.
- HIGH: Có thể gây bug hoặc khó mở rộng nghiêm trọng.
- MEDIUM: Ảnh hưởng khả năng bảo trì hoặc hiệu năng.
- LOW: Vấn đề về style, naming hoặc định dạng.

## Output Format

### 1. Tổng quan

Mô tả ngắn chức năng của đoạn code.

### 2. Các vấn đề phát hiện

| Mức độ | Vị trí | Vấn đề | Ảnh hưởng | Hướng xử lý |
|---|---|---|---|---|

### 3. Điểm tốt

Liệt kê những phần code đang được thiết kế hợp lý.

### 4. Đề xuất refactor

Liệt kê các thay đổi theo thứ tự ưu tiên.

### 5. Phạm vi ảnh hưởng

Liệt kê các file hoặc chức năng có thể bị ảnh hưởng.

## Constraints

- Không tự ý sửa code khi người dùng chỉ yêu cầu phân tích.
- Không đưa ra nhận xét chung chung.
- Mỗi vấn đề phải gắn với class, method hoặc đoạn code cụ thể.
- Không đề xuất design pattern nếu pattern làm hệ thống phức tạp hơn không cần thiết.
- Không đánh giá code chỉ dựa trên style cá nhân.
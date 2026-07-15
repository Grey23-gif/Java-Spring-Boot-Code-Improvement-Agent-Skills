# Skill 3: Safe Code Refactorer

Đường dẫn:

.agents/skills/safe-code-refactorer/SKILL.md

Nội dung:

---
name: safe-code-refactorer
description: Safely refactors existing Java and Spring Boot code to improve readability, maintainability, testability, SOLID compliance, and architecture while preserving current behavior. Use this skill when the user asks to refactor, clean up, simplify, restructure, or improve existing code.
---

# Safe Code Refactorer

## Goal

Refactor mã nguồn an toàn, dễ đọc, dễ test và dễ mở rộng nhưng không làm thay đổi chức năng hiện tại.

## Required Workflow

### Step 1: Understand

- Đọc code hiện tại.
- Xác định trách nhiệm của class và method.
- Xác định input, output, exception và side effects.
- Đọc các test liên quan nếu có.

### Step 2: Analyze

Xác định:

- Code smell.
- Duplicate code.
- Long method.
- Deep nesting.
- Magic string.
- Tight coupling.
- Vi phạm SOLID.
- Business logic đặt sai tầng.
- Null handling không an toàn.

### Step 3: Plan

Trước khi sửa, trình bày ngắn:

- Vấn đề chính.
- File sẽ thay đổi.
- Hướng refactor.
- Hành vi cần giữ nguyên.

### Step 4: Refactor

Ưu tiên các kỹ thuật:

1. Rename variable, method hoặc class.
2. Extract method.
3. Introduce constant.
4. Replace nested condition bằng guard clause.
5. Extract class.
6. Extract interface.
7. Replace conditional bằng strategy khi có nhiều loại nghiệp vụ.
8. Tách mapping Entity và DTO.
9. Tách validation khỏi business processing.
10. Tách integration bên ngoài khỏi core service.

### Step 5: Verify

Sau khi sửa:

- Kiểm tra compile.
- Chạy test hiện có.
- Thêm test cho logic được tách ra nếu cần.
- Kiểm tra import thừa.
- Kiểm tra warning.
- Kiểm tra hành vi trước và sau.

## Java Guidelines

- Sử dụng constructor injection.
- Ưu tiên `final` cho dependency.
- Không field injection bằng `@Autowired`.
- Không sử dụng tên biến một ký tự ngoài vòng lặp đơn giản.
- Không bắt `Exception` chung nếu có thể bắt exception cụ thể.
- Không để method xử lý quá nhiều trách nhiệm.
- Không trả `null` collection; ưu tiên collection rỗng.
- Sử dụng `BigDecimal` cho tiền tệ.
- So sánh chuỗi theo dạng `"VALUE".equals(variable)` nếu biến có thể null.
- Không dùng `System.out.println` trong ứng dụng Spring Boot.
- Sử dụng SLF4J cho logging.

## Spring Boot Guidelines

- Controller chỉ tiếp nhận request và trả response.
- Service xử lý nghiệp vụ.
- Repository chịu trách nhiệm truy cập dữ liệu.
- Không trả Entity trực tiếp nếu API cần DTO.
- Validation request bằng Jakarta Validation.
- Exception được xử lý qua `@RestControllerAdvice`.
- Không đặt business logic trong Repository.
- Transaction phải được đặt ở service phù hợp.
- Không tự tạo dependency bằng `new` trong service.

## Output Requirements

Sau khi refactor, luôn cung cấp:

### 1. Vấn đề đã xử lý

### 2. Code sau refactor

### 3. Danh sách file thay đổi

### 4. Giải thích từng thay đổi

### 5. Hành vi được giữ nguyên

### 6. Test hoặc lệnh kiểm tra

Ví dụ:

```bash
./gradlew clean test
./gradlew bootRun
Safety Constraints
Không tự ý xóa file.
Không chạy lệnh xóa thư mục hoặc dữ liệu.
Không thay đổi secret, password hoặc environment configuration.
Không sửa migration đã chạy trên production.
Không thay đổi tên endpoint nếu chưa được yêu cầu.
Không thay đổi response contract nếu chưa được yêu cầu.
Không thêm dependency mới nếu giải pháp hiện tại đã đủ.
Không sửa nhiều module không liên quan trong cùng một lượt.
Nếu không chắc chắn về nghiệp vụ, giữ nguyên hành vi hiện tại.

---

# Skill 4: Spring Security Auditor

Đường dẫn:

```text
.agents/skills/spring-security-auditor/SKILL.md

Nội dung:

---
name: spring-security-auditor
description: Reviews and improves Spring Security, JWT authentication, authorization, refresh token, logout, password handling, endpoint permissions, and security configuration. Use this skill when the user asks to review security code, fix 401 or 403 errors, improve JWT authentication, audit endpoint permissions, or refactor Spring Security configuration.
---

# Spring Security Auditor

## Goal

Kiểm tra và cải tiến cấu hình Spring Security, JWT và phân quyền API.

## Inspection Areas

### Authentication

- `AuthenticationManager`.
- `AuthenticationProvider`.
- `UserDetailsService`.
- `PasswordEncoder`.
- Login flow.
- JWT validation.
- Token expiration.

### Authorization

- `requestMatchers`.
- `hasRole`.
- `hasAnyRole`.
- `hasAuthority`.
- `@PreAuthorize`.
- `@EnableMethodSecurity`.
- Thứ tự khai báo rule.

### JWT Filter

- Có đọc đúng `Authorization: Bearer <token>` không.
- Có xử lý token thiếu hoặc sai định dạng không.
- Có kiểm tra blacklist không.
- Có đặt Authentication vào `SecurityContextHolder` đúng không.
- Có gọi `filterChain.doFilter()` trong mọi trường hợp hợp lệ không.
- Có ghi token vào log không.

### Refresh Token

- Refresh token có thời hạn riêng không.
- Có được lưu và revoke đúng cách không.
- Endpoint refresh có nhận access token sai mục đích không.
- Token cũ có bị vô hiệu hóa khi cần không.

### Logout

- Access token có được đưa vào blacklist không.
- Refresh token có bị revoke không.
- Có xóa Security Context không.
- Có tránh gửi token qua URL không.

### Password

- Có sử dụng BCrypt không.
- Có hard-code password không.
- Có trả password hash qua response không.
- Có validation password phù hợp không.

## Output Format

### 1. Luồng bảo mật hiện tại

Mô tả request đi qua filter và security chain như thế nào.

### 2. Lỗi phát hiện

| Mức độ | Vị trí | Lỗi | Nguy cơ | Cách sửa |
|---|---|---|---|---|

### 3. Code đề xuất

Chỉ sửa những phần cần thiết.

### 4. Test bảo mật

Bao gồm tối thiểu:

- Không có token.
- Token không hợp lệ.
- Token hết hạn.
- Đúng role.
- Sai role.
- Tài khoản bị disabled.
- Token đã logout hoặc blacklist.

## Constraints

- Không bao giờ hiển thị secret hoặc token đầy đủ.
- Không chuyển token sang query parameter.
- Không tắt CSRF mà không xem xét loại ứng dụng.
- Không sử dụng `permitAll()` quá rộng.
- Không đặt `.anyRequest().authenticated()` trước các matcher cụ thể.
- Không xử lý phân quyền chỉ bằng điều kiện trong Controller.
- Không trả thông tin nhạy cảm trong thông báo lỗi.
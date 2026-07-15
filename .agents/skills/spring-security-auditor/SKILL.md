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
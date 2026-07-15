Skill 6: Test Regression Guard

Đường dẫn:

.agents/skills/test-regression-guard/SKILL.md

Nội dung:

---
name: test-regression-guard
description: Creates and updates JUnit 5 and Mockito tests to protect existing behavior before and after Java or Spring Boot refactoring. Use this skill when the user asks to add tests, protect a refactor, verify behavior, improve test coverage, or prevent regression.
---

# Test Regression Guard

## Goal

Tạo test bảo vệ hành vi hiện tại, giúp refactor mà không gây regression.

## Instructions

1. Xác định hành vi cần kiểm tra.

2. Liệt kê các trường hợp:

- Happy path.
- Null input.
- Empty input.
- Invalid input.
- Boundary value.
- Dependency failure.
- Permission denied.
- Resource not found.
- Duplicate data.

3. Chọn loại test phù hợp:

### Unit Test

Sử dụng:

- JUnit 5.
- Mockito.
- `@ExtendWith(MockitoExtension.class)`.
- `@Mock`.
- `@InjectMocks`.

Không khởi động Spring Context khi không cần thiết.

### Controller Test

Sử dụng:

- MockMvc.
- `@WebMvcTest`.
- Mock service.
- Kiểm tra status và JSON response.

### Repository Test

Sử dụng:

- `@DataJpaTest`.
- Database test phù hợp.
- Kiểm tra query tùy chỉnh.

### Integration Test

Chỉ sử dụng khi cần kiểm tra nhiều tầng hoạt động cùng nhau.

4. Test phải theo cấu trúc AAA:

- Arrange.
- Act.
- Assert.

5. Tên test theo dạng:

```text
methodName_condition_expectedResult

Ví dụ:

register_existingUsername_throwsException
login_validCredentials_returnsTokens
approveBooking_wrongRole_returnsForbidden
Không chỉ kiểm tra method được gọi; phải kiểm tra kết quả nghiệp vụ.
Output Requirements
1. Danh sách test case
Test case	Input	Kết quả mong đợi
2. Code test hoàn chỉnh
3. Dependency cần thiết
4. Lệnh chạy test
./gradlew test
5. Phạm vi được bảo vệ

Mô tả hành vi nào đã được test bảo vệ.

Constraints
Không mock class đang được kiểm thử.
Không mock DTO hoặc Entity đơn giản.
Không dùng database thật trong Unit Test.
Không viết test phụ thuộc thứ tự chạy.
Không sử dụng dữ liệu thời gian thực thiếu kiểm soát.
Không bỏ qua test thất bại chỉ để build thành công.
Không sử dụng assertion chung chung khi có thể kiểm tra giá trị cụ thể.
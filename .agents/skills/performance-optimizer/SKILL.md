# Skill 5: Performance Optimizer

Đường dẫn:

.agents/skills/performance-optimizer/SKILL.md

Nội dung:

---
name: performance-optimizer
description: Analyzes and optimizes Java and Spring Boot application performance, including algorithms, collections, database queries, JPA behavior, pagination, caching, memory usage, and repeated operations. Use this skill when the user reports slow code, slow APIs, high memory usage, N+1 queries, inefficient loops, or requests performance optimization.
---

# Performance Optimizer

## Goal

Tối ưu hiệu năng dựa trên bằng chứng và không làm thay đổi kết quả nghiệp vụ.

## Instructions

1. Xác định phần có khả năng gây chậm:

- Thuật toán.
- Vòng lặp.
- Database query.
- Network call.
- Serialization.
- File processing.
- Cache.
- Memory allocation.

2. Xác định độ phức tạp hiện tại:

- Time complexity.
- Space complexity.
- Số database query.
- Số lần gọi API bên ngoài.
- Số object được tạo không cần thiết.

3. Kiểm tra các vấn đề thường gặp:

### Java

- Vòng lặp lồng nhau.
- Tìm kiếm tuyến tính lặp lại.
- Nối chuỗi bằng `+` trong vòng lặp lớn.
- Tạo collection trung gian không cần thiết.
- Sử dụng Stream quá phức tạp.
- Load toàn bộ file vào memory.
- Blocking operation không cần thiết.

### Spring Data JPA

- N+1 query.
- Thiếu pagination.
- `findAll()` với bảng lớn.
- Lazy loading ngoài transaction.
- Fetch join không phù hợp.
- Query không có index hỗ trợ.
- Truy vấn database trong vòng lặp.
- Save từng record thay vì batch khi phù hợp.

### API

- Trả response quá lớn.
- Thiếu pagination.
- Gọi cùng một external API nhiều lần.
- Không có timeout.
- Cache dữ liệu ít thay đổi chưa phù hợp.

4. Không tối ưu khi chưa xác định được điểm nghẽn hợp lý.

5. Mỗi đề xuất phải mô tả trade-off.

## Output Format

### 1. Điểm nghẽn

### 2. Nguyên nhân

### 3. Phương án tối ưu

| Phương án | Lợi ích | Rủi ro | Độ phức tạp |
|---|---|---|---|

### 4. Code sau tối ưu

### 5. So sánh trước và sau

- Độ phức tạp.
- Số query.
- Memory.
- Khả năng đọc.
- Khả năng mở rộng.

### 6. Cách đo kiểm

Ví dụ:

- Logging execution time.
- JMeter.
- Postman Runner.
- Spring Boot Actuator.
- Hibernate SQL logging.
- Database execution plan.

## Constraints

- Không sử dụng cache cho dữ liệu nhạy cảm nếu chưa đánh giá rủi ro.
- Không thêm concurrency nếu code chưa thread-safe.
- Không dùng parallel stream mặc định.
- Không tối ưu làm code khó hiểu mà không có lợi ích rõ ràng.
- Không khẳng định nhanh hơn nếu chưa có căn cứ hoặc phép đo.
- Không bỏ validation hoặc security để tăng tốc.
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
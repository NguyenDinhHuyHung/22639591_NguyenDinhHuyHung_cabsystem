# Login Test Cases

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-AUTH-001 | Người dùng đăng nhập | Đăng nhập bằng email và password hợp lệ | Tài khoản đã tồn tại và được phép sử dụng hệ thống | 1. Mở Login<br>2. Nhập email<br>3. Nhập password<br>4. Nhấn Login | Email: customer01@example.com<br>Password: Password@123 | Đăng nhập thành công; tạo phiên/token và chuyển vào hệ thống. | High |
| TC-AUTH-002 | Người dùng đăng nhập | Email không tồn tại | Hệ thống đang hoạt động | 1. Nhập email không tồn tại<br>2. Nhập password<br>3. Nhấn Login | Email: unknown@example.com<br>Password: Password@123 | Đăng nhập thất bại; không tạo phiên/token. | High |
| TC-AUTH-003 | Người dùng đăng nhập | Password không đúng | Email tồn tại | 1. Nhập email đúng<br>2. Nhập password sai<br>3. Nhấn Login | Email: customer01@example.com<br>Password: Wrong@123 | Đăng nhập thất bại; không tạo phiên/token. | High |
| TC-AUTH-004 | Người dùng đăng nhập | Email để trống | Đang ở màn hình Login | 1. Để trống email<br>2. Nhập password<br>3. Nhấn Login | Email: empty<br>Password: Password@123 | Không đăng nhập; hiển thị lỗi bắt buộc nhập email. | High |
| TC-AUTH-005 | Người dùng đăng nhập | Password để trống | Đang ở màn hình Login | 1. Nhập email<br>2. Để trống password<br>3. Nhấn Login | Email: customer01@example.com<br>Password: empty | Không đăng nhập; hiển thị lỗi bắt buộc nhập password. | High |
| TC-AUTH-006 | Người dùng đăng nhập | Email và password đều rỗng | Đang ở màn hình Login | 1. Không nhập email/password<br>2. Nhấn Login | Email: empty<br>Password: empty | Không đăng nhập; hiển thị validation tương ứng. | High |
| TC-AUTH-007 | Người dùng đăng nhập | Email sai định dạng | Đang ở màn hình Login | 1. Nhập email sai định dạng<br>2. Nhập password<br>3. Nhấn Login | Email: user@@abc<br>Password: Password@123 | Không đăng nhập; hiển thị lỗi định dạng email. | Medium |
| TC-AUTH-008 | Người dùng đăng nhập | Password phân biệt hoa/thường | Tài khoản tồn tại | 1. Nhập email đúng<br>2. Nhập password khác hoa/thường<br>3. Nhấn Login | Password đúng: Password@123<br>Nhập: password@123 | Đăng nhập thất bại nếu password khác với giá trị đã đăng ký. | High |
| TC-AUTH-009 | Người dùng đăng nhập | Request thiếu trường email | API Login hoạt động | 1. Gửi request Login không có email | { password: 'Password@123' } | Request bị validation; không xác thực. | High |
| TC-AUTH-010 | Người dùng đăng nhập | Request thiếu trường password | API Login hoạt động | 1. Gửi request Login không có password | { email: 'customer01@example.com' } | Request bị validation; không xác thực. | High |
| TC-AUTH-011 | Người dùng đăng nhập | Response đăng nhập không lộ password | Đăng nhập thành công | 1. Login bằng dữ liệu hợp lệ<br>2. Kiểm tra response/session | Email: customer01@example.com | Response không chứa password hoặc dữ liệu xác thực nhạy cảm. | High |

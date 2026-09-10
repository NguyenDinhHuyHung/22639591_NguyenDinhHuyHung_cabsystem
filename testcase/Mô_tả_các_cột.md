# Mô tả các cột

| Cột | Ý nghĩa | Mô tả chi tiết | Ví dụ |
| --- | --- | --- | --- |
| Test Case ID | Mã định danh duy nhất của Test Case | Dùng để quản lý, tìm kiếm, truy xuất và tham chiếu Test Case. | TC_LOGIN_001 |
| Test Scenario | Scenario mà Test Case đang kiểm thử | Mô tả chức năng hoặc tình huống cần kiểm thử ở mức tổng quát. Một Test Scenario có thể có nhiều Test Case. | Kiểm tra chức năng đăng nhập |
| Test Case | Trường hợp kiểm thử cụ thể | Mô tả chính xác trường hợp cần kiểm thử được phân rã từ Test Scenario. | Đăng nhập với username và password hợp lệ |
| Preconditions | Điều kiện tiên quyết | Các điều kiện hoặc trạng thái phải được đáp ứng trước khi bắt đầu thực hiện Test Case. | User đã đăng ký tài khoản và đang ở màn hình Login |
| Test Steps | Các bước thực hiện kiểm thử | Mô tả tuần tự các thao tác mà Tester cần thực hiện để kiểm tra Test Case. | 1. Mở Login<br>2. Nhập username<br>3. Nhập password<br>4. Nhấn Login |
| Test Data | Dữ liệu kiểm thử | Dữ liệu đầu vào cụ thể được sử dụng trong quá trình thực hiện Test Case. | Username: user01<br>Password: 123456 |
| Expected Result | Kết quả mong đợi | Kết quả mà hệ thống phải trả về nếu chức năng hoạt động đúng. Dùng để so sánh với Actual Result. | Đăng nhập thành công và chuyển đến trang Home |
| Priority | Mức độ ưu tiên | Cho biết mức độ quan trọng của Test Case và thứ tự ưu tiên khi thực hiện kiểm thử. | High / Medium / Low |

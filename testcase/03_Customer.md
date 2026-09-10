# 03 Customer

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-CUS-001 | Quản lý hồ sơ khách hàng | Xem thông tin cá nhân | Customer đã đăng nhập | 1. Mở Hồ sơ cá nhân | Customer ID hợp lệ | Hiển thị đúng thông tin của Customer đang đăng nhập. | High |
| TC-CUS-002 | Quản lý hồ sơ khách hàng | Cập nhật họ tên hợp lệ | Customer đã đăng nhập | 1. Mở hồ sơ<br>2. Sửa họ tên<br>3. Lưu | Full name: Nguyễn Văn B | Lưu thành công và hiển thị thông tin mới. | High |
| TC-CUS-003 | Quản lý hồ sơ khách hàng | Cập nhật email sai định dạng | Customer đã đăng nhập | 1. Sửa email thành dữ liệu invalid<br>2. Lưu | Email: abc@@xyz | Không lưu; hiển thị lỗi định dạng email. | Medium |
| TC-CUS-004 | Quản lý hồ sơ khách hàng | Cập nhật trường thành chuỗi rỗng | Customer đã đăng nhập | 1. Xóa nội dung trường bắt buộc<br>2. Lưu | Full name: empty | Không cập nhật nếu trường được quy định bắt buộc; hiển thị validation. | High |
| TC-CUS-005 | Quản lý lịch sử chuyến | Xem lịch sử khi đã có chuyến | Customer có lịch sử chuyến | 1. Mở Lịch sử chuyến | Customer có Completed/Cancelled trips | Hiển thị các chuyến thuộc đúng Customer; không lẫn dữ liệu người khác. | High |
| TC-CUS-006 | Quản lý lịch sử chuyến | Xem lịch sử khi chưa có chuyến | Customer chưa từng đặt xe | 1. Mở Lịch sử chuyến | Không có trip | Hiển thị trạng thái danh sách rỗng phù hợp; không phát sinh lỗi. | Medium |
| TC-CUS-007 | Quản lý lịch sử chuyến | Xem chi tiết một chuyến hợp lệ | Customer có trip tồn tại | 1. Chọn một trip trong lịch sử | Trip ID thuộc Customer | Hiển thị đúng pickup, destination, driver, trạng thái và số tiền (nếu có). | High |
| TC-CUS-008 | Quản lý lịch sử chuyến | Truy cập trip của Customer khác | Customer A và B đều có dữ liệu | 1. Customer A cố truy cập Trip ID của Customer B | Trip ID thuộc Customer B | Từ chối truy cập; không lộ dữ liệu chuyến của người khác. | High |

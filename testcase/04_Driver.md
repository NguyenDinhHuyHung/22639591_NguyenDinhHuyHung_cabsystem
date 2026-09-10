# 04 Driver

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-DRV-001 | Quản lý tài xế | Tạo tài khoản Driver với dữ liệu hợp lệ | Operator/Admin có quyền tạo Driver | 1. Nhập hồ sơ Driver<br>2. Lưu | Tên/phone/email hợp lệ | Driver được tạo thành công. | High |
| TC-DRV-002 | Quản lý tài xế | Tạo Driver thiếu họ tên | Operator/Admin đang thao tác | 1. Bỏ trống họ tên<br>2. Nhập phone/email<br>3. Lưu | Full name: empty | Không tạo Driver; hiển thị validation. | High |
| TC-DRV-003 | Quản lý tài xế | Tạo Driver email sai định dạng | Operator/Admin đang thao tác | 1. Nhập email invalid<br>2. Lưu | Email: driver@@cab | Không tạo Driver; hiển thị lỗi email. | Medium |
| TC-DRV-004 | Trạng thái hoạt động tài xế | Chuyển Driver sang AVAILABLE | Driver đã đăng nhập và không có chuyến đang chạy | 1. Chọn trạng thái AVAILABLE | Status: AVAILABLE | Driver ở trạng thái sẵn sàng và có thể được xét khi matching. | High |
| TC-DRV-005 | Trạng thái hoạt động tài xế | Chuyển Driver sang OFFLINE | Driver không có trip đang thực hiện | 1. Chọn OFFLINE | Status: OFFLINE | Driver không còn được xét nhận chuyến mới. | High |
| TC-DRV-006 | Trạng thái hoạt động tài xế | Gửi trạng thái ngoài tập hợp cho phép | Driver hợp lệ | 1. Gửi status không hỗ trợ | Status: VACATION | Từ chối cập nhật; giữ nguyên trạng thái cũ. | Medium |
| TC-DRV-007 | Vị trí tài xế | Cập nhật vị trí hợp lệ | Driver đã xác thực | 1. Gửi latitude, longitude hợp lệ | Latitude: 10.7769<br>Longitude: 106.7009 | Vị trí Driver được cập nhật và có thể dùng cho matching/ETA. | High |
| TC-DRV-008 | Vị trí tài xế | Thiếu latitude | Driver đã xác thực | 1. Gửi location chỉ có longitude | Latitude: missing<br>Longitude: 106.7009 | Không cập nhật vị trí; validation lỗi. | High |
| TC-DRV-009 | Vị trí tài xế | Thiếu longitude | Driver đã xác thực | 1. Gửi location chỉ có latitude | Latitude: 10.7769<br>Longitude: missing | Không cập nhật vị trí; validation lỗi. | High |
| TC-DRV-010 | Vị trí tài xế | Kiểm tra biên tọa độ GPS | Hệ thống nhận tọa độ địa lý | 1. Thử các giá trị biên và ngoài biên<br>2. Cập nhật location | Latitude: -90, 90, -90.0001, 90.0001<br>Longitude: -180, 180, -180.0001, 180.0001 | Chấp nhận tọa độ trong biên địa lý; từ chối giá trị ngoài biên. | Medium |

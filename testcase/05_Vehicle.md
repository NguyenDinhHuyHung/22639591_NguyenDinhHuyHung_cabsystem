# 05 Vehicle

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-VEH-001 | Quản lý phương tiện | Thêm MOTORBIKE hợp lệ | Driver tồn tại | 1. Nhập driverId, biển số, loại xe<br>2. Lưu | VehicleType: MOTORBIKE | Tạo phương tiện và liên kết đúng Driver. | High |
| TC-VEH-002 | Quản lý phương tiện | Thêm CAR hợp lệ | Driver tồn tại | 1. Tạo vehicle loại CAR | VehicleType: CAR | Tạo phương tiện thành công. | High |
| TC-VEH-003 | Quản lý phương tiện | Thêm PREMIUM hợp lệ | Driver tồn tại | 1. Tạo vehicle loại PREMIUM | VehicleType: PREMIUM | Tạo phương tiện thành công. | High |
| TC-VEH-004 | Quản lý phương tiện | Bỏ trống biển số | Driver tồn tại | 1. Không nhập license plate<br>2. Lưu | License plate: empty | Không tạo phương tiện; validation lỗi. | High |
| TC-VEH-005 | Quản lý phương tiện | Bỏ trống loại xe | Driver tồn tại | 1. Không chọn vehicle type<br>2. Lưu | VehicleType: empty | Không tạo phương tiện; validation lỗi. | High |
| TC-VEH-006 | Quản lý phương tiện | Loại xe không được hỗ trợ | Driver tồn tại | 1. Gửi vehicle type không thuộc danh sách | VehicleType: BUS | Từ chối dữ liệu; không tạo phương tiện. | High |
| TC-VEH-007 | Quản lý phương tiện | Driver ID không tồn tại | Không có Driver ID tương ứng | 1. Tạo vehicle với driverId không tồn tại | DriverId: 999999 | Không tạo liên kết phương tiện với Driver không tồn tại. | High |

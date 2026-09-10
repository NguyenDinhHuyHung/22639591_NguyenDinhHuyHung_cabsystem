# 06 Booking

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-BKG-001 | Khách hàng tạo yêu cầu đặt xe | Tạo booking hợp lệ với MOTORBIKE | Customer đã đăng nhập; pickup và destination hợp lệ | 1. Nhập điểm đón<br>2. Nhập điểm đến<br>3. Chọn MOTORBIKE<br>4. Xác nhận | Pickup: 10.7769,106.7009<br>Destination: 10.7820,106.6950<br>Vehicle: MOTORBIKE | Booking được tạo; hệ thống bắt đầu quá trình tìm tài xế. | High |
| TC-BKG-002 | Khách hàng tạo yêu cầu đặt xe | Tạo booking hợp lệ với CAR | Customer đã đăng nhập | 1. Nhập pickup/destination<br>2. Chọn CAR<br>3. Xác nhận | Vehicle: CAR | Booking được tạo thành công và chuyển sang tìm Driver. | High |
| TC-BKG-003 | Khách hàng tạo yêu cầu đặt xe | Tạo booking hợp lệ với PREMIUM | Customer đã đăng nhập | 1. Nhập pickup/destination<br>2. Chọn PREMIUM<br>3. Xác nhận | Vehicle: PREMIUM | Booking được tạo thành công. | High |
| TC-BKG-004 | Khách hàng tạo yêu cầu đặt xe | Điểm đón để trống | Customer đã đăng nhập | 1. Bỏ trống pickup<br>2. Nhập destination/vehicle<br>3. Xác nhận | Pickup: empty | Không tạo booking; yêu cầu nhập điểm đón. | High |
| TC-BKG-005 | Khách hàng tạo yêu cầu đặt xe | Điểm đến để trống | Customer đã đăng nhập | 1. Nhập pickup<br>2. Bỏ trống destination<br>3. Xác nhận | Destination: empty | Không tạo booking; yêu cầu nhập điểm đến. | High |
| TC-BKG-006 | Khách hàng tạo yêu cầu đặt xe | Loại xe để trống | Customer đã đăng nhập | 1. Nhập pickup/destination<br>2. Không chọn loại xe<br>3. Xác nhận | VehicleType: empty | Không tạo booking; yêu cầu chọn loại xe. | High |
| TC-BKG-007 | Khách hàng tạo yêu cầu đặt xe | Loại xe không hợp lệ | Customer đã đăng nhập | 1. Nhập thông tin chuyến<br>2. Gửi loại xe không được hỗ trợ | VehicleType: BUS | Từ chối booking; không bắt đầu matching. | High |
| TC-BKG-008 | Khách hàng tạo yêu cầu đặt xe | Pickup thiếu latitude | Customer đã đăng nhập | 1. Gửi pickup thiếu latitude | Pickup: {longitude:106.7009} | Không tạo booking; location không hợp lệ. | High |
| TC-BKG-009 | Khách hàng tạo yêu cầu đặt xe | Destination thiếu longitude | Customer đã đăng nhập | 1. Gửi destination thiếu longitude | Destination: {latitude:10.7820} | Không tạo booking; location không hợp lệ. | High |
| TC-BKG-010 | Khách hàng tạo yêu cầu đặt xe | Người dùng chưa đăng nhập tạo booking | Không có phiên/token hợp lệ | 1. Mở/gửi yêu cầu đặt xe | No authentication | Từ chối chức năng yêu cầu tài khoản; không tạo booking. | High |
| TC-BKG-011 | Khách hàng tạo yêu cầu đặt xe | Nhấn xác nhận đặt xe nhiều lần liên tiếp | Customer đã nhập dữ liệu hợp lệ | 1. Nhấn Confirm nhiều lần nhanh liên tiếp | Cùng một yêu cầu booking | Không tạo duplicate booking/trip ngoài chủ đích; xử lý idempotent theo thiết kế. | High |

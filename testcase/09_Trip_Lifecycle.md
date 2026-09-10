# 09 Trip Lifecycle

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-TRIP-001 | Quản lý vòng đời chuyến | Trip chuyển sang DRIVER_ASSIGNED sau khi Driver Accept | Trip đang SEARCHING_DRIVER; Driver Accept hợp lệ | 1. Driver Accept<br>2. Kiểm tra trạng thái Trip | SEARCHING_DRIVER -> Accept | Trip được gán Driver và chuyển trạng thái phù hợp. | High |
| TC-TRIP-002 | Quản lý vòng đời chuyến | Driver cập nhật DRIVER_ARRIVING | Trip đã assign Driver | 1. Driver bắt đầu di chuyển tới pickup | Status: DRIVER_ARRIVING | Trip cập nhật DRIVER_ARRIVING; Customer theo dõi được. | High |
| TC-TRIP-003 | Quản lý vòng đời chuyến | Driver cập nhật DRIVER_ARRIVED | Trip đang DRIVER_ARRIVING | 1. Driver xác nhận đã tới điểm đón | Status: DRIVER_ARRIVED | Trip cập nhật DRIVER_ARRIVED; Customer được thông báo. | High |
| TC-TRIP-004 | Quản lý vòng đời chuyến | Driver xác nhận đã đón khách | Trip đang DRIVER_ARRIVED | 1. Driver xác nhận Passenger Picked Up | Status: PASSENGER_PICKED_UP | Trip cập nhật trạng thái đã đón khách. | High |
| TC-TRIP-005 | Quản lý vòng đời chuyến | Bắt đầu chuyến | Khách đã được đón | 1. Driver bắt đầu di chuyển | Status: IN_PROGRESS | Trip chuyển IN_PROGRESS. | High |
| TC-TRIP-006 | Quản lý vòng đời chuyến | Hoàn thành chuyến | Trip đang IN_PROGRESS | 1. Driver xác nhận hoàn thành | Status: COMPLETED | Trip chuyển COMPLETED; hệ thống có thể thực hiện tính cước. | High |
| TC-TRIP-007 | Quản lý vòng đời chuyến | Gửi status rỗng | Trip tồn tại; Driver có quyền cập nhật | 1. Gửi update status với giá trị rỗng | Status: empty/null | Từ chối cập nhật; giữ nguyên trạng thái hiện tại. | High |
| TC-TRIP-008 | Quản lý vòng đời chuyến | Gửi status không thuộc tập cho phép | Trip tồn tại | 1. Gửi status invalid | Status: FINISHED | Từ chối cập nhật. | High |
| TC-TRIP-009 | Quản lý vòng đời chuyến | Chuyển trạng thái ngược từ COMPLETED về IN_PROGRESS | Trip đã COMPLETED | 1. Gửi IN_PROGRESS | COMPLETED -> IN_PROGRESS | Từ chối vì trạng thái kết thúc không được quay lại đang thực hiện. | High |
| TC-TRIP-010 | Quản lý vòng đời chuyến | Cập nhật Trip không thuộc Driver | Driver A được assign Trip A; Driver B đăng nhập | 1. Driver B cập nhật Trip A | Trip assigned to A | Từ chối thao tác; trạng thái không đổi. | High |

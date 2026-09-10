# 10 Tracking

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-TRK-001 | Khách hàng theo dõi chuyến | Theo dõi khi hệ thống đang tìm Driver | Booking đã tạo, chưa assign | 1. Customer mở chi tiết chuyến | Trip: SEARCHING_DRIVER | Hiển thị rõ hệ thống đang tìm tài xế. | High |
| TC-TRK-002 | Khách hàng theo dõi chuyến | Hiển thị Driver sau khi được assign | Driver đã Accept | 1. Customer mở chi tiết chuyến | Trip: DRIVER_ASSIGNED | Hiển thị Driver được assign và thông tin chuyến liên quan. | High |
| TC-TRK-003 | Khách hàng theo dõi chuyến | Theo dõi Driver đang đến | Trip DRIVER_ARRIVING; Driver có location | 1. Customer theo dõi chuyến | Driver location cập nhật | Hiển thị trạng thái đang đến và ETA nếu dịch vụ location/routing cung cấp. | High |
| TC-TRK-004 | Khách hàng theo dõi chuyến | Theo dõi Driver đã đến | Trip DRIVER_ARRIVED | 1. Customer xem trạng thái | Status: DRIVER_ARRIVED | Hiển thị Driver đã tới điểm đón. | High |
| TC-TRK-005 | Khách hàng theo dõi chuyến | Theo dõi khi IN_PROGRESS | Trip đang thực hiện | 1. Customer mở tracking | Status: IN_PROGRESS | Hiển thị trạng thái chuyến đang di chuyển. | High |
| TC-TRK-006 | Khách hàng theo dõi chuyến | Theo dõi sau COMPLETED | Trip đã hoàn thành | 1. Customer mở trip | Status: COMPLETED | Hiển thị trạng thái hoàn thành và số tiền phải trả khi đã tính. | High |
| TC-TRK-007 | Khách hàng theo dõi chuyến | Customer mất mạng rồi kết nối lại | Booking/trip vẫn tồn tại trên server | 1. Mất mạng<br>2. Trong lúc đó trip đổi trạng thái<br>3. Kết nối lại | Network disconnect/reconnect | Sau reconnect hiển thị trạng thái mới nhất; không tạo trip mới. | High |

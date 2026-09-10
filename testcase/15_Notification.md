# 15 Notification

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-NOT-001 | Thông báo nghiệp vụ | Thông báo khi booking được tiếp nhận | Customer tạo booking hợp lệ | 1. Confirm booking | Event: Booking received | Customer nhận thông báo booking đã được hệ thống tiếp nhận. | High |
| TC-NOT-002 | Thông báo nghiệp vụ | Thông báo chuyến mới cho Driver | Driver được chọn để nhận offer | 1. Dispatch offer | Event: New trip | Driver nhận được thông báo chuyến mới. | High |
| TC-NOT-003 | Thông báo nghiệp vụ | Thông báo Customer khi Driver được assign | Driver Accept thành công | 1. Kiểm tra Customer notification | Event: Driver assigned | Customer nhận thông báo có tài xế nhận chuyến. | High |
| TC-NOT-004 | Thông báo nghiệp vụ | Thông báo khi Driver đến điểm đón | Trip chuyển DRIVER_ARRIVED | 1. Driver cập nhật Arrived | Event: Driver arrived | Customer nhận thông báo tài xế đã đến. | High |
| TC-NOT-005 | Thông báo nghiệp vụ | Thông báo khi Trip hoàn thành | Trip chuyển COMPLETED | 1. Complete trip | Event: Trip completed | Customer nhận thông báo chuyến hoàn thành. | High |
| TC-NOT-006 | Thông báo nghiệp vụ | Thông báo kết quả payment SUCCESS | Payment SUCCESS | 1. Nhận kết quả thanh toán | Event: Payment success | Customer nhận thông báo thanh toán thành công. | High |
| TC-NOT-007 | Thông báo nghiệp vụ | Thông báo kết quả payment FAILED | Payment FAILED | 1. Nhận kết quả thanh toán | Event: Payment failed | Customer nhận thông báo thanh toán thất bại. | High |
| TC-NOT-008 | Thông báo nghiệp vụ | Notification Provider bị lỗi | Core booking/trip service vẫn hoạt động | 1. Giả lập lỗi provider<br>2. Tạo/tiếp tục booking | Notification service unavailable | Lỗi thông báo không làm toàn bộ chức năng đặt xe ngừng hoạt động; sự kiện được xử lý/ghi nhận theo thiết kế. | High |

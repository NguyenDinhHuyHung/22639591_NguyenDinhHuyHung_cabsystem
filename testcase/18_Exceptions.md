# 18 Exceptions

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-EXC-001 | Xử lý ngoại lệ | Customer mất mạng khi đang tìm Driver | Booking đã tạo | 1. Ngắt mạng Customer<br>2. Hệ thống tiếp tục xử lý<br>3. Kết nối lại | Network loss | Booking không tự mất; khi reconnect Customer nhận trạng thái mới nhất theo policy. | High |
| TC-EXC-002 | Xử lý ngoại lệ | Driver mất mạng trước khi Accept offer | Offer đang chờ | 1. Driver mất mạng<br>2. Hết điều kiện phản hồi | Driver disconnected | Hệ thống không treo booking; chuyển sang Driver khác theo timeout/eligibility policy. | High |
| TC-EXC-003 | Xử lý ngoại lệ | Driver mất mạng khi đang IN_PROGRESS | Trip đang chạy | 1. Ngắt mạng Driver<br>2. Kiểm tra trip/customer tracking | Driver disconnected during trip | Trip không bị tự động hoàn thành/hủy sai; hệ thống xử lý theo Network Failure Policy cần BA chốt. | High |
| TC-EXC-004 | Xử lý ngoại lệ | Payment Service lỗi nhưng Booking vẫn hoạt động | Payment component unavailable | 1. Tạo booking mới<br>2. Matching/Trip | Payment service down | Booking/dispatch/trip không bị ngừng toàn hệ thống. | High |
| TC-EXC-005 | Xử lý ngoại lệ | Notification Service lỗi nhưng Booking vẫn hoạt động | Notification component unavailable | 1. Tạo và thực hiện booking | Notification service down | Core booking/trip tiếp tục hoạt động; lỗi notification được cô lập/ghi nhận. | High |
| TC-EXC-006 | Xử lý ngoại lệ | Không tìm được Driver sau toàn bộ quá trình matching | Không còn Driver eligible | 1. Tạo booking<br>2. Matching đến khi không còn candidate | No eligible driver | Customer được thông báo rõ ràng; không bị yêu cầu tạo lại trong quá trình retry nội bộ. | High |
| TC-EXC-007 | Xử lý ngoại lệ | Dữ liệu đầu vào null ngoài dự kiến | Endpoint/chức năng đang hoạt động | 1. Gửi null cho field bắt buộc trong booking/payment/rating | Required field = null | Validation thất bại có kiểm soát; không crash service. | High |
| TC-EXC-008 | Xử lý ngoại lệ | Ký tự đặc biệt/chuỗi rất dài ở trường text | Có trường text như fullName/comment/reason | 1. Nhập ký tự Unicode, emoji, chuỗi tại/qua max length cấu hình | Text edge cases | Không gây lỗi hệ thống/SQL injection/XSS; áp dụng đúng giới hạn đã cấu hình. | Medium |

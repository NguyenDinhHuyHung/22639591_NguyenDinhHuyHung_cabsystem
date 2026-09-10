# 11 Cancellation

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-CAN-001 | Hủy booking/chuyến | Customer hủy khi đang SEARCHING_DRIVER | Booking đang tìm Driver | 1. Customer chọn Cancel<br>2. Xác nhận hủy | Reason: Thay đổi kế hoạch | Dừng quá trình tìm Driver; hủy các offer đang chờ; trạng thái chuyển CANCELLED theo thiết kế. | High |
| TC-CAN-002 | Hủy booking/chuyến | Customer hủy khi offer đang chờ Driver phản hồi | Offer đang active | 1. Customer Cancel | Active driver offer | Offer bị vô hiệu; Driver không được Accept sau khi booking đã hủy. | High |
| TC-CAN-003 | Hủy booking/chuyến | Driver Accept sau khi Customer đã hủy | Booking CANCELLED | 1. Driver dùng offer cũ để Accept | Cancelled booking | Từ chối Accept; không phục hồi trip. | High |
| TC-CAN-004 | Hủy booking/chuyến | Lý do hủy để trống | Booking cho phép hủy; trường reason là tùy chọn theo API | 1. Không nhập reason<br>2. Xác nhận hủy | Reason: empty | Hủy được nếu reason không bắt buộc; không phát sinh lỗi chỉ vì reason rỗng. | Medium |
| TC-CAN-005 | Hủy booking/chuyến | Kiểm tra phí hủy | Chính sách phí hủy chưa được khách hàng chốt | 1. Hủy ở các giai đoạn khác nhau<br>2. Kiểm tra phí | SEARCHING_DRIVER / DRIVER_ASSIGNED / ARRIVED | Kết quả tuân theo Cancellation Policy sau khi BA chốt; không tự suy diễn phí. | Medium |
| TC-CAN-006 | Hủy booking/chuyến | Hủy trip đã COMPLETED | Trip đã COMPLETED | 1. Thực hiện Cancel | Status: COMPLETED | Từ chối hủy vì trip đã kết thúc. | High |

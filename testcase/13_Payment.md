# 13 Payment

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-PAY-001 | Thanh toán | Thanh toán CASH sau chuyến hoàn thành | Trip COMPLETED; fare đã xác định | 1. Chọn CASH<br>2. Xác nhận thanh toán/thu tiền | PaymentMethod: CASH | Tạo giao dịch đúng Trip và số tiền; trạng thái được cập nhật theo quy trình. | High |
| TC-PAY-002 | Thanh toán | Thanh toán ONLINE thành công | Trip COMPLETED; Payment Provider hoạt động | 1. Chọn ONLINE<br>2. Thực hiện thanh toán<br>3. Provider trả success | PaymentMethod: ONLINE<br>Provider result: SUCCESS | Payment SUCCESS; Customer nhận thông báo kết quả. | High |
| TC-PAY-003 | Thanh toán | ONLINE payment thất bại | Trip COMPLETED | 1. Chọn ONLINE<br>2. Provider trả failed | Provider result: FAILED | Ghi nhận FAILED; thông báo Customer; cho phép xử lý lại theo chính sách. | High |
| TC-PAY-004 | Thanh toán | Payment method để trống | Trip COMPLETED | 1. Gửi payment không có paymentMethod | PaymentMethod: empty/null | Không tạo payment; validation lỗi. | High |
| TC-PAY-005 | Thanh toán | Trip ID để trống | Có Customer hợp lệ | 1. Gửi payment không có tripId | TripId: empty/null | Không tạo payment; validation lỗi. | High |
| TC-PAY-006 | Thanh toán | Payment method không hỗ trợ | Trip COMPLETED | 1. Gửi paymentMethod invalid | PaymentMethod: CRYPTO | Từ chối dữ liệu; chỉ chấp nhận phương thức được hỗ trợ. | High |
| TC-PAY-007 | Thanh toán | Thanh toán cho Trip chưa COMPLETED | Trip IN_PROGRESS | 1. Tạo payment | Trip status: IN_PROGRESS | Không finalize thanh toán cho chuyến chưa hoàn thành. | High |
| TC-PAY-008 | Thanh toán | Payment Provider timeout/mất kết nối | Trip COMPLETED; thanh toán ONLINE | 1. Gửi payment<br>2. Provider không phản hồi | Provider timeout | Không ghi nhận SUCCESS sai; lưu trạng thái phù hợp và cho phép xử lý/retry theo policy. | High |
| TC-PAY-009 | Thanh toán | Retry sau payment FAILED | Payment trước đó FAILED | 1. Customer thực hiện lại thanh toán | Previous payment: FAILED | Cho phép xử lý lại theo policy; lịch sử không bị mất. | High |
| TC-PAY-010 | Thanh toán | Không lưu trực tiếp dữ liệu thẻ/tài khoản nhạy cảm | Có giao dịch ONLINE | 1. Thanh toán<br>2. Kiểm tra dữ liệu CAB lưu/log | Card/account sensitive data | CAB không lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản. | High |
| TC-PAY-011 | Thanh toán | Callback SUCCESS bị gửi lặp | Provider đã trả SUCCESS một lần | 1. Gửi lại callback cùng giao dịch | Duplicate payment callback | Không tạo giao dịch/doanh thu trùng; xử lý idempotent. | High |

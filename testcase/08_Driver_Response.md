# 08 Driver Response

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-DSP-001 | Phân công tài xế | Driver Accept offer hợp lệ | Driver nhận được offer cho booking; offer còn hiệu lực | 1. Driver mở offer<br>2. Chọn Accept | Offer valid | Driver được assign chính thức cho trip; Customer nhận thông tin Driver. | High |
| TC-DSP-002 | Phân công tài xế | Driver Reject offer | Driver nhận offer hợp lệ | 1. Chọn Reject | Offer valid | Driver không được assign; hệ thống tiếp tục tìm Driver khác; Customer không phải tạo booking lại. | High |
| TC-DSP-003 | Phân công tài xế | Driver không phản hồi đến hết timeout cấu hình | Offer đã gửi; timeout T được cấu hình | 1. Không Accept/Reject<br>2. Chờ đến T | T = giá trị cấu hình (chưa chốt trong Customer Requirement) | Offer hết hiệu lực; hệ thống tiếp tục tìm Driver khác; cần BA xác nhận giá trị T. | High |
| TC-DSP-004 | Phân công tài xế | Driver Accept sau khi offer đã timeout | Offer của Driver A đã hết hạn | 1. Sau timeout, Driver A bấm Accept | Expired offer | Không assign Driver A bằng offer đã hết hiệu lực. | High |
| TC-DSP-005 | Phân công tài xế | Driver A Reject, Driver B Accept | A và B đều từng đủ điều kiện | 1. Gửi offer A<br>2. A Reject<br>3. Hệ thống gửi B<br>4. B Accept | A Reject; B Accept | B được assign; booking ban đầu tiếp tục; không tạo booking mới. | High |
| TC-DSP-006 | Phân công tài xế | Hai Driver Accept gần như đồng thời | Thiết kế có thể gửi nhiều offer hoặc race condition xảy ra | 1. A và B cùng Accept gần thời điểm nhau | Concurrent Accept | Chỉ một Driver được assign; Driver còn lại nhận kết quả không còn hiệu lực/đã có Driver. | High |
| TC-DSP-007 | Phân công tài xế | Driver đã BUSY cố Accept chuyến khác | Driver đã được assign trip A | 1. Driver nhận/cố Accept trip B | Driver status: BUSY | Không cho Driver nhận đồng thời trip B. | High |
| TC-DSP-008 | Phân công tài xế | Offer không thuộc Driver hiện tại | Trip offer được gửi cho Driver A | 1. Driver B cố Accept offer của A | Driver B != offered driver | Từ chối thao tác; không thay đổi assignment. | High |

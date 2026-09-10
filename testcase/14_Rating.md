# 14 Rating

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-RAT-001 | Đánh giá tài xế | Đánh giá 1 sao sau trip hoàn thành | Trip COMPLETED; Customer là chủ chuyến | 1. Chọn rating = 1<br>2. Submit | Rating: 1 | Đánh giá được lưu thành công. | High |
| TC-RAT-002 | Đánh giá tài xế | Đánh giá 5 sao sau trip hoàn thành | Trip COMPLETED | 1. Chọn rating = 5<br>2. Submit | Rating: 5 | Đánh giá được lưu thành công. | High |
| TC-RAT-003 | Đánh giá tài xế | Rating nhỏ hơn giá trị tối thiểu | Trip COMPLETED | 1. Gửi rating = 0 | Rating: 0 | Từ chối; rating hợp lệ nằm trong khoảng 1-5. | High |
| TC-RAT-004 | Đánh giá tài xế | Rating lớn hơn giá trị tối đa | Trip COMPLETED | 1. Gửi rating = 6 | Rating: 6 | Từ chối; rating hợp lệ nằm trong khoảng 1-5. | High |
| TC-RAT-005 | Đánh giá tài xế | Rating để trống | Trip COMPLETED | 1. Submit không chọn rating | Rating: empty/null | Không tạo đánh giá; rating là dữ liệu bắt buộc. | High |
| TC-RAT-006 | Đánh giá tài xế | Đánh giá trước khi chuyến hoàn thành | Trip IN_PROGRESS | 1. Submit rating | Rating: 5 | Từ chối vì chỉ được đánh giá sau khi trip hoàn thành. | High |
| TC-RAT-007 | Đánh giá tài xế | Đánh giá trip đã CANCELLED | Trip CANCELLED | 1. Submit rating | Rating: 5 | Từ chối đánh giá. | High |
| TC-RAT-008 | Đánh giá tài xế | Comment để trống nhưng rating hợp lệ | Trip COMPLETED | 1. Rating = 4<br>2. Không nhập comment<br>3. Submit | Rating: 4<br>Comment: empty | Lưu rating thành công nếu comment là tùy chọn. | Medium |

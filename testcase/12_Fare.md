# 12 Fare

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-FARE-001 | Tính cước | Tính cước sau khi trip COMPLETED | Trip đã hoàn thành | 1. Chuyển Trip COMPLETED<br>2. Thực hiện/kiểm tra tính cước | Trip có thông tin dịch vụ và chuyến | Hệ thống xác định số tiền phải trả theo Fare Policy. | High |
| TC-FARE-002 | Tính cước | Không tính cước chính thức khi trip chưa hoàn thành | Trip đang IN_PROGRESS | 1. Yêu cầu final fare | Status: IN_PROGRESS | Không finalize cước trước khi hoàn thành chuyến. | High |
| TC-FARE-003 | Tính cước | Fare gắn đúng Trip/Customer | Có nhiều trip hoàn thành | 1. Tính cước Trip A<br>2. Xem Trip A/B | Trip A và Trip B khác nhau | Fare của Trip A không bị gắn nhầm sang Trip B. | High |
| TC-FARE-004 | Tính cước | Kiểm tra số tiền không âm | Trip COMPLETED | 1. Tính fare | Trip hợp lệ | Final fare không âm; dữ liệu bất thường phải được xử lý/ghi nhận. | High |
| TC-FARE-005 | Tính cước | Thiếu dữ liệu cần cho công thức cước | Trip COMPLETED nhưng thiếu một dữ liệu đầu vào cần thiết | 1. Thực hiện tính cước | Missing fare input | Không tạo số tiền sai; hệ thống xử lý lỗi/exception theo thiết kế. | High |
| TC-FARE-006 | Tính cước | Kiểm tra giá trị biên theo Fare Policy | Công thức và min/max fare chưa được khách hàng chốt | 1. Test các mức min-1/min/max/max+1 khi policy được xác nhận | Boundary values theo cấu hình | Tính đúng theo policy; hiện cần BA xác nhận chi tiết công thức. | Medium |

# 07 Driver Matching

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-MAT-001 | Tự động tìm tài xế phù hợp | Có Driver AVAILABLE, đúng loại xe và gần pickup | Driver A AVAILABLE; vehicle phù hợp; có location | 1. Customer tạo booking<br>2. Hệ thống lọc Driver | Booking: CAR<br>Driver A: AVAILABLE + CAR + near pickup | Driver A thuộc tập Driver đủ điều kiện và được xét ưu tiên. | High |
| TC-MAT-002 | Tự động tìm tài xế phù hợp | Driver OFFLINE dù ở gần khách | Driver A OFFLINE | 1. Tạo booking gần Driver A<br>2. Matching | Driver A: OFFLINE | Driver A không được chọn/gửi offer. | High |
| TC-MAT-003 | Tự động tìm tài xế phù hợp | Driver BUSY không nhận thêm chuyến | Driver A đang thực hiện trip khác | 1. Tạo booking mới<br>2. Matching | Driver A: BUSY | Driver A không được chọn cho booking mới. | High |
| TC-MAT-004 | Tự động tìm tài xế phù hợp | Driver đúng vị trí nhưng sai loại xe | Booking CAR; Driver A có MOTORBIKE | 1. Tạo booking CAR<br>2. Matching | Requested: CAR<br>Driver vehicle: MOTORBIKE | Driver A bị loại khỏi tập phù hợp. | High |
| TC-MAT-005 | Tự động tìm tài xế phù hợp | Nhiều Driver cùng phù hợp | A/B/C đều AVAILABLE và đúng loại xe | 1. Tạo booking<br>2. Hệ thống xếp hạng Driver | A/B/C có vị trí/tiêu chí khác nhau | Hệ thống ưu tiên theo rule cấu hình; tiêu chí chi tiết cần BA xác nhận. | High |
| TC-MAT-006 | Tự động tìm tài xế phù hợp | Không có Driver phù hợp | Không có Driver thỏa điều kiện | 1. Tạo booking<br>2. Chờ matching kết thúc | 0 Driver eligible | Không assign Driver; Customer nhận thông báo rõ ràng không tìm được tài xế. | High |
| TC-MAT-007 | Tự động tìm tài xế phù hợp | Driver thiếu dữ liệu vị trí | Driver AVAILABLE nhưng không có location hiện tại | 1. Tạo booking<br>2. Matching | Driver location: null | Không ưu tiên/không chọn Driver nếu không đủ dữ liệu cần cho matching; xử lý theo rule. | High |
| TC-MAT-008 | Tự động tìm tài xế phù hợp | Driver có location ngoài phạm vi cấu hình | Driver AVAILABLE, đúng xe nhưng quá xa | 1. Tạo booking<br>2. Matching | Distance > configured matching radius | Driver bị loại nếu vượt bán kính/điều kiện cấu hình; bán kính cần BA xác nhận. | Medium |

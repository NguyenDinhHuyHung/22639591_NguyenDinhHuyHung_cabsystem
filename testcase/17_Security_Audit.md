# 17 Security Audit

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-SEC-001 | Xác thực và phân quyền | Customer truy cập chức năng của Driver | Customer đã login | 1. Customer gọi/chọn chức năng cập nhật trip như Driver | Role: CUSTOMER | Từ chối truy cập. | High |
| TC-SEC-002 | Xác thực và phân quyền | Driver truy cập Dashboard Admin | Driver đã login | 1. Truy cập admin dashboard | Role: DRIVER | Từ chối truy cập. | High |
| TC-SEC-003 | Xác thực và phân quyền | Operator không có quyền nhạy cảm thực hiện thao tác Admin | Operator thông thường | 1. Thực hiện thao tác nhạy cảm bị giới hạn | Role: OPERATOR | Từ chối theo RBAC; không thay đổi dữ liệu. | High |
| TC-SEC-004 | Xác thực và phân quyền | Request không có token | Endpoint yêu cầu authentication | 1. Gửi request không có token | Authorization: missing | Từ chối truy cập. | High |
| TC-SEC-005 | Xác thực và phân quyền | Token không hợp lệ/hết hạn | Có token invalid/expired | 1. Gửi request protected endpoint | Invalid/expired token | Từ chối truy cập; không xử lý nghiệp vụ. | High |
| TC-SEC-006 | Bảo vệ dữ liệu | Customer A truy cập dữ liệu vị trí/chuyến của Customer B | Có hai Customer | 1. Customer A yêu cầu dữ liệu của B | Foreign resource ID | Từ chối và không lộ dữ liệu. | High |
| TC-SEC-007 | Audit log | Ghi log thao tác quản trị quan trọng | Admin/Operator có quyền thực hiện thao tác | 1. Thực hiện thay đổi quan trọng<br>2. Kiểm tra audit | Thao tác quản trị | Có audit record đủ để truy vết actor, hành động, thời điểm và đối tượng theo thiết kế. | High |
| TC-SEC-008 | Audit log | Không cho user thông thường sửa/xóa audit trái phép | Customer/Driver đăng nhập | 1. Cố truy cập/chỉnh sửa audit log | Role: CUSTOMER/DRIVER | Từ chối truy cập. | High |

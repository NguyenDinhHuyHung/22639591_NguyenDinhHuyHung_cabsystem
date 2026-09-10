# 16 Admin Report

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TC-ADM-001 | Quản trị vận hành | Operator xem danh sách Customer | Operator đã đăng nhập và có quyền | 1. Mở Customer Management | Role: OPERATOR | Hiển thị danh sách theo quyền được cấp. | High |
| TC-ADM-002 | Quản trị vận hành | Operator xem Driver và trạng thái | Operator có quyền | 1. Mở Driver Management | Driver statuses available | Hiển thị Driver và trạng thái hiện tại. | High |
| TC-ADM-003 | Quản trị vận hành | Operator xem phương tiện | Operator có quyền | 1. Mở Vehicle Management | Vehicles exist | Hiển thị thông tin phương tiện theo quyền. | High |
| TC-ADM-004 | Quản trị vận hành | Operator xem các chuyến đang diễn ra | Có trip đang chạy | 1. Mở Trip Monitoring | Trip IN_PROGRESS/ARRIVING... | Hiển thị các chuyến đang diễn ra và trạng thái. | High |
| TC-ADM-005 | Quản trị vận hành | Tra cứu lịch sử giao dịch | Có payment history | 1. Mở Transaction lookup<br>2. Tra cứu trip/payment | Trip/Payment ID hợp lệ | Trả đúng lịch sử giao dịch. | High |
| TC-ADM-006 | Báo cáo vận hành | Đếm tổng số chuyến | Có dữ liệu trip | 1. Mở dashboard/report | Dataset có N trips | Total trips phản ánh đúng dữ liệu. | High |
| TC-ADM-007 | Báo cáo vận hành | Đếm chuyến hoàn thành và hủy | Có COMPLETED/CANCELLED trips | 1. Mở report | Mixed trip statuses | Completed/Cancelled counts đúng theo trạng thái. | High |
| TC-ADM-008 | Báo cáo vận hành | Tổng doanh thu | Có giao dịch hợp lệ | 1. Mở Revenue report | Payments có SUCCESS/FAILED | Doanh thu được tính theo dữ liệu giao dịch được doanh nghiệp xác nhận; giao dịch thất bại không bị tính sai. | High |
| TC-ADM-009 | Báo cáo vận hành | Báo cáo khi chưa có dữ liệu | Hệ thống mới/không có dữ liệu kỳ chọn | 1. Mở dashboard | No data | Hiển thị 0/empty state phù hợp; không lỗi chia cho 0. | Medium |

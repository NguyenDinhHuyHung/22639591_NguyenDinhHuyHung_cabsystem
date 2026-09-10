# Test Coverage

| STT | Test Scenario/Module | Số Test Case | Coverage chính |
| --- | --- | --- | --- |
| 1 | 01 Register | 11 | Đăng ký: valid/invalid/empty/duplicate/boundary |
| 2 | 02 Login | 11 | Đăng nhập: valid/invalid/empty/authentication |
| 3 | 03 Customer | 8 | Profile, lịch sử chuyến, dữ liệu chéo Customer |
| 4 | 04 Driver | 10 | Profile, status, location, empty/invalid/boundary |
| 5 | 05 Vehicle | 7 | Vehicle type, required fields, invalid driver |
| 6 | 06 Booking | 11 | Pickup/destination/vehicle, valid/invalid/empty/duplicate |
| 7 | 07 Driver Matching | 8 | Available/status/vehicle/location/ranking/no driver |
| 8 | 08 Driver Response | 8 | Accept/Reject/Timeout/concurrency/expired offer |
| 9 | 09 Trip Lifecycle | 10 | State transitions, invalid/null/unauthorized state |
| 10 | 10 Tracking | 7 | Trip status, Driver info, reconnect |
| 11 | 11 Cancellation | 6 | Cancel/search/offer/fee policy/terminal state |
| 12 | 12 Fare | 6 | Completed-only, missing data, boundary by policy |
| 13 | 13 Payment | 11 | Cash/Online/failed/retry/null/invalid/idempotency/security |
| 14 | 14 Rating | 8 | Boundary 1-5, empty, invalid lifecycle |
| 15 | 15 Notification | 8 | Booking/driver/trip/payment events + provider failure |
| 16 | 16 Admin Report | 9 | Operations, transaction lookup, dashboard/report |
| 17 | 17 Security Audit | 8 | RBAC, token, data isolation, audit trail |
| 18 | 18 Exceptions | 8 | Network/provider/null/oversized text/no driver |
| 19 | 19 E2E | 6 | Happy path và các exception end-to-end |

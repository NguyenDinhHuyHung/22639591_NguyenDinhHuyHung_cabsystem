# CAB SYSTEM -- BUSINESS ANALYSIS DOCUMENT

## Đề tài

**Dự án xây dựng hệ thống CAB System -- Nền tảng đặt xe**

------------------------------------------------------------------------

## B1. Phân tích yêu cầu và Business Vision/Context

### 1. Business Context

Công ty ABC đang cung cấp dịch vụ đặt xe trực tuyến thông qua tổng đài
và một ứng dụng đơn giản. Mô hình hiện tại có thể đáp ứng nhu cầu cơ bản
nhưng chưa phù hợp khi số lượng khách hàng, tài xế và chuyến đi tăng.

Quy trình hiện tại phụ thuộc nhiều vào thao tác thủ công, đặc biệt là
việc tìm và phân công tài xế. Dữ liệu chuyến đi, tài xế, thanh toán và
vận hành chưa được quản lý tập trung.

ABC muốn chuyển từ một ứng dụng đặt xe đơn giản thành một **CAB
Platform** có kiến trúc linh hoạt, có khả năng mở rộng và hỗ trợ toàn bộ
vòng đời của một chuyến xe.

### 2. Business Problems

  -----------------------------------------------------------------------
  ID                      Vấn đề hiện tại         Ảnh hưởng
  ----------------------- ----------------------- -----------------------
  BP01                    Phân công tài xế chủ    Tốn thời gian, khó mở
                          yếu thủ công            rộng

  BP02                    Khách hàng khó theo dõi Trải nghiệm khách hàng
                          chuyến đi               kém

  BP03                    Chưa tự động tìm tài xế Hiệu quả điều phối thấp
                          phù hợp                 

  BP04                    Thanh toán chưa quản lý Khó đối soát giao dịch
                          tập trung               

  BP05                    Dữ liệu vận hành phân   Khó báo cáo và phân
                          tán                     tích

  BP06                    Hệ thống hiện tại khó   Không đáp ứng tốt khi
                          mở rộng                 lượng người dùng tăng

  BP07                    Các thành phần phụ      Lỗi thanh toán/thông
                          thuộc nhiều vào nhau    báo có thể ảnh hưởng
                                                  đặt xe

  BP08                    Khả năng mở rộng tính   Khó thêm dịch vụ,
                          năng hạn chế            payment provider,
                                                  notification provider

  BP09                    Quản trị và phân quyền  Rủi ro bảo mật
                          chưa hoàn thiện         

  BP10                    Khả năng lưu vết hoạt   Khó kiểm tra khi xảy ra
                          động còn hạn chế        sự cố
  -----------------------------------------------------------------------

### 3. Business Vision

> Xây dựng CAB System thành nền tảng đặt xe trực tuyến có khả năng quản
> lý xuyên suốt quá trình từ đặt chuyến, tìm tài xế, thực hiện chuyến,
> tính cước, thanh toán, thông báo, đánh giá đến quản trị và báo cáo.

Hệ thống cần có khả năng mở rộng độc lập từng thành phần và cho phép bổ
sung dịch vụ mới trong tương lai mà không phải xây dựng lại toàn bộ nền
tảng.

------------------------------------------------------------------------

## B2. Ma trận Stakeholder

  --------------------------------------------------------------------------------
  Stakeholder    Vai trò                       Power         Interest Nhóm quản lý
  -------------- ------------------ ---------------- ---------------- ------------
  Ban giám đốc   Sponsor/Decision                Cao              Cao Manage
  ABC            Maker                                                Closely

  Nhân viên vận  Quản trị và vận                 Cao              Cao Manage
  hành           hành                                                 Closely

  Khách hàng     Người đặt xe                   Thấp              Cao Keep
                                                                      Informed

  Tài xế         Người cung cấp           Trung bình              Cao Keep
                 chuyến đi                                            Informed /
                                                                      Engage

  Bộ phận tài    Theo dõi thanh           Trung bình       Trung bình Keep
  chính          toán/doanh thu                                       Satisfied

  Payment        Xử lý thanh toán         Trung bình       Trung bình Keep
  Provider       điện tử                                              Satisfied

  Notification   SMS/Email/Push                 Thấp       Trung bình Monitor
  Provider                                                            

  Đội phát triển Xây dựng hệ thống        Trung bình              Cao Engage

  BA             Phân tích yêu cầu        Trung bình              Cao Engage

  QA/Tester      Kiểm thử hệ thống        Trung bình              Cao Engage
  --------------------------------------------------------------------------------

``` text
                  INTEREST
               Thấp                 Cao
        +------------------+----------------------+
POWER   |                  | Ban giám đốc        |
Cao     | Keep Satisfied   | Nhân viên vận hành  |
        |                  | Manage Closely       |
        +------------------+----------------------+
        | Payment/         | Khách hàng           |
Thấp    | Notification     | Tài xế               |
        | Monitor          | Keep Informed        |
        +------------------+----------------------+
```

------------------------------------------------------------------------

## B3. Business Goals

  -----------------------------------------------------------------------
  ID                      Business Goal           Diễn giải
  ----------------------- ----------------------- -----------------------
  BG01                    Giảm thời gian tìm tài  Tự động hóa quá trình
                          xế                      tìm và đề xuất tài xế
                                                  phù hợp

  BG02                    Tự động hóa điều phối   Giảm phụ thuộc vào nhân
                          chuyến                  viên điều phối

  BG03                    Nâng cao trải nghiệm    Cho phép khách theo dõi
                          khách hàng              toàn bộ trạng thái
                                                  chuyến

  BG04                    Nâng cao hiệu quả hoạt  Tài xế nhận thông báo
                          động tài xế             và chủ động nhận/từ
                                                  chối chuyến

  BG05                    Quản lý thanh toán tập  Hỗ trợ tiền mặt và
                          trung                   thanh toán điện tử

  BG06                    Tăng khả năng kiểm soát Theo dõi khách hàng,
                          vận hành                tài xế, xe, chuyến và
                                                  giao dịch

  BG07                    Cung cấp dữ liệu quản   Báo cáo chuyến, doanh
                          trị                     thu và hiệu quả

  BG08                    Tăng khả năng mở rộng   Các thành phần có thể
                                                  scale độc lập

  BG09                    Tăng tính ổn định       Lỗi một thành phần
                                                  không làm dừng toàn bộ
                                                  nền tảng

  BG10                    Tăng bảo mật và khả     Xác thực, phân quyền,
                          năng kiểm toán          bảo vệ dữ liệu và audit
                                                  log

  BG11                    Hỗ trợ phát triển lâu   Có thể thêm dịch vụ,
                          dài                     payment/notification
                                                  provider
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## B4. Xác định phạm vi

### In Scope

  Module                       Phạm vi
  ---------------------------- ---------------------------------
  M01 -- Authentication        Đăng ký, đăng nhập, xác thực
  M02 -- Customer Management   Quản lý khách hàng
  M03 -- Driver Management     Quản lý tài xế
  M04 -- Vehicle Management    Quản lý phương tiện
  M05 -- Booking               Đặt chuyến
  M06 -- Driver Matching       Tìm và phân công tài xế
  M07 -- Trip Management       Quản lý quá trình chuyến đi
  M08 -- Driver Location       Cập nhật/theo dõi vị trí tài xế
  M09 -- Fare                  Tính cước
  M10 -- Payment               Tiền mặt và thanh toán điện tử
  M11 -- Notification          Thông báo khách hàng/tài xế
  M12 -- Rating                Đánh giá tài xế
  M13 -- Administration        Quản trị hệ thống
  M14 -- Reporting             Báo cáo hoạt động
  M15 -- Audit & Security      Phân quyền và lưu vết

### Out of Scope -- MVP

-   Chương trình loyalty/điểm thưởng.
-   Dịch vụ giao hàng hoặc đặt đồ ăn.
-   Ví điện tử riêng của CAB.
-   Hệ thống kế toán hoàn chỉnh.
-   AI dự báo nhu cầu.
-   Dynamic pricing phức tạp khi chính sách chưa được xác nhận.
-   Xây dựng hệ thống bản đồ riêng.
-   Lưu trực tiếp thông tin thẻ ngân hàng nhạy cảm.

------------------------------------------------------------------------

## B5. Business Requirements

  -----------------------------------------------------------------------
  ID                      Tên                     Diễn giải
  ----------------------- ----------------------- -----------------------
  BR01                    Quản lý tài khoản       Hệ thống hỗ trợ tài
                                                  khoản khách hàng, tài
                                                  xế và nhân viên

  BR02                    Đặt chuyến              Khách hàng tạo yêu cầu
                                                  chuyến từ điểm đón đến
                                                  điểm đến

  BR03                    Lựa chọn dịch vụ        Khách hàng lựa chọn
                                                  loại xe/dịch vụ phù hợp

  BR04                    Tìm tài xế              Hệ thống tự động tìm
                                                  tài xế phù hợp

  BR05                    Phân công tài xế        Gửi yêu cầu và xử lý
                                                  tài xế nhận/từ
                                                  chối/không phản hồi

  BR06                    Theo dõi chuyến         Theo dõi trạng thái và
                                                  thông tin chuyến

  BR07                    Quản lý vị trí tài xế   Thu thập vị trí để hỗ
                                                  trợ matching và ETA

  BR08                    Thực hiện chuyến        Tài xế cập nhật trạng
                                                  thái chuyến

  BR09                    Tính cước               Xác định số tiền sau
                                                  chuyến

  BR10                    Thanh toán              Hỗ trợ tiền mặt và
                                                  thanh toán điện tử

  BR11                    Thông báo               Thông báo các sự kiện
                                                  quan trọng

  BR12                    Lịch sử chuyến          Khách hàng tra cứu
                                                  chuyến đã thực hiện

  BR13                    Đánh giá                Khách hàng đánh giá tài
                                                  xế

  BR14                    Quản trị                Quản lý khách hàng, tài
                                                  xế, xe và chuyến

  BR15                    Báo cáo                 Báo cáo chuyến, doanh
                                                  thu và hiệu quả

  BR16                    Phân quyền              Kiểm soát chức năng
                                                  quản trị

  BR17                    Audit                   Lưu vết các hoạt động
                                                  quan trọng
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## B6. Business Process -- Quy trình đặt chuyến

``` text
[Bắt đầu]
    |
Khách hàng đăng nhập
    |
Nhập điểm đón
    |
Nhập điểm đến
    |
Chọn loại xe
    |
Gửi yêu cầu đặt chuyến
    |
Hệ thống tiếp nhận yêu cầu
    |
Hệ thống tìm tài xế phù hợp
    |
[Tìm được tài xế?]
   / \
 Có   Không
 |       |
Gửi yêu cầu   Không còn tài xế
cho tài xế    phù hợp
 |                 |
[Tài xế nhận?]  Thông báo khách hàng
 / \               |
Có Không         Kết thúc
|    |
|    +--> Tìm tài xế phù hợp tiếp theo
|
Phân công tài xế
|
Thông báo cho khách hàng
|
Tài xế di chuyển đến điểm đón
|
Tài xế đến điểm đón
|
Đón khách
|
Thực hiện chuyến
|
Hoàn thành chuyến
|
Tính cước
|
Thanh toán
|
Thông báo kết quả
|
Khách hàng đánh giá
|
[Kết thúc]
```

------------------------------------------------------------------------

## B7. Phân rã Business Requirement thành Functional Requirements

### BR04 -- Tìm tài xế

  ID     Functional Requirement
  ------ --------------------------------------------------------
  FR01   Hệ thống xác định vị trí điểm đón của khách hàng
  FR02   Hệ thống xác định khu vực tìm kiếm tài xế
  FR03   Hệ thống lấy danh sách tài xế đang online/sẵn sàng
  FR04   Hệ thống lọc tài xế theo loại phương tiện phù hợp
  FR05   Hệ thống xác định khoảng cách tài xế tới điểm đón
  FR06   Hệ thống áp dụng tiêu chí ưu tiên tài xế được cấu hình
  FR07   Hệ thống sắp xếp danh sách tài xế phù hợp
  FR08   Hệ thống gửi yêu cầu chuyến tới tài xế
  FR09   Hệ thống ghi nhận chấp nhận/từ chối
  FR10   Hệ thống xử lý tài xế không phản hồi
  FR11   Hệ thống chuyển sang tài xế phù hợp tiếp theo
  FR12   Hệ thống thông báo khi không còn tài xế phù hợp

### BR10 -- Thanh toán

  ID     Functional Requirement
  ------ -----------------------------------------------
  FR13   Cho phép chọn thanh toán tiền mặt
  FR14   Cho phép chọn thanh toán điện tử
  FR15   Gửi yêu cầu thanh toán tới Payment Provider
  FR16   Nhận kết quả thanh toán
  FR17   Cập nhật trạng thái giao dịch
  FR18   Thông báo thanh toán thành công
  FR19   Thông báo thanh toán thất bại
  FR20   Cho phép xử lý lại thanh toán theo chính sách

------------------------------------------------------------------------

## B8. Business Rules và Exception

### Business Rules

  -----------------------------------------------------------------------
  ID                                  Business Rule
  ----------------------------------- -----------------------------------
  BRU01                               Chỉ tài xế ở trạng thái sẵn sàng
                                      mới được xét nhận chuyến

  BRU02                               Phương tiện của tài xế phải phù hợp
                                      loại xe khách chọn

  BRU03                               Một chuyến chỉ được phân công cho
                                      một tài xế tại một thời điểm

  BRU04                               Tài xế phải chấp nhận chuyến trước
                                      khi được phân công chính thức

  BRU05                               Khi tài xế từ chối, hệ thống tiếp
                                      tục tìm tài xế khác

  BRU06                               Khi tài xế không phản hồi trong
                                      thời gian quy định, hệ thống chuyển
                                      sang tài xế khác

  BRU07                               Chỉ chuyến hoàn thành mới được tính
                                      cước cuối cùng

  BRU08                               Khách hàng chỉ được đánh giá sau
                                      chuyến hoàn thành

  BRU09                               Thanh toán điện tử phải thông qua
                                      Payment Provider

  BRU10                               CAB không lưu trực tiếp dữ liệu thẻ
                                      nhạy cảm

  BRU11                               Chỉ người có quyền phù hợp mới được
                                      thực hiện thao tác quản trị nhạy
                                      cảm

  BRU12                               Các thao tác quan trọng phải được
                                      ghi Audit Log
  -----------------------------------------------------------------------

> **Lưu ý:** Mốc 30 giây cho tài xế phản hồi chỉ là đề xuất. Đề bài chưa
> chốt thời gian cụ thể, vì vậy trạng thái hiện tại là **TBD -- chờ
> khách hàng xác nhận**.

### Exception

  -----------------------------------------------------------------------
  ID                      Exception               Xử lý
  ----------------------- ----------------------- -----------------------
  EX01                    Không có tài xế phù hợp Thông báo khách hàng

  EX02                    Tài xế từ chối          Tìm tài xế tiếp theo

  EX03                    Tài xế timeout          Tìm tài xế tiếp theo

  EX04                    Payment Provider lỗi    Thông báo thất bại và
                                                  áp dụng retry policy

  EX05                    Notification Provider   Không được làm dừng quy
                          lỗi                     trình chuyến

  EX06                    Mất kết nối             Xử lý theo chính sách
                                                  đồng bộ/retry sau khi
                                                  được xác nhận

  EX07                    Dữ liệu vị trí không    Xử lý theo chính sách
                          khả dụng                matching được xác nhận
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## B9. Data Modeling

### Các thực thể chính

``` text
USER
- user_id PK
- name
- phone
- email
- password_hash
- status

CUSTOMER
- customer_id PK
- user_id FK

DRIVER
- driver_id PK
- user_id FK
- status
- rating

VEHICLE
- vehicle_id PK
- driver_id FK
- vehicle_type_id FK
- license_plate
- status

VEHICLE_TYPE
- vehicle_type_id PK
- name

DRIVER_LOCATION
- location_id PK
- driver_id FK
- latitude
- longitude
- recorded_at

TRIP
- trip_id PK
- customer_id FK
- driver_id FK
- vehicle_id FK
- pickup_location
- destination
- status
- created_at
- completed_at

TRIP_STATUS_HISTORY
- history_id PK
- trip_id FK
- status
- changed_at

FARE
- fare_id PK
- trip_id FK
- amount

PAYMENT
- payment_id PK
- trip_id FK
- method
- amount
- status
- provider_reference

RATING
- rating_id PK
- trip_id FK
- customer_id FK
- driver_id FK
- score
- comment

NOTIFICATION
- notification_id PK
- user_id FK
- channel
- type
- status

ROLE
- role_id PK
- name

USER_ROLE
- user_id FK
- role_id FK

AUDIT_LOG
- audit_id PK
- user_id FK
- action
- created_at
```

### Quan hệ ERD chính

``` text
USER 1 ---- 0..1 CUSTOMER
USER 1 ---- 0..1 DRIVER
DRIVER 1 -------- N VEHICLE
DRIVER 1 -------- N DRIVER_LOCATION
CUSTOMER 1 ------ N TRIP
DRIVER 1 -------- N TRIP
VEHICLE 1 ------- N TRIP
TRIP 1 ---------- N TRIP_STATUS_HISTORY
TRIP 1 ---------- 1 FARE
TRIP 1 ---------- N PAYMENT
TRIP 1 ---------- 0..1 RATING
USER 1 ---------- N NOTIFICATION
USER N ---------- N ROLE
USER 1 ---------- N AUDIT_LOG
```

------------------------------------------------------------------------

## B10. Non-Functional Requirements

  -----------------------------------------------------------------------
  ID                      Nhóm                    NFR
  ----------------------- ----------------------- -----------------------
  NFR01                   Performance             Matching tài xế phải có
                                                  thời gian phản hồi phù
                                                  hợp với SLA được xác
                                                  nhận

  NFR02                   Scalability             Booking, Matching,
                                                  Payment, Notification
                                                  có khả năng mở rộng độc
                                                  lập

  NFR03                   Availability            Lỗi
                                                  Payment/Notification
                                                  không được làm dừng
                                                  toàn bộ Booking

  NFR04                   Security                Người dùng phải xác
                                                  thực trước chức năng
                                                  yêu cầu tài khoản

  NFR05                   Authorization           Chức năng quản trị phải
                                                  kiểm soát theo quyền

  NFR06                   Privacy                 Bảo vệ PII, dữ liệu xe,
                                                  vị trí và giao dịch

  NFR07                   Payment Security        Không lưu trực tiếp
                                                  thông tin thẻ nhạy cảm

  NFR08                   Auditability            Hoạt động quan trọng
                                                  phải có audit log

  NFR09                   Maintainability         Cho phép thay thế/mở
                                                  rộng thành phần hạn chế
                                                  ảnh hưởng hệ thống

  NFR10                   Extensibility           Cho phép thêm loại dịch
                                                  vụ, payment provider,
                                                  notification channel

  NFR11                   Reliability             Có cơ chế xử lý lỗi
                                                  thành phần tích hợp

  NFR12                   Deployability           Có khả năng triển khai
                                                  từng phần hạn chế
                                                  downtime
  -----------------------------------------------------------------------

> Không tự đặt các giá trị như 99.9% uptime, `<2 giây` hay
> `1.000 request/giây` khi stakeholder chưa xác nhận.

------------------------------------------------------------------------

## B11. Use Case

  ID     Use Case                       Actor chính
  ------ ------------------------------ ------------------
  UC01   Đăng ký tài khoản khách hàng   Khách hàng
  UC02   Đăng nhập                      Người dùng
  UC03   Cập nhật thông tin cá nhân     Khách hàng
  UC04   Đặt chuyến                     Khách hàng
  UC05   Theo dõi chuyến                Khách hàng
  UC06   Xem lịch sử chuyến             Khách hàng
  UC07   Thanh toán chuyến              Khách hàng
  UC08   Đánh giá tài xế                Khách hàng
  UC09   Quản lý hồ sơ tài xế           Tài xế
  UC10   Quản lý phương tiện            Tài xế/Nhân viên
  UC11   Cập nhật trạng thái sẵn sàng   Tài xế
  UC12   Nhận/Từ chối chuyến            Tài xế
  UC13   Cập nhật trạng thái chuyến     Tài xế
  UC14   Cập nhật vị trí                Tài xế
  UC15   Tìm tài xế                     Hệ thống
  UC16   Phân công tài xế               Hệ thống
  UC17   Tính cước                      Hệ thống
  UC18   Gửi thông báo                  Hệ thống
  UC19   Quản lý khách hàng             Nhân viên
  UC20   Quản lý tài xế                 Nhân viên
  UC21   Quản lý chuyến đi              Nhân viên
  UC22   Theo dõi chuyến đang diễn ra   Nhân viên
  UC23   Tra cứu giao dịch              Nhân viên
  UC24   Xem báo cáo                    Quản lý
  UC25   Quản lý phân quyền             Quản trị viên

------------------------------------------------------------------------

## B12. Đặc tả Use Case mẫu -- UC04 Đặt chuyến

  Thuộc tính       Nội dung
  ---------------- ------------------------------------------------
  Use Case ID      UC04
  Tên              Đặt chuyến
  Actor            Khách hàng
  Mục tiêu         Tạo yêu cầu đặt xe
  Tiền điều kiện   Khách hàng đã được xác thực
  Trigger          Khách hàng chọn chức năng đặt xe
  Hậu điều kiện    Chuyến được tạo và hệ thống bắt đầu tìm tài xế

### Basic Flow

  Actor                 System
  --------------------- ---------------------------------------------
  1\. Chọn đặt chuyến   
  2\. Nhập điểm đón     
  3\. Nhập điểm đến     
  4\. Chọn loại xe      
  5\. Gửi yêu cầu       
                        6\. Kiểm tra thông tin
                        7\. Tạo chuyến
                        8\. Chuyển yêu cầu tới quá trình tìm tài xế
                        9\. Thông báo yêu cầu đã được tiếp nhận

### Alternative Flow

**AF01 -- Tài xế được đề xuất từ chối**

Hệ thống loại tài xế đó khỏi lượt phân công hiện tại và tiếp tục tìm tài
xế phù hợp khác mà khách hàng không cần tạo lại chuyến.

**AF02 -- Tài xế không phản hồi**

Khi vượt quá thời gian phản hồi đã cấu hình, hệ thống tiếp tục với tài
xế phù hợp tiếp theo.

### Exception Flow

**EX01 -- Không tìm được tài xế**

Hệ thống cập nhật kết quả tìm kiếm và thông báo rõ ràng cho khách hàng.

------------------------------------------------------------------------

## B13. Acceptance Criteria

  -----------------------------------------------------------------------
  ID                                  Acceptance Criteria
  ----------------------------------- -----------------------------------
  AC01                                Khách hàng đã xác thực có thể tạo
                                      chuyến với điểm đón, điểm đến và
                                      loại xe

  AC02                                Sau khi tạo chuyến thành công, hệ
                                      thống bắt đầu quá trình tìm tài xế

  AC03                                Chỉ tài xế đủ điều kiện và đang sẵn
                                      sàng được đưa vào danh sách
                                      matching

  AC04                                Khi tài xế từ chối, hệ thống tự
                                      động xét tài xế tiếp theo

  AC05                                Khi tài xế không phản hồi quá thời
                                      gian cấu hình, hệ thống xét tài xế
                                      tiếp theo

  AC06                                Khách hàng không phải tạo lại
                                      chuyến khi một tài xế từ chối

  AC07                                Khi tài xế nhận chuyến, khách hàng
                                      nhận được thông tin tài xế

  AC08                                Khách hàng có thể theo dõi trạng
                                      thái chuyến

  AC09                                Khi chuyến hoàn thành, hệ thống xác
                                      định cước

  AC10                                Hệ thống hỗ trợ tiền mặt

  AC11                                Hệ thống hỗ trợ thanh toán điện tử
                                      qua provider

  AC12                                Thanh toán thất bại được thông báo
                                      cho khách hàng

  AC13                                Payment failure không làm mất dữ
                                      liệu chuyến

  AC14                                Khách hàng có thể đánh giá tài xế
                                      sau chuyến hoàn thành

  AC15                                Người không có quyền không được
                                      thực hiện chức năng quản trị nhạy
                                      cảm
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## B14. Requirement Traceability Matrix -- RTM

Chuỗi truy xuất:

``` text
BG → BR → FR → UC → AC → TC
```

  BG     BR     FR     UC     AC     TC
  ------ ------ ------ ------ ------ ------
  BG01   BR02   FR01   UC04   AC01   TC01
  BG01   BR04   FR02   UC15   AC02   TC02
  BG01   BR04   FR03   UC15   AC03   TC03
  BG01   BR04   FR04   UC15   AC03   TC04
  BG01   BR04   FR05   UC15   AC03   TC05
  BG02   BR05   FR08   UC16   AC07   TC06
  BG02   BR05   FR09   UC16   AC04   TC07
  BG02   BR05   FR10   UC16   AC05   TC08
  BG02   BR05   FR11   UC16   AC06   TC09
  BG05   BR10   FR13   UC07   AC10   TC10
  BG05   BR10   FR14   UC07   AC11   TC11
  BG05   BR10   FR15   UC07   AC11   TC12
  BG05   BR10   FR16   UC07   AC12   TC13
  BG05   BR10   FR19   UC07   AC12   TC14

### Ví dụ truy xuất

``` text
BG01 – Giảm thời gian tìm tài xế
        ↓
BR04 – Tự động tìm tài xế
        ↓
FR03 – Lấy tài xế đang sẵn sàng
        ↓
FR05 – Xác định khoảng cách tới khách hàng
        ↓
UC15 – Tìm tài xế
        ↓
AC03 – Chỉ tài xế đủ điều kiện được matching
        ↓
TC03 – Kiểm tra tài xế Offline không được matching
```

------------------------------------------------------------------------

## Các vấn đề cần xác nhận với Stakeholder

  ID    Vấn đề cần làm rõ                       Trạng thái
  ----- --------------------------------------- ------------
  Q01   Công thức tính cước cụ thể?             TBD
  Q02   Bán kính tìm tài xế?                    TBD
  Q03   Tiêu chí xếp hạng tài xế?               TBD
  Q04   Tài xế có bao nhiêu giây để phản hồi?   TBD
  Q05   Tối đa thử bao nhiêu tài xế?            TBD
  Q06   Chính sách khách hàng hủy chuyến?       TBD
  Q07   Tài xế hủy chuyến xử lý thế nào?        TBD
  Q08   Mất mạng trong chuyến xử lý thế nào?    TBD
  Q09   Dữ liệu vị trí lưu trong bao lâu?       TBD
  Q10   Lịch sử giao dịch lưu bao lâu?          TBD
  Q11   Payment retry tối đa bao nhiêu lần?     TBD
  Q12   SLA/response time mục tiêu?             TBD
  Q13   Peak concurrent users/trips?            TBD
  Q14   Những role quản trị cụ thể?             TBD

------------------------------------------------------------------------

## Tổng thể quy trình BA

``` text
B1  Business Context / Problem / Vision
 ↓
B2  Stakeholder Analysis
 ↓
B3  Business Goals (BG)
 ↓
B4  Scope – In Scope / Out of Scope
 ↓
B5  Business Requirements (BR)
 ↓
B6  Business Process
 ↓
B7  Functional Requirements (FR)
 ↓
B8  Business Rules + Exceptions
 ↓
B9  Data Model / ERD
 ↓
B10 Non-Functional Requirements
 ↓
B11 Use Case Model
 ↓
B12 Use Case Specification
 ↓
B13 Acceptance Criteria (AC)
 ↓
B14 RTM
     BG → BR → FR → UC → AC → TC
```

------------------------------------------------------------------------

**Ghi chú:** Những thông tin mà khách hàng chưa chốt phải được đánh dấu
**TBD** và xác nhận với stakeholder trước khi trở thành yêu cầu chính
thức.

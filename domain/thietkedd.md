# THIẾT KẾ MICRO-SERVICE CHO CAB SYSTEM


## 1. Phân tách Use Case theo miền nghiệp vụ

CAB System được chia thành 10 Bounded Context chính. Việc gán mã Use
Case dưới đây dùng bộ mã UC đề xuất cho tài liệu kiến trúc này; khi
repository có danh sách UC chính thức, cần ánh xạ lại mã nhưng giữ
nguyên boundary nghiệp vụ.

  ---------------------------------------------------------------------------
  Bounded Context   Use Case liên     Năng lực nghiệp   Khái niệm chính
                    quan              vụ                
  ----------------- ----------------- ----------------- ---------------------
  Identity & Access UC-01 Đăng ký;    Xác thực, phiên   Account, Credential,
                    UC-02 Đăng nhập;  đăng nhập, vai    OTP, Session, Role,
                    UC-03 Quên mật    trò và quyền.     Permission
                    khẩu; UC-04 Đăng                    
                    xuất; UC-05 Phân                    
                    quyền                               

  Customer          UC-06 Xem hồ sơ;  Quản lý hồ sơ và  CustomerProfile,
                    UC-07 Cập nhật hồ thông tin nghiệp  ContactInfo
                    sơ; UC-08 Xem     vụ khách hàng.    
                    lịch sử chuyến                      

  Booking           UC-09 Tạo yêu cầu Tiếp nhận và quản Booking,
                    đặt xe; UC-10     lý yêu cầu đặt xe PickupLocation,
                    Chọn loại xe;     trước khi phân    DropoffLocation,
                    UC-11 Hủy yêu     công tài xế.      VehicleType
                    cầu; UC-12 Theo                     
                    dõi yêu cầu                         

  Driver & Vehicle  UC-13 Quản lý hồ  Quản lý tài xế,   Driver, Vehicle,
                    sơ tài xế; UC-14  xe, trạng thái và DriverStatus,
                    Quản lý phương    vị trí.           DriverLocation
                    tiện; UC-15                         
                    Bật/tắt sẵn sàng;                   
                    UC-16 Cập nhật vị                   
                    trí                                 

  Driver Matching   UC-17 Tìm tài xế; Lọc, ưu tiên, đề  MatchingRequest,
                    UC-18 Gửi đề nghị xuất và phân công DriverCandidate,
                    chuyến; UC-19     tài xế.           MatchingAttempt
                    Chấp nhận/từ                        
                    chối; UC-20                         
                    Chuyển tài xế                       
                    khác                                

  Trip              UC-21 Tài xế đến  Quản lý vòng đời  Trip, TripStatus,
                    điểm đón; UC-22   chuyến đi.        TripStatusHistory
                    Đón khách; UC-23                    
                    Bắt đầu chuyến;                     
                    UC-24 Hoàn thành;                   
                    UC-25 Theo dõi                      
                    trạng thái                          

  Fare & Pricing    UC-26 Ước tính    Tính giá theo     Fare, FareRule,
                    cước; UC-27 Tính  loại dịch vụ và   PricingSnapshot
                    cước cuối         dữ liệu chuyến.   

  Payment           UC-28 Thanh toán  Quản lý giao dịch Payment, Transaction,
                    tiền mặt; UC-29   và tích hợp nhà   PaymentProvider
                    Thanh toán điện   cung cấp thanh    
                    tử; UC-30 Xử lý   toán.             
                    thanh toán thất                     
                    bại                                 

  Notification      UC-31 Thông báo   Phát thông báo    Notification,
                    khách hàng; UC-32 theo sự kiện, hỗ  Template, Channel,
                    Thông báo tài xế  trợ mở rộng kênh. Delivery

  Rating & Feedback UC-33 Đánh giá    Thu thập phản hồi Rating, Feedback,
                    tài xế; UC-34 Xem sau chuyến và cập DriverRatingSummary
                    tổng hợp đánh giá nhật điểm tài xế. 
  ---------------------------------------------------------------------------

Supporting capabilities:

-   Administration: quản lý khách hàng, tài xế, phương tiện, chuyến đi
    và thao tác nhạy cảm theo quyền.
-   Reporting: số chuyến, doanh thu, tỷ lệ hoàn thành/hủy, hiệu quả tài
    xế.
-   Audit & Logging: lưu vết đăng nhập, thay đổi dữ liệu và thao tác
    quản trị quan trọng. \## 2. Ubiquitous Language

  -----------------------------------------------------------------------
  Thuật ngữ               Ý nghĩa                 Context
  ----------------------- ----------------------- -----------------------
  Account                 Danh tính dùng để xác   Identity & Access
                          thực vào CAB System.    

  Customer                Người sử dụng dịch vụ   Customer
                          để yêu cầu chuyến xe.   

  Driver                  Người lái xe có thể     Driver & Vehicle
                          nhận và thực hiện       
                          chuyến.                 

  Vehicle                 Phương tiện gắn với tài Driver & Vehicle
                          xế và loại dịch vụ.     

  Booking                 Yêu cầu đặt xe của      Booking
                          khách hàng trước khi hệ 
                          thống phân công tài xế. 

  Pickup Location         Điểm tài xế đón khách.  Booking

  Drop-off Location       Điểm khách hàng muốn    Booking
                          đến.                    

  Available Driver        Tài xế đang online, sẵn Driver & Vehicle /
                          sàng và đủ điều kiện    Matching
                          nhận chuyến.            

  Matching Request        Yêu cầu tìm tài xế cho  Driver Matching
                          một Booking.            

  Driver Candidate        Tài xế đang được xét/đề Driver Matching
                          xuất cho một Matching   
                          Request.                

  Assignment              Kết quả phân công một   Driver Matching
                          tài xế cho              
                          Booking/Trip.           

  Trip                    Chuyến đi được hình     Trip
                          thành sau khi tài xế    
                          được phân công.         

  Fare                    Số tiền được tính cho   Fare & Pricing
                          chuyến đi.              

  Payment                 Nghiệp vụ thanh toán    Payment
                          cước chuyến.            

  Payment Provider        Nhà cung cấp bên ngoài  Payment
                          xử lý thanh toán điện   
                          tử.                     

  Notification            Thông báo gửi đến khách Notification
                          hàng hoặc tài xế theo   
                          sự kiện.                

  Rating                  Điểm và nhận xét của    Rating & Feedback
                          khách hàng sau chuyến   
                          hoàn thành.             
  -----------------------------------------------------------------------

## 3. Bounded Context và Context Map

Context Map đề xuất cho CAB System:

``` text
Identity & Access
   ├── user.registered ──> Customer
   └── identity/role ────> Driver & Administration

Customer ── customer reference ──> Booking
Booking ── booking.created ───────> Driver Matching
Driver & Vehicle <── driver availability/location ──> Driver Matching
Driver Matching ── driver.assigned ────────────────> Trip
Trip ── trip.completed ────────────────────────────> Fare & Pricing
Fare & Pricing ── fare.calculated ─────────────────> Payment
Booking/Trip/Payment ── domain events ─────────────> Notification
Trip ── completed trip reference ──────────────────> Rating & Feedback
Trip/Payment/Rating ── events/read model ──────────> Reporting
All critical actions ──────────────────────────────> Audit & Logging
```

### Nguyên tắc giao tiếp

-   REST/API Gateway cho truy vấn hoặc lệnh cần phản hồi đồng bộ.
-   Domain Event/Event Broker cho các tác vụ bất đồng bộ như
    notification, reporting và audit.
-   Không cho service A truy cập trực tiếp database của service B.
-   Dùng ID/reference và contract ổn định giữa các context; dữ liệu chi
    tiết vẫn thuộc service sở hữu.
-   Notification hoặc Payment lỗi không được làm toàn bộ luồng
    Booking/Trip dừng theo kiểu lỗi dây chuyền. \## 4. Aggregate và
    invariant nghiệp vụ

  --------------------------------------------------------------------------------------
  Aggregate      Aggregate Root    Thành phần chính      Invariant        Use Case
  -------------- ----------------- --------------------- ---------------- --------------
  Identity       Account           Credential,           Email/phone định UC-01..05
  Aggregate                        RoleAssignment,       danh không       
                                   Session               trùng;           
                                                         credential hợp   
                                                         lệ mới cấp       
                                                         session/token.   

  Customer       Customer          CustomerProfile       Customer phải    UC-06..08
  Aggregate                                              tham chiếu một   
                                                         user hợp lệ; cập 
                                                         nhật hồ sơ không 
                                                         làm thay đổi     
                                                         credential.      

  Booking        Booking           PickupLocation,       Chỉ tạo/xác nhận UC-09..12
  Aggregate                        DropoffLocation,      booking khi điểm 
                                   VehicleType,          đón, điểm đến và 
                                   PaymentMethod         loại xe hợp lệ.  

  Driver         Driver            Vehicle,              Chỉ tài xế đủ    UC-13..16
  Aggregate                        DriverStatus,         điều kiện và     
                                   DriverLocation        AVAILABLE mới    
                                                         tham gia         
                                                         matching; xe     
                                                         phải ở trạng     
                                                         thái cho phép    
                                                         hoạt động.       

  Matching       MatchingRequest   DriverCandidate,      Một candidate    UC-17..20
  Aggregate                        MatchingAttempt       không được đồng  
                                                         thời được coi là 
                                                         accepted và      
                                                         rejected;        
                                                         timeout/reject   
                                                         phải cho phép    
                                                         xét candidate    
                                                         tiếp theo.       

  Trip Aggregate Trip              TripStatusHistory,    Trip phải có     UC-21..25
                                   AssignedDriver        booking và tài   
                                                         xế đã được phân  
                                                         công; chuyển     
                                                         trạng thái phải  
                                                         đúng thứ tự      
                                                         nghiệp vụ.       

  Fare Aggregate Fare              FareRule,             Cước cuối phải   UC-26..27
                                   PricingSnapshot       gắn với trip;    
                                                         rule áp dụng     
                                                         phải còn hiệu    
                                                         lực; công thức   
                                                         chi tiết là cấu  
                                                         hình nghiệp vụ.  

  Payment        Payment           PaymentTransaction,   Không đánh dấu   UC-28..30
  Aggregate                        ProviderReference     PAID nếu chưa có 
                                                         kết quả hợp lệ;  
                                                         không lưu dữ     
                                                         liệu thẻ/tài     
                                                         khoản nhạy cảm.  

  Notification   Notification      DeliveryAttempt,      Lỗi gửi một kênh UC-31..32
  Aggregate                        Channel               không được       
                                                         rollback nghiệp  
                                                         vụ nguồn; trạng  
                                                         thái gửi phải    
                                                         được theo dõi.   

  Rating         Rating            Feedback              Chỉ đánh giá     UC-33..34
  Aggregate                                              trip COMPLETED;  
                                                         điểm trong miền  
                                                         cho phép (đề     
                                                         xuất 1--5).      
  --------------------------------------------------------------------------------------

### Các ngoại lệ cần xử lý

-   Tài xế từ chối hoặc không phản hồi: Matching tiếp tục candidate
    khác, khách hàng không tạo lại Booking.
-   Không còn tài xế phù hợp: kết thúc matching theo trạng thái không
    tìm được và thông báo khách hàng.
-   Thanh toán điện tử thất bại: Payment ghi nhận FAILED/PENDING theo
    chính sách và cho phép xử lý lại.
-   Notification thất bại: ghi nhận delivery failure/retry mà không đảo
    ngược trạng thái chuyến.
-   Mất kết nối: chính sách retry, idempotency và reconciliation cần
    được stakeholder chốt. \## 5. Domain Event phát sinh từ Use Case

  ---------------------------------------------------------------------------------------------------
  Domain Event                  Use Case nguồn Producer       Consumer Context      Mục đích
                                               Context                              
  ----------------------------- -------------- -------------- --------------------- -----------------
  user.registered               UC-01          Identity &     Customer/Driver       Khởi tạo hồ sơ
                                               Access                               nghiệp vụ sau
                                                                                    đăng ký.

  booking.created               UC-09          Booking        Matching,             Bắt đầu tìm tài
                                                              Notification          xế và xác nhận đã
                                                                                    tiếp nhận yêu
                                                                                    cầu.

  booking.cancelled             UC-11          Booking        Matching,             Dừng
                                                              Notification          matching/chuyến
                                                                                    chưa bắt đầu và
                                                                                    thông báo.

  driver.availability.changed   UC-15          Driver &       Matching              Cập nhật tập tài
                                               Vehicle                              xế có thể được
                                                                                    xét.

  driver.location.updated       UC-16          Driver &       Matching/Trip         Hỗ trợ tìm tài xế
                                               Vehicle                              gần và theo dõi
                                                                                    ETA.

  driver.candidate.selected     UC-18          Driver         Driver/Notification   Gửi đề nghị
                                               Matching                             chuyến đến tài
                                                                                    xế.

  driver.rejected               UC-19          Driver &       Matching              Matching chuyển
                                               Vehicle                              sang tài xế tiếp
                                                                                    theo.

  driver.response.timed_out     UC-20          Driver         Matching              Đánh dấu lần thử
                                               Matching                             timeout và tiếp
                                                                                    tục tìm.

  driver.assigned               UC-19          Driver         Booking, Trip,        Xác nhận tài xế
                                               Matching       Notification          nhận chuyến và
                                                                                    tạo/khởi động
                                                                                    Trip.

  driver.arrived                UC-21          Trip           Notification          Thông báo tài xế
                                                                                    đã đến điểm đón.

  trip.started                  UC-23          Trip           Notification          Thông báo chuyến
                                                                                    bắt đầu.

  trip.completed                UC-24          Trip           Fare, Notification,   Kích hoạt tính
                                                              Reporting, Rating     cước và các
                                                                                    nghiệp vụ sau
                                                                                    chuyến.

  fare.calculated               UC-27          Fare & Pricing Payment               Cung cấp số tiền
                                                                                    phải thanh toán.

  payment.succeeded             UC-29          Payment        Notification,         Thông báo thanh
                                                              Reporting             toán thành công
                                                                                    và cập nhật read
                                                                                    model.

  payment.failed                UC-30          Payment        Notification          Thông báo thất
                                                                                    bại và hỗ trợ
                                                                                    retry theo
                                                                                    policy.

  rating.created                UC-33          Rating &       Driver, Reporting     Cập nhật dữ liệu
                                               Feedback                             đánh giá/hiệu quả
                                                                                    tài xế.
  ---------------------------------------------------------------------------------------------------

## 6. Ánh xạ Context sang Microservice

  ------------------------------------------------------------------------------
  Bounded Context   Service triển khai     Dữ liệu sở hữu      Giao tiếp chính
  ----------------- ---------------------- ------------------- -----------------
  Identity & Access auth-service           auth_db             REST Gateway +
                                                               Event

  Customer          customer-service       customer_db         REST Gateway +
                                                               Event

  Booking           booking-service        booking_db          REST Gateway +
                                                               Event

  Driver & Vehicle  driver-service         driver_db           REST + Event;
                                                               location update

  Driver Matching   matching-service       matching_db /       Event + internal
                                           matching store      REST/read model

  Trip              trip-service           trip_db             REST + Event

  Fare & Pricing    fare-service           fare_db             REST + Event

  Payment           payment-service        payment_db          REST + Payment
                                                               Provider + Event

  Notification      notification-service   notification_db     Event consumer +
                                                               external channels

  Rating & Feedback rating-service         rating_db           REST + Event

  Reporting         reporting-service      reporting_db/read   Event consumer
  (supporting)                             model               

  Audit             audit-service          audit_db            Event/log
  (supporting)                                                 consumer
  ------------------------------------------------------------------------------

Khuyến nghị hạ tầng:

-   API Gateway: điểm vào chung cho Web/Mobile/Admin.
-   Event Broker: Kafka/RabbitMQ hoặc công nghệ tương đương để truyền
    domain event.
-   Service discovery/configuration: quản lý endpoint và cấu hình theo
    môi trường.
-   Centralized observability: log, metric, tracing, correlation ID.
-   Database per service; không dùng shared schema làm nguồn ghi chung.
    \## 7. Mô tả Service

  ----------------------------------------------------------------------------------
  Bounded Context   Service triển khai     Trách nhiệm chính       Dữ liệu sở hữu
  ----------------- ---------------------- ----------------------- -----------------
  Identity & Access auth-service           Đăng ký, đăng nhập,     auth_db
                                           OTP, JWT/access token,  
                                           refresh token, quên mật 
                                           khẩu, role/permission.  

  Customer          customer-service       Quản lý hồ sơ khách     customer_db
                                           hàng và dữ liệu cá nhân 
                                           nghiệp vụ.              

  Booking           booking-service        Tạo/hủy booking, lưu    booking_db
                                           điểm đón/đến, loại xe,  
                                           phương thức thanh toán  
                                           và trạng thái yêu cầu.  

  Driver & Vehicle  driver-service         Hồ sơ tài xế, phương    driver_db
                                           tiện, trạng thái        
                                           online/available/busy   
                                           và vị trí.              

  Driver Matching   matching-service       Lọc tài xế phù hợp, xếp matching_db
                                           ưu tiên, gửi đề nghị,   
                                           timeout/reject và phân  
                                           công.                   

  Trip              trip-service           Quản lý trạng thái từ   trip_db
                                           assigned đến            
                                           completed/cancelled và  
                                           lịch sử chuyến.         

  Fare & Pricing    fare-service           Ước tính/tính cước theo fare_db
                                           rule có thể cấu hình.   

  Payment           payment-service        Tiền mặt/điện tử, tích  payment_db
                                           hợp provider,           
                                           transaction status,     
                                           retry/reconciliation.   

  Notification      notification-service   Nhận event, dựng nội    notification_db
                                           dung, gửi qua kênh,     
                                           theo dõi                
                                           delivery/retry.         

  Rating & Feedback rating-service         Nhận đánh giá sau       rating_db
                                           chuyến và tổng hợp dữ   
                                           liệu đánh giá.          

  Reporting         reporting-service      Xây read model và báo   reporting_db
                                           cáo số chuyến, doanh    
                                           thu, tỷ lệ hoàn         
                                           thành/hủy, hiệu quả tài 
                                           xế.                     

  Audit             audit-service          Lưu vết thao tác quan   audit_db
                                           trọng phục vụ kiểm tra  
                                           sự cố.                  
  ----------------------------------------------------------------------------------

### Yêu cầu độc lập và khả năng chịu lỗi

-   Mỗi service có thể scale độc lập theo tải; Matching/Driver Location
    có thể cần scale cao hơn Reporting.
-   Timeout, retry có backoff và circuit breaker khi gọi external
    provider.
-   Consumer event phải idempotent để tránh xử lý trùng.
-   Dùng outbox/inbox pattern nếu cần bảo đảm nhất quán giữa database
    transaction và event.
-   Không dùng distributed transaction xuyên tất cả service; ưu tiên
    eventual consistency/Saga cho luồng dài. \## 8. Mô hình dữ liệu cho
    Service

Mô hình dưới đây là logical data model theo ownership. FK ghi trong tài
liệu là quan hệ logic; khi hai thực thể thuộc hai database/service khác
nhau, chỉ lưu ID tham chiếu và không tạo foreign key vật lý xuyên
database.

### 8.1 Auth Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  users                               user_id PK; phone/email UNIQUE;
                                      password_hash; status; created_at;
                                      updated_at

  roles                               role_id PK; role_name; description

  user_roles                          user_id; role_id; assigned_at

  refresh_tokens                      token_id PK; user_id; token_hash;
                                      expires_at; revoked_at; created_at

  audit_login                         id PK; user_id; action; ip_address;
                                      success; created_at
  -----------------------------------------------------------------------

### 8.2 Customer Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  customers                           customer_id PK; user_id REF;
                                      full_name; date_of_birth; gender;
                                      address; avatar_url; loyalty_point;
                                      status

  -----------------------------------------------------------------------

### 8.3 Booking Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  bookings                            booking_id PK; customer_id REF;
                                      pickup_location_id;
                                      dropoff_location_id;
                                      vehicle_type_id REF;
                                      payment_method; status; note;
                                      timestamps

  locations                           location_id PK; address; latitude;
                                      longitude; ward; district; city

  booking_status_history              id PK; booking_id; status; reason;
                                      changed_at
  -----------------------------------------------------------------------

### 8.4 Driver Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  drivers                             driver_id PK; user_id REF;
                                      full_name; license_number;
                                      rating_avg; status; is_online;
                                      timestamps

  vehicles                            vehicle_id PK; driver_id;
                                      vehicle_type_id; license_plate;
                                      brand; model; color; year; status

  vehicle_types                       vehicle_type_id PK; name;
                                      description; status

  driver_locations                    id PK; driver_id; latitude;
                                      longitude; recorded_at

  driver_status_history               id PK; driver_id; status;
                                      changed_at
  -----------------------------------------------------------------------

### 8.5 Matching Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  matching_requests                   request_id PK; booking_id REF;
                                      vehicle_type_id REF; search_radius;
                                      status; created_at

  driver_candidates                   candidate_id PK; request_id;
                                      driver_id REF; score; status;
                                      responded_at

  matching_attempts                   attempt_id PK; request_id;
                                      driver_id REF; sent_at; expired_at;
                                      result
  -----------------------------------------------------------------------

### 8.6 Trip Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  trips                               trip_id PK; booking_id REF;
                                      driver_id REF; vehicle_id REF;
                                      start_time; end_time; distance_km;
                                      status; actual_fare

  trip_status_history                 history_id PK; trip_id; status;
                                      latitude; longitude; changed_at;
                                      note
  -----------------------------------------------------------------------

### 8.7 Fare Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  fare_rules                          rule_id PK; vehicle_type_id REF;
                                      name; base_price; price_per_km;
                                      price_per_minute; effective_from;
                                      effective_to; status

  fares                               fare_id PK; trip_id REF; rule_id;
                                      distance_km; duration_minute;
                                      base_fare; additional_fee;
                                      discount_amount; total_amount;
                                      currency; calculated_at
  -----------------------------------------------------------------------

### 8.8 Payment Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  payments                            payment_id PK; trip_id REF; amount;
                                      method; status;
                                      provider_transaction_id; paid_at;
                                      timestamps

  payment_transactions                transaction_id PK; payment_id;
                                      provider_id; amount; status;
                                      request_ref; response_ref;
                                      created_at

  payment_providers                   provider_id PK; name; type;
                                      configuration_ref; status
  -----------------------------------------------------------------------

### 8.9 Notification Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  notifications                       notification_id PK; user_id REF;
                                      type; channel; title; content;
                                      status; sent_at; read_at;
                                      created_at

  delivery_attempts                   attempt_id PK; notification_id;
                                      provider; status; error_code;
                                      attempted_at

  notification_templates              template_id PK; event_type;
                                      channel; title_template;
                                      body_template; status
  -----------------------------------------------------------------------

### 8.10 Rating Service

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  ratings                             rating_id PK; trip_id REF;
                                      customer_id REF; driver_id REF;
                                      score; comment; timestamps

  driver_rating_summary               driver_id REF; rating_avg;
                                      rating_count; updated_at
  -----------------------------------------------------------------------

### 8.11 Reporting & Audit (supporting)

  -----------------------------------------------------------------------
  Bảng/Collection                     Thuộc tính chính
  ----------------------------------- -----------------------------------
  reporting_read_models               Các bảng/read model tổng hợp theo
                                      nhu cầu báo cáo, cập nhật từ event.

  audit_logs                          log_id PK; actor_user_id REF;
                                      action; resource_type; resource_id;
                                      detail; ip_address; created_at
  -----------------------------------------------------------------------

### Các chính sách còn phải xác nhận với stakeholder

-   Công thức tính cước, phụ phí và thời điểm chốt giá.
-   Bán kính tìm tài xế và tiêu chí xếp hạng/ưu tiên.
-   Thời gian tài xế phải phản hồi trước khi timeout.
-   Chính sách hủy chuyến và phí hủy.
-   Xử lý mất mạng, retry và đồng bộ trạng thái sau khi kết nối lại.
-   Thời gian lưu vị trí, giao dịch, audit log và dữ liệu cá nhân. ---
    HẾT ---

1. Business Context – Ngữ cảnh nghiệp vụ
Công ty ABC là doanh nghiệp cung cấp dịch vụ đặt xe trực tuyến.

Quy trình nghiệp vụ hiện tại có thể hiểu đơn giản:

Khách hàng
    ↓
Gửi yêu cầu đặt xe
    ↓
Hệ thống / tổng đài tiếp nhận
    ↓
Tìm tài xế
    ↓
Phân công tài xế
    ↓
Tài xế đón khách
    ↓
Thực hiện chuyến
    ↓
Hoàn thành chuyến
    ↓
Tính tiền
    ↓
Thanh toán
    ↓
Đánh giá

Nhưng trong hệ thống hiện tại, rất nhiều bước vẫn thủ công hoặc chưa được quản lý tập trung.

Đây chính là nguyên nhân khiến doanh nghiệp muốn xây dựng một nền tảng CAB mới.

2. Vấn đề cốt lõi của nghiệp vụ là gì?
Nếu phải tóm tắt toàn bộ đề bài thành một vấn đề lớn nhất, mình sẽ nói:

Hệ thống hiện tại không còn đáp ứng được quy mô và mức độ tự động hóa mà doanh nghiệp cần.

Cụ thể có 7 nhóm vấn đề chính.

Vấn đề 1 – Phân công tài xế thủ công
Đây là một trong những pain point quan trọng nhất.

Hiện tại:

Khách đặt xe
     ↓
Nhân viên / hệ thống tìm tài xế
     ↓
Phân công

Việc phân công tài xế chủ yếu thủ công.

Khi số lượng khách tăng:

100 khách
→ 100 yêu cầu
→ nhân viên phải xử lý nhiều yêu cầu

10.000 khách
→ 10.000 yêu cầu
→ quy trình thủ công bị quá tải

Do đó doanh nghiệp cần hệ thống tự động:

Booking
   ↓
Tìm tài xế phù hợp
   ↓
Ưu tiên tài xế
   ↓
Gửi request
   ↓
Driver accept / reject
   ↓
Nếu reject → tìm driver khác

Đây là một business problem, không chỉ là vấn đề UI.

3. Vấn đề 2 – Không theo dõi được trạng thái chuyến đi tốt
Khách hàng hiện nay muốn biết:

Đã có tài xế chưa?
Ai đang nhận chuyến?
Tài xế đang ở đâu?
Bao lâu nữa tài xế đến?
Chuyến đang ở trạng thái nào?
Đã đón khách chưa?
Đang đi hay đã hoàn thành?
Hệ thống cũ không đáp ứng tốt nhu cầu này.

Vì vậy cần quản lý một Trip Lifecycle rõ ràng:

REQUESTED
    ↓
SEARCHING_DRIVER
    ↓
DRIVER_ASSIGNED
    ↓
DRIVER_ARRIVING
    ↓
DRIVER_ARRIVED
    ↓
PASSENGER_PICKED_UP
    ↓
IN_PROGRESS
    ↓
COMPLETED
    ↓
PAID
    ↓
RATED

Đây là một vấn đề rất quan trọng khi phân tích hệ thống.

4. Vấn đề 3 – Thông tin thanh toán chưa tập trung
Hệ thống cũ có vấn đề với:

tính cước
quản lý giao dịch
thanh toán điện tử
xử lý thanh toán thất bại
tra cứu lịch sử giao dịch
Doanh nghiệp muốn:

Trip completed
      ↓
Calculate fare
      ↓
Payment
   ↙      ↘
Cash    Online
           ↓
   Payment Provider

Đặc biệt:

CAB không được lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản.

Điều này cho thấy hệ thống mới cần có Payment Integration với bên thứ ba thay vì tự xử lý toàn bộ thông tin thanh toán.

5. Vấn đề 4 – Hệ thống cũ khó mở rộng
Đây là vấn đề ở cấp độ System Architecture.

Doanh nghiệp nói rất rõ:

“có khả năng phục vụ số lượng lớn khách hàng và tài xế”

và:

“các thành phần cần có khả năng mở rộng độc lập khi tải tăng”.

Điều đó có nghĩa là hệ thống cũ có khả năng đang gặp vấn đề scalability.

Ví dụ:

100 users
     ↓
System hoạt động tốt

10,000 users
     ↓
System chậm

100,000 users
     ↓
System có thể quá tải

Doanh nghiệp không muốn khi một module bị lỗi thì toàn bộ hệ thống chết.

Ví dụ:

Payment Service bị lỗi
        ↓
Booking vẫn phải hoạt động

hoặc:

Notification Service bị lỗi
        ↓
Customer vẫn có thể đặt xe

Đây là lý do họ yêu cầu:

Các thành phần có khả năng mở rộng độc lập.

6. Vấn đề 5 – Notification chưa đủ linh hoạt
Hệ thống CAB cần gửi rất nhiều thông báo.

Ví dụ:

Customer
Booking received
Driver assigned
Driver arrived
Trip completed
Payment successful/failed

Driver
New trip
Trip cancelled
Trip changed

Doanh nghiệp còn nói:

“có khả năng mở rộng thêm các kênh thông báo trong tương lai”.

Điều này có nghĩa là hiện tại có thể dùng:

Push Notification

nhưng tương lai muốn thêm:

SMS
Email
Zalo
WhatsApp
...

Do đó không nên thiết kế Notification quá cứng.

Nên có một lớp:

Notification Service
       ↓
 ┌─────┼─────┐
 ↓     ↓     ↓
Push  SMS   Email

7. Vấn đề 6 – Nhân viên vận hành thiếu công cụ quản lý
Đây là một pain point rất lớn.

Doanh nghiệp không chỉ cần app cho Customer và Driver.

Họ cần Operations/Admin System.

Nhân viên phải có thể:

quản lý customer
quản lý driver
quản lý vehicle
xem trip
xem trip đang chạy
xem trạng thái driver
xử lý trip lỗi
xem transaction
xem lịch sử
xem báo cáo
Có thể hình dung:

                  CAB PLATFORM
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
   Customer         Driver         Operations
       │               │               │
   Booking          Receive         Manage
   Tracking         Trip            Customer
   Payment          Update          Driver
   Rating           Status          Trip
                                    Report

Hệ thống cũ rõ ràng chưa cung cấp đầy đủ khả năng quản trị tập trung.

8. Vấn đề 7 – Thiếu dữ liệu để quản trị và ra quyết định
Ban lãnh đạo muốn biết:

Có bao nhiêu chuyến?
Doanh thu bao nhiêu?
Tỷ lệ hoàn thành?
Tỷ lệ hủy?
Driver nào hoạt động tốt?
Hiệu quả vận hành như thế nào?
Điều đó có nghĩa là dữ liệu hiện tại có thể:

phân tán
khó truy xuất
thiếu thống nhất
không có báo cáo realtime/định kỳ
Hệ thống mới phải biến dữ liệu nghiệp vụ thành thông tin quản trị.

9. Tại sao hệ thống cũ “không dùng được”?
Điểm này rất quan trọng.

Không nên hiểu câu:

“hệ thống cũ không dùng được”

theo nghĩa hệ thống hoàn toàn hỏng.

Chính xác hơn là:

Hệ thống cũ không còn phù hợp với mục tiêu phát triển và quy mô kinh doanh trong tương lai.

Có thể chia thành:

Vấn đề	Hệ thống cũ	Hệ thống mới
Phân công tài xế	Chủ yếu thủ công	Tự động
Tracking	Hạn chế	Theo dõi trạng thái chuyến
Driver matching	Chưa tối ưu	Tìm và ưu tiên tài xế
Payment	Chưa tập trung	Payment integration
Notification	Hạn chế	Mở rộng nhiều kênh
Operations	Khó quản lý	Admin/Operations portal
Reporting	Hạn chế	Dashboard & reports
Scalability	Khó mở rộng	Scale độc lập
Security	Chưa đáp ứng đầy đủ	Authentication + Authorization
Audit	Hạn chế	Audit log
Future expansion	Khó thay đổi	Kiến trúc linh hoạt

10. Khách hàng thực sự đang “đặt vấn đề” gì?
Nếu đi họp với khách hàng, mình sẽ viết Problem Statement như sau:

Công ty ABC đang gặp khó khăn trong việc quản lý và mở rộng dịch vụ đặt xe do hệ thống hiện tại phụ thuộc nhiều vào thao tác thủ công, đặc biệt trong việc phân công tài xế, theo dõi chuyến đi, quản lý thanh toán và vận hành. Hệ thống hiện tại chưa đáp ứng tốt nhu cầu phục vụ số lượng lớn khách hàng và tài xế, thiếu khả năng mở rộng độc lập, tích hợp với các dịch vụ bên ngoài và cung cấp dữ liệu quản trị. Điều này làm tăng chi phí vận hành, giảm khả năng kiểm soát chuyến đi và hạn chế khả năng phát triển các dịch vụ mới trong tương lai.

Đây chính là Business Problem.

11. Khách hàng muốn giải quyết vấn đề bằng gì?
Họ muốn xây dựng:

CAB System – một nền tảng đặt xe có khả năng tự động hóa quy trình từ lúc đặt xe đến khi hoàn thành và thanh toán, đồng thời hỗ trợ vận hành, báo cáo và mở rộng trong tương lai.

Mục tiêu không phải đơn giản:

"Xây một app đặt xe"

mà là:

              CAB PLATFORM
                    │
      ┌─────────────┼─────────────┐
      ↓             ↓             ↓
   Booking       Dispatch      Operations
      │             │             │
      ↓             ↓             ↓
    Trip         Driver        Reporting
      │          Matching          │
      ↓             ↓              ↓
   Payment       Location       Analytics
      │
      ↓
 Notification
      │
      ↓
    Rating

12. Business Goal – Mục tiêu kinh doanh
Từ yêu cầu, mình xác định khoảng 6 mục tiêu chính.

BG01 – Tự động hóa đặt xe
Giảm phụ thuộc vào nhân viên trong việc tiếp nhận và phân công chuyến.

BG02 – Tối ưu việc tìm tài xế
Tự động tìm tài xế phù hợp dựa trên:

vị trí
trạng thái
tiêu chí vận hành
mức độ ưu tiên
BG03 – Nâng cao trải nghiệm khách hàng
Khách hàng có thể:

đặt xe
theo dõi chuyến
biết tài xế
biết trạng thái
biết giá
thanh toán
đánh giá.
BG04 – Tăng hiệu quả vận hành
Nhân viên có một hệ thống tập trung để quản lý toàn bộ hoạt động.

BG05 – Hỗ trợ tăng trưởng
Hệ thống phải chịu được lượng khách hàng/tài xế tăng lên.

BG06 – Tạo nền tảng phát triển lâu dài
Có thể thêm:

loại xe mới
dịch vụ mới
payment provider mới
notification provider mới
công nghệ mới
mà không phải xây lại toàn bộ hệ thống.

13. Các Actor chính
Từ đề bài, BA có thể xác định:

                    CAB SYSTEM
                         │
       ┌─────────────────┼─────────────────┐
       ↓                 ↓                 ↓
   Customer           Driver           Operator
       │                 │                 │
       │                 │                 │
   Register          Profile          Manage Customer
   Login             Vehicle          Manage Driver
   Booking           Availability     Manage Vehicle
   Tracking          Accept Trip      Manage Trip
   Payment           Reject Trip      Handle Issue
   History            Trip Status     Transaction
   Rating             Location        Reports

Ngoài ra còn external actors/systems:

Payment Provider
Notification Provider
Map/Location Service

Có thể cần xác nhận thêm với khách hàng xem hệ thống có tích hợp:

Google Maps
Mapbox
một nhà cung cấp bản đồ khác
SMS provider
Email provider
Push notification provider
hay không.

14. Quy trình nghiệp vụ quan trọng nhất
Đây là core business flow của CAB.

Customer
   │
   │ Create Booking
   ↓
CAB
   │
   │ Validate request
   ↓
Search Driver
   │
   ├── Driver 1 reject/no response
   │
   ↓
Search Driver 2
   │
   ├── Driver accepts
   │
   ↓
Driver Assigned
   │
   ↓
Driver Arriving
   │
   ↓
Driver Arrived
   │
   ↓
Passenger Picked Up
   │
   ↓
Trip In Progress
   │
   ↓
Trip Completed
   │
   ↓
Calculate Fare
   │
   ├── Cash
   │
   └── Online Payment
   │
   ↓
Payment Result
   │
   ↓
Customer Rating

Đây chính là core business process mà BA cần đào sâu nhất.

15. Những vấn đề khách hàng chưa quyết định
Đây là phần cực kỳ quan trọng đối với BA.

Khách hàng đã nói rõ rằng còn nhiều vấn đề chưa chốt.

Fare
Chưa biết tính tiền:

Base fare?
Distance?
Duration?
Vehicle type?
Peak hour?
Surge?
Toll?
Promotion?

Driver matching
Chưa biết:

Ưu tiên theo khoảng cách?
Rating?
Acceptance rate?
Driver level?
Thời gian online?

Driver timeout
Ví dụ:

Driver được bao nhiêu giây để accept?
15s?
30s?
60s?

Cancellation
Chưa rõ:

Customer cancel → có phí không?
Driver cancel → xử lý thế nào?
Ai chịu phí?

Network failure
Ví dụ:

Driver mất mạng khi đang chạy?
Customer mất mạng?
Payment timeout?

Data retention
Chưa rõ:

Trip history lưu 1 năm?
3 năm?
5 năm?

Đây chính là Open Issues / Questions / Assumptions mà BA phải đưa ra để khách hàng xác nhận.

16. Nếu nhìn theo tư duy BA, dự án này có 4 tầng
Mình khuyên bạn nhớ mô hình này:

                 BUSINESS
                    │
                    ↓
             Business Problem
                    │
                    ↓
             Business Goal
                    │
                    ↓
              User Needs
                    │
                    ↓
           System Requirements
                    │
                    ↓
              Solution

Đối với CAB:

Business Problem
Quy trình đặt xe và vận hành hiện tại quá thủ công, khó mở rộng và thiếu khả năng quản lý tập trung.

↓

Business Goal
Tự động hóa và nâng cao khả năng vận hành dịch vụ đặt xe.

↓

User Needs
Customer cần đặt xe và theo dõi chuyến.

Driver cần nhận và thực hiện chuyến.

Operator cần quản lý hệ thống.

↓

System Requirements
Hệ thống phải có:

Authentication
Booking
Driver matching
Trip management
Tracking
Payment
Notification
Rating
Admin
Reporting
Audit
Security
↓

Solution
CAB Platform

“Tại sao phải xây dựng hệ thống CAB mới?”

Hệ thống hiện tại không đáp ứng tốt quy mô và nhu cầu phát triển của doanh nghiệp vì quy trình phân công tài xế còn thủ công, khả năng theo dõi chuyến đi hạn chế, thanh toán và thông tin vận hành chưa được quản lý tập trung, đồng thời hệ thống khó mở rộng khi số lượng khách hàng và tài xế tăng. Ngoài ra, doanh nghiệp cần tích hợp các dịch vụ bên ngoài như thanh toán, bản đồ và thông báo, đồng thời yêu cầu bảo mật, phân quyền, audit và báo cáo quản trị. Vì vậy, doanh nghiệp cần xây dựng một nền tảng CAB mới có khả năng tự động hóa quy trình đặt xe, mở rộng độc lập và linh hoạt bổ sung các tính năng, dịch vụ trong tương lai.

“Nghiệp vụ chính của hệ thống là gì?”

Quản lý toàn bộ vòng đời một chuyến xe: từ khách hàng tạo yêu cầu → tìm và phân công tài xế → tài xế thực hiện chuyến → hoàn thành → tính cước → thanh toán → đánh giá, đồng thời hỗ trợ quản lý khách hàng, tài xế, phương tiện, vận hành và báo cáo.


bước 2:
Được. Với B2 – Stakeholder Matrix, từ context CAB ở trên, mình sẽ xác định stakeholder trước rồi đưa vào ma trận Power / Interest.

Mình chưa xác định được “MOMES” là công cụ cụ thể nào qua nguồn web công khai, nên nếu bạn đang nói đến một tool MOMES trong khóa học/lớp của bạn, bạn có thể gửi ảnh giao diện MOMES; mình sẽ hướng dẫn đúng từng bước trên tool đó.

1. Stakeholder của dự án CAB
Stakeholder	Vai trò	Power	Interest
Business Owner / Sponsor	Quyết định đầu tư, mục tiêu kinh doanh	Cao	Cao
Operations Manager	Quản lý vận hành đặt xe	Cao	Cao
Operator / Call Center	Tiếp nhận và xử lý booking/trip	Trung bình	Cao
Customer	Đặt xe, thanh toán, đánh giá	Thấp	Cao
Driver	Nhận và thực hiện chuyến	Trung bình	Cao
Finance / Accounting	Quản lý doanh thu, transaction, đối soát	Cao	Trung bình
IT / System Admin	Quản trị hệ thống, hạ tầng	Cao	Cao
Security / Compliance	Bảo mật, audit, quyền truy cập	Cao	Trung bình
Payment Provider	Xử lý thanh toán online	Trung bình	Trung bình
Map / Location Provider	Cung cấp bản đồ, GPS, routing	Trung bình	Trung bình
Notification Provider	Push/SMS/Email	Thấp–TB	Trung bình

bước 2:
1. Trong MOMES, chọn loại biểu đồ
Nếu MOMES của bạn có lựa chọn template, hãy chọn:

Stakeholder Matrix / Power–Interest Grid

Thiết lập:

X-axis = Interest
Y-axis = Power / Influence
Bố cục:

                         POWER
                           ↑
            HIGH           │
                           │
       KEEP SATISFIED      │    MANAGE CLOSELY
                           │
                           │
                           │
       ────────────────────┼────────────────────→ INTEREST
                           │
       MONITOR             │    KEEP INFORMED
                           │
            LOW            │

2. Nhập 11 stakeholder của CAB
Bạn có thể nhập theo bảng dưới đây.

Stakeholder	Power	Interest	Quadrant
Business Owner / Sponsor	5	5	Manage Closely
Operations Manager	5	5	Manage Closely
IT / System Admin	5	5	Manage Closely
Finance / Accounting	4	3	Keep Satisfied
Security / Compliance	4	3	Keep Satisfied
Customer	2	5	Keep Informed
Driver	3	5	Keep Informed
Operator / Call Center	3	5	Keep Informed
Payment Provider	3	3	Keep Satisfied / Monitor
Map / Location Provider	3	3	Monitor
Notification Provider	2	3	Monitor

Nếu MOMES sử dụng thang 1–5, bạn nhập trực tiếp các giá trị trên.

3. Vị trí cụ thể trên Matrix
Sau khi nhập, bạn nên có bố cục gần như sau:

             HIGH POWER
                 ↑
                 │
 Finance         │       Business Owner
 Security        │       Operations Manager
                 │       IT / System Admin
                 │
─────────────────┼────────────────────────→ HIGH INTEREST
                 │
 Map Provider    │       Customer
 Payment         │       Driver
 Provider        │       Operator
                 │
 Notification    │
 Provider        │
                 │
             LOW POWER

Tuy nhiên, có một điểm mình muốn chỉnh so với bảng ban đầu:

Payment Provider
Không nhất thiết phải xếp Keep Satisfied cố định. Nếu ABC phụ thuộc rất nhiều vào một Payment Provider duy nhất thì Power của provider có thể tăng lên.

Ví dụ:

Payment Provider outage → Online payment không hoạt động.

Do đó trong project thực tế, BA nên đánh giá lại Power dựa trên mức độ phụ thuộc, không chỉ dựa trên việc provider có phải nhân viên nội bộ hay không.

4. Nếu MOMES yêu cầu nhập “Name / Role / Power / Interest”
Bạn có thể copy dữ liệu này để nhập lần lượt:

Business Owner / Sponsor | 5 | 5
Operations Manager | 5 | 5
IT / System Admin | 5 | 5
Finance / Accounting | 4 | 3
Security / Compliance | 4 | 3
Customer | 2 | 5
Driver | 3 | 5
Operator / Call Center | 3 | 5
Payment Provider | 3 | 3
Map / Location Provider | 3 | 3
Notification Provider | 2 | 3

Nếu MOMES cho nhập Description/Role, thêm:

Business Owner / Sponsor
→ Quyết định mục tiêu, scope, ngân sách và ưu tiên kinh doanh.

Operations Manager
→ Quản lý vận hành, dispatch, driver và xử lý sự cố.

IT / System Admin
→ Quản lý hạ tầng, integration, scalability và technical operation.

Finance / Accounting
→ Quản lý fare, transaction, revenue và reconciliation.

Security / Compliance
→ Quản lý security, authorization, audit và data protection.

Customer
→ Đặt xe, theo dõi chuyến, thanh toán và đánh giá.

Driver
→ Nhận chuyến, thực hiện chuyến và cập nhật trạng thái.

Operator / Call Center
→ Theo dõi và hỗ trợ xử lý booking/trip.

Payment Provider
→ Xử lý giao dịch thanh toán điện tử.

Map / Location Provider
→ Cung cấp location, routing và ETA.

Notification Provider
→ Cung cấp các kênh gửi notification.

5. Sau khi vẽ xong, ghi kết luận
Phần này rất nên đưa vào bài BA:

Stakeholder Analysis Result:
Dựa trên Power–Interest Matrix, Business Owner/Sponsor, Operations Manager và IT/System Admin là các stakeholder có mức Power và Interest cao nên cần được Manage Closely. Finance/Accounting và Security/Compliance có Power cao nhưng Interest tương đối thấp nên cần được Keep Satisfied. Customer, Driver và Operator có Interest cao nhưng Power thấp/trung bình nên cần được Keep Informed và thường xuyên thu thập feedback. Các external providers như Payment, Map/Location và Notification Provider cần được theo dõi và quản lý theo mức độ phụ thuộc và ảnh hưởng tới hệ thống.

Cách phân nhóm này phù hợp với nguyên tắc Power–Interest Matrix: high power/high interest → manage closely; high power/low interest → keep satisfied; low power/high interest → keep informed; low power/low interest → monitor. 
B
Business Analyst Learnings


bước 3:
Nếu BG01 = Giảm thời gian tìm tài xế, thì có thể thiết kế bộ Business Goal như sau:

ID	Business Goal	Mục tiêu
BG01	Giảm thời gian tìm tài xế	Rút ngắn thời gian từ khi khách hàng tạo yêu cầu đến khi tìm được tài xế phù hợp.
BG02	Tự động hóa việc tìm và phân công tài xế	Hệ thống tự động tìm, ưu tiên và phân công tài xế phù hợp thay vì phụ thuộc chủ yếu vào nhân viên vận hành.
BG03	Đa dạng hóa phương thức thanh toán	Cho phép khách hàng thanh toán bằng tiền mặt hoặc chuyển khoản/thanh toán điện tử.
BG04	Nâng cao khả năng theo dõi chuyến đi	Giúp khách hàng và nhân viên vận hành theo dõi trạng thái chuyến và thông tin tài xế.
BG05	Tăng hiệu quả vận hành	Cung cấp công cụ tập trung để nhân viên quản lý khách hàng, tài xế, phương tiện và chuyến đi.
BG06	Nâng cao khả năng mở rộng hệ thống	Hệ thống có thể phục vụ số lượng khách hàng và tài xế tăng lên mà vẫn đảm bảo hoạt động ổn định.
BG07	Tăng khả năng kiểm soát doanh thu và giao dịch	Tập trung dữ liệu fare, payment và transaction để hỗ trợ đối soát và báo cáo.
BG08	Tạo nền tảng linh hoạt cho phát triển tương lai	Cho phép bổ sung loại dịch vụ, phương thức thanh toán và nhà cung cấp notification mà không phải xây dựng lại toàn bộ hệ thống.

Mình đề xuất đặc biệt chỉnh BG02
Câu bạn viết:

“hệ thống phải có khả năng tự động tài xế”

nên sửa thành:

BG02 – Tự động hóa việc tìm và phân công tài xế

Vì “tự động tài xế” không rõ nghĩa về mặt nghiệp vụ. Business Goal cần thể hiện doanh nghiệp muốn đạt được điều gì, còn “hệ thống phải tự động tìm tài xế” sẽ phù hợp hơn ở tầng Business Requirement / Functional Requirement.

Ví dụ:

Business Goal:

BG02 – Tự động hóa việc tìm và phân công tài xế.

↓

Business Requirement:

BR02 – Hệ thống phải tự động xác định và lựa chọn tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và các tiêu chí vận hành.

↓

Functional Requirement:

FR02.1 – Khi Customer tạo booking, hệ thống phải tìm các Driver đang ở trạng thái AVAILABLE.

FR02.2 – Hệ thống phải ưu tiên Driver theo tiêu chí đã được doanh nghiệp cấu hình.

FR02.3 – Hệ thống phải gửi yêu cầu nhận chuyến cho Driver.

FR02.4 – Nếu Driver từ chối hoặc không phản hồi trong thời gian quy định, hệ thống phải tiếp tục tìm Driver khác.

Tương tự BG03
BG03 – Đa dạng hóa phương thức thanh toán

↓

Business Requirement:

BR03 – Hệ thống phải hỗ trợ khách hàng thanh toán bằng tiền mặt hoặc phương thức thanh toán điện tử.

↓

Functional Requirement:

FR03.1 – Customer có thể chọn Cash hoặc Electronic Payment.

FR03.2 – Với Electronic Payment, hệ thống phải tích hợp Payment Provider.

FR03.3 – CAB không lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản thanh toán.

FR03.4 – Hệ thống phải cập nhật kết quả giao dịch thành công/thất bại.

FR03.5 – Khi thanh toán thất bại, hệ thống phải thông báo cho Customer và cho phép xử lý lại theo chính sách doanh nghiệp.

Nếu bài yêu cầu “Mục đích – Mục tiêu nghiệp vụ”
Bạn có thể trình bày theo cấu trúc này:

Business Purpose

Xây dựng nền tảng CAB nhằm tự động hóa và tập trung hóa toàn bộ quy trình đặt xe, từ khi khách hàng tạo yêu cầu, tìm và phân công tài xế, thực hiện chuyến, tính cước, thanh toán đến đánh giá, đồng thời nâng cao hiệu quả vận hành và khả năng mở rộng của doanh nghiệp.

Business Goals

BG01: Giảm thời gian tìm tài xế.
BG02: Tự động hóa việc tìm và phân công tài xế.
BG03: Đa dạng hóa phương thức thanh toán.
BG04: Nâng cao khả năng theo dõi chuyến đi.
BG05: Tăng hiệu quả vận hành.
BG06: Nâng cao khả năng mở rộng hệ thống.
BG07: Tăng khả năng kiểm soát doanh thu và giao dịch.
BG08: Tạo nền tảng linh hoạt để phát triển các dịch vụ trong tương lai.
Lưu ý quan trọng: BG01 và BG02 có liên quan nhưng không trùng nhau. BG01 tập trung vào kết quả cần đạt (giảm thời gian), còn BG02 tập trung vào thay đổi nghiệp vụ (tự động hóa tìm và phân công). Điều này sẽ giúp bạn trace từ Business Goal → Business Requirement → Functional Requirement → Use Case rõ ràng hơn.

bước 4:
1. Phạm vi yêu cầu – In Scope
Mình đề xuất hệ thống CAB có 7 module nghiệp vụ chính:

STT	Module	Phạm vi chính
M01	Quản lý khách hàng	Đăng ký, đăng nhập, hồ sơ, lịch sử chuyến
M02	Quản lý tài xế & phương tiện	Hồ sơ tài xế, vehicle, trạng thái hoạt động
M03	Đặt xe & quản lý chuyến	Tạo booking, pickup, destination, loại xe, trạng thái trip
M04	Tìm & phân công tài xế	Tự động tìm, ưu tiên, accept/reject/timeout
M05	Tính cước & thanh toán	Fare, tiền mặt, chuyển khoản/thanh toán điện tử, transaction
M06	Thông báo	Thông báo cho Customer/Driver về booking, trip, payment
M07	Quản trị & vận hành	Quản lý customer, driver, vehicle, trip, transaction, báo cáo, phân quyền

Có thể hình dung hệ thống MPP/MVP cơ bản như sau:

                    CAB SYSTEM
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
  CUSTOMER          DRIVER           OPERATION
  MANAGEMENT        MANAGEMENT       MANAGEMENT
        │                │                │
        └──────────┬─────┴────────────────┘
                   │
                   ▼
             BOOKING / TRIP
                   │
                   ▼
              DISPATCH
                   │
          ┌────────┴────────┐
          ▼                 ▼
       FARE              PAYMENT
          │                 │
          └────────┬────────┘
                   ▼
              NOTIFICATION

M01 – Quản lý khách hàng
Trong phạm vi:

Đăng ký.
Đăng nhập.
Cập nhật thông tin cá nhân.
Quản lý tài khoản.
Xem lịch sử chuyến.
Xem thông tin thanh toán của chuyến.
M02 – Quản lý tài xế
Trong phạm vi:

Tạo tài khoản tài xế.
Cập nhật hồ sơ.
Quản lý thông tin phương tiện.
AVAILABLE / UNAVAILABLE.
Nhận thông báo chuyến.
Accept / Reject.
Cập nhật trạng thái chuyến.
Cập nhật vị trí.
M03 – Đặt xe & quản lý chuyến
Trong phạm vi:

Create Booking
      ↓
Pickup
      ↓
Destination
      ↓
Vehicle Type
      ↓
Search Driver
      ↓
Driver Assigned
      ↓
Trip
      ↓
Completed

Quản lý lifecycle của Trip.

M04 – Driver Dispatch
Đây là core module của CAB.

Booking
   ↓
Find Drivers
   ↓
Filter
   ↓
Rank
   ↓
Send Offer
   ↓
Accept?
 ┌─┴─────────────┐
YES             NO/TIMEOUT
 │                 │
 ▼                 ▼
Assigned       Next Driver

Module này nên nằm trong MVP vì đây chính là vấn đề nghiệp vụ lớn nhất mà khách hàng muốn giải quyết.

M05 – Fare & Payment
Trong phạm vi MVP:

Tính cước.
Hiển thị số tiền phải trả.
Cash.
Chuyển khoản/thanh toán điện tử.
Transaction status.
Payment success/failure.
Payment history.
Với online payment:

CAB
 │
 ▼
Payment Provider
 │
 ├── Success
 │
 └── Failed

CAB không lưu thông tin nhạy cảm của thẻ/tài khoản thanh toán.

M06 – Notification
MVP có thể giới hạn một hoặc một số kênh được khách hàng xác nhận.

Các event chính:

Booking received.
Driver assigned.
New trip.
Driver arrived.
Trip completed.
Payment success/failure.
Trip cancelled.
Kiến trúc nên để mở rộng thêm SMS/Email/etc. sau này.

M07 – Operation/Admin
Trong phạm vi:

Customer management.
Driver management.
Vehicle management.
Trip monitoring.
Driver status monitoring.
Xử lý trip exception.
Transaction lookup.
RBAC.
Audit log.
Báo cáo cơ bản.
2. Những thứ KHÔNG nên làm trong 7 tuần – Out of Scope
Đây là phần rất quan trọng. BA phải chủ động giới hạn scope, nếu không dự án rất dễ bị phình.

❌ 1. Không tự xây Payment Gateway
Không nên làm:

CAB
 ↓
Tự xử lý card
 ↓
Tự lưu card number
 ↓
Tự xử lý banking

Chỉ nên:

CAB → External Payment Provider

❌ 2. Không xây hệ thống bản đồ riêng
Không xây:

Map engine.
GPS platform.
Routing engine riêng.
Chỉ tích hợp với Map/Location Provider nếu cần.

❌ 3. Không xây hệ thống SMS/Email riêng
Không nên tự xây infrastructure gửi SMS/email.

CAB chỉ nên có Notification module/interface, sau đó tích hợp provider.

❌ 4. Không làm AI/ML Driver Matching trong MVP
Ví dụ không nên làm ngay:

Machine Learning ranking.
Predictive driver behavior.
AI demand prediction.
AI dynamic pricing.
MVP chỉ cần rule-based matching.

Ví dụ:

AVAILABLE
+
Correct Vehicle Type
+
Within Radius
+
Ranking Rule

❌ 5. Không làm Dynamic Pricing phức tạp
Nếu khách hàng chưa xác định:

Surge pricing.
Peak pricing.
Demand prediction.
Real-time pricing algorithm.
thì không nên đưa vào MVP.

❌ 6. Không làm Loyalty / Membership
Ví dụ:

VIP customer.
Membership tier.
Point.
Reward.
Cashback.
Đây là future scope.

❌ 7. Không làm Promotion/Coupon nếu chưa được yêu cầu
Không nên tự thêm:

Coupon.
Voucher.
Referral.
Promotion engine.
❌ 8. Không làm Scheduled Booking nếu khách hàng chưa yêu cầu
Ví dụ:

Đặt xe trước 2 ngày lúc 8:00 sáng.

Đây là một business flow khác và sẽ làm tăng scope dispatch.

❌ 9. Không làm Multi-stop nếu chưa có requirement
Ví dụ:

A → B → C → D

MVP chỉ nên:

Pickup → Destination

nếu đây là scope khách hàng xác nhận.

❌ 10. Không làm Multi-country / Multi-currency
Trong 7 tuần không nên tự mở rộng sang:

nhiều quốc gia
nhiều currency
timezone phức tạp
nếu ABC chưa yêu cầu.

❌ 11. Không làm Analytics/AI nâng cao
MVP chỉ cần báo cáo nghiệp vụ:

Total trips.
Completed trips.
Cancelled trips.
Revenue.
Driver performance.
Không cần xây Data Lake/AI analytics ngay.

3. Scope Boundary
Bạn có thể đưa vào tài liệu BA một bảng rất rõ như sau:

In Scope	Out of Scope
Customer Management	Loyalty/Membership
Driver Management	AI/ML Driver Matching
Vehicle Management	Dynamic Pricing nâng cao
Booking	Scheduled Booking
Trip Management	Multi-stop
Driver Dispatch	Tự xây Map Engine
Location Tracking cơ bản	Tự xây GPS Platform
Fare Calculation	Tự xây Payment Gateway
Cash Payment	Tự xây Banking System
Electronic Payment Integration	Tự xây SMS/Email Provider
Notification	Advanced AI Analytics
Operation Portal	Multi-country
RBAC	Multi-currency
Audit Log	Advanced Promotion Engine
Basic Reports	Advanced BI/Data Lake

4. Với dự án 7 tuần, nên chốt MVP như thế nào?
Nếu đây là bài BA và bạn cần vẽ Scope Diagram, mình sẽ lấy trung tâm:

                 ┌────────────────────┐
                 │    CAB SYSTEM      │
                 └─────────┬──────────┘
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
       ▼                   ▼                   ▼
 Customer              Driver             Operation
 Management            Management          Management
       │                   │                   │
       └─────────────┬─────┴───────────────────┘
                     ▼
                  Booking
                     │
                     ▼
                  Dispatch
                     │
                     ▼
                    Trip
                     │
              ┌──────┴──────┐
              ▼             ▼
            Fare          Payment
              │             │
              └──────┬──────┘
                     ▼
                Notification

Bên ngoài boundary:

┌──────────────────── OUT OF SCOPE ────────────────────┐

AI/ML Matching
Dynamic Pricing
Loyalty
Promotion
Scheduled Booking
Multi-stop
Own Map Engine
Own Payment Gateway
Advanced BI
Multi-country

└───────────────────────────────────────────────────────┘

5. Một điểm quan trọng: “MPP” hay “MVP”?
Nếu bạn đang nói MVP (Minimum Viable Product) thì với dự án 7 tuần, mình khuyên chốt MVP là:

Customer Management + Driver Management + Booking + Dispatch + Trip + Fare/Payment + Notification + Operation Portal cơ bản.

bước 5:
Mã	    Tên	                           Mô tả
BR01	Đặt chuyến	                   Hệ thống cho phép khách hàng tạo yêu cầu đặt xe bằng cách nhập điểm đón, điểm đến và lựa chọn loại xe/dịch vụ.
BR02	Quản lý khách hàng	           Hệ thống cho phép khách hàng đăng ký, đăng nhập, cập nhật thông tin cá nhân và xem lịch sử chuyến đi.
BR03	Quản lý tài xế	               Hệ thống cho phép quản lý hồ sơ tài xế, thông tin phương tiện và trạng thái hoạt động của tài xế.
BR04	Tự động tìm tài xế	           Hệ thống tự động tìm tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và các tiêu chí vận hành.
BR05	Phân công tài xế	           Hệ thống tự động gửi yêu cầu nhận chuyến cho tài xế phù hợp; nếu tài xế từ chối hoặc không phản hồi, hệ thống tiếp tục tìm tài xế khác.
BR06	Quản lý chuyến đi	           Hệ thống quản lý toàn bộ vòng đời chuyến đi từ lúc tạo yêu cầu, phân công tài xế, thực hiện chuyến đến khi hoàn thành hoặc hủy.
BR07	Theo dõi chuyến đi	           Hệ thống cho phép khách hàng theo dõi trạng thái chuyến, thông tin tài xế và thời gian dự kiến tài xế đến.
BR08	Quản lý vị trí tài xế	       Hệ thống ghi nhận vị trí tài xế để hỗ trợ tìm tài xế gần khách hàng và xác định thời gian dự kiến đến.
BR09	Tính cước	                   Hệ thống xác định số tiền khách hàng phải thanh toán dựa trên loại dịch vụ và thông tin chuyến đi theo chính sách của doanh nghiệp.
BR10	Thanh toán	                   Hệ thống cho phép khách hàng thanh toán bằng tiền mặt hoặc phương thức thanh toán điện tử/chuyển khoản.
BR11	Thông báo	                   Hệ thống gửi thông báo cho khách hàng và tài xế về các sự kiện quan trọng trong quá trình đặt và thực hiện chuyến.
BR12	Đánh giá tài xế	               Hệ thống cho phép khách hàng đánh giá tài xế sau khi chuyến đi hoàn thành.
BR13	Quản lý vận hành           	   Hệ thống cung cấp giao diện cho nhân viên vận hành quản lý khách hàng, tài xế, phương tiện và chuyến đi.
BR14	Báo cáo	                       Hệ thống cung cấp báo cáo về số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả hoạt động của tài xế.
BR15	Bảo mật và phân quyền	       Hệ thống xác thực người dùng, kiểm soát quyền truy cập và bảo vệ thông tin cá nhân, dữ liệu vị trí và dữ liệu giao dịch.

bước 6:

B6 – Business Process: Khách hàng đặt chuyến
1. Luồng nghiệp vụ tổng quát
[Bắt đầu]
    ↓
Khách hàng tạo chuyến đi
    ↓
Nhập điểm đón + điểm đến
    ↓
Chọn loại xe/dịch vụ
    ↓
Xác nhận yêu cầu đặt chuyến
    ↓
Hệ thống kiểm tra / xác nhận yêu cầu
    ↓
Tìm tài xế phù hợp
    ↓
┌─────────────────────────────┐
│ Có tìm được tài xế phù hợp? │
└──────────────┬──────────────┘
         Có    │       Không
          ↓    │         ↓
  Gửi yêu cầu nhận chuyến    Thông báo
       cho tài xế           không tìm được tài xế
          ↓                   ↓
   Tài xế phản hồi?        Kết thúc
       ↓
 ┌─────┴──────┐
 │            │
Nhận       Từ chối/
chuyến     Không phản hồi
 │            │
 ↓            ↓
Xác nhận    Tìm tài xế
tài xế      tiếp theo
 │            │
 ↓            └──────────────┐
Thông báo                     │
khách hàng                   │
 │                            │
 ↓                            │
Tài xế đang đến điểm đón     │
 │                            │
 ↓                            │
Tài xế đến điểm đón           │
 │                            │
 ↓                            │
Đón khách                      │
 │                            │
 ↓                            │
Thực hiện chuyến               │
 │                            │
 ↓                            │
Hoàn thành chuyến              │
 │                            │
 ↓                            │
Tính cước                     │
 │                            │
 ↓                            │
Thanh toán                     │
 │                            │
 ↓                            │
[Kết thúc] ←──────────────────┘

2. Chia theo Actor
Actor	Hoạt động
Customer	Tạo chuyến → nhập điểm đón/điểm đến → chọn loại xe → xác nhận đặt chuyến
CAB System	Kiểm tra yêu cầu → tìm tài xế phù hợp → gửi yêu cầu nhận chuyến
Driver	Nhận thông báo → Accept / Reject
CAB System	Nếu Accept → phân công tài xế; nếu Reject/Timeout → tìm tài xế tiếp theo
Customer	Nhận thông báo tài xế → theo dõi trạng thái chuyến
Driver	Đến điểm đón → đón khách → thực hiện chuyến → hoàn thành
CAB System	Tính cước → xử lý thanh toán → cập nhật trạng thái chuyến

3. Business Process chuẩn hóa
Có thể đặt tên process:

BP01 – Quy trình đặt và thực hiện chuyến xe

Trigger: Customer có nhu cầu đặt xe.

Input:

Điểm đón.
Điểm đến.
Loại xe/dịch vụ.
Thông tin khách hàng.
Process:

Customer tạo yêu cầu chuyến.
Customer nhập điểm đón và điểm đến.
Customer chọn loại xe/dịch vụ.
Customer xác nhận đặt chuyến.
CAB kiểm tra tính hợp lệ của yêu cầu.
CAB chuyển chuyến sang trạng thái tìm tài xế.
CAB tìm tài xế phù hợp.
CAB gửi yêu cầu nhận chuyến cho tài xế.
Driver Accept / Reject / Timeout.
Nếu Driver Accept → CAB phân công tài xế.
CAB thông báo thông tin tài xế cho Customer.
Driver di chuyển đến điểm đón.
CAB cập nhật/truyền trạng thái chuyến cho Customer.
Driver đón khách.
Driver thực hiện chuyến.
Driver hoàn thành chuyến.
CAB tính cước.
Customer thanh toán.
CAB cập nhật kết quả thanh toán.
Customer đánh giá Driver.
Kết thúc process.
4. Business Rule quan trọng trong bước tìm tài xế
Đây là phần bạn nên thể hiện rõ trong sơ đồ:

              Tìm tài xế
                   ↓
          Có tài xế phù hợp?
             /          \
           Có            Không
           ↓               ↓
      Gửi request       Thông báo
      cho Driver        Customer
           ↓               ↓
    Driver phản hồi?    Kết thúc
       /       \
    Accept    Reject/Timeout
      ↓           ↓
   Assign      Tìm Driver
   Driver       tiếp theo
      ↓           │
      └───────────┘


bước 7:
B7 – Phân rã yêu cầu nghiệp vụ
1. BR01 – Đặt chuyến
Mã	Tên Function Requirement	Mô tả
FR01	Nhập điểm đón	Hệ thống cho phép khách hàng nhập hoặc chọn vị trí điểm đón.
FR02	Nhập điểm đến	Hệ thống cho phép khách hàng nhập hoặc chọn vị trí điểm đến.
FR03	Chọn loại xe	Hệ thống cho phép khách hàng lựa chọn loại xe/dịch vụ phù hợp.
FR04	Xác nhận thông tin chuyến	Hệ thống hiển thị thông tin điểm đón, điểm đến và loại xe để khách hàng xác nhận.
FR05	Tạo yêu cầu đặt chuyến	Sau khi khách hàng xác nhận, hệ thống tạo booking và chuyển sang trạng thái tìm tài xế.
FR06	Kiểm tra yêu cầu	Hệ thống kiểm tra tính hợp lệ của thông tin trước khi tạo booking.

2. BR02 – Quản lý khách hàng
Mã	Tên Function Requirement	Mô tả
FR07	Đăng ký tài khoản	Hệ thống cho phép khách hàng tạo tài khoản.
FR08	Đăng nhập	Hệ thống xác thực khách hàng trước khi sử dụng chức năng yêu cầu tài khoản.
FR09	Cập nhật thông tin	Khách hàng có thể cập nhật thông tin cá nhân.
FR10	Xem lịch sử chuyến	Khách hàng có thể xem các chuyến đã thực hiện.
FR11	Xem chi tiết chuyến	Khách hàng có thể xem thông tin chi tiết của từng chuyến.

3. BR03 – Quản lý tài xế
Mã	Tên Function Requirement	Mô tả
FR12	Quản lý hồ sơ tài xế	Hệ thống lưu và quản lý thông tin hồ sơ tài xế.
FR13	Quản lý phương tiện	Hệ thống lưu thông tin phương tiện của tài xế.
FR14	Cập nhật trạng thái tài xế	Tài xế có thể chuyển trạng thái Online/Offline hoặc Available/Unavailable.
FR15	Cập nhật vị trí	Hệ thống ghi nhận vị trí hiện tại của tài xế.

4. BR04 – Tự động tìm tài xế
Đây chính là phần bạn đang hỏi và nên phân rã kỹ nhất.

Mã	Tên Function Requirement	Mô tả
FR16	Xác định vị trí khách hàng	Hệ thống phải xác định vị trí điểm đón của khách hàng để làm cơ sở tìm tài xế.
FR17	Xác định phạm vi tìm kiếm	Hệ thống xác định phạm vi/khu vực tìm kiếm tài xế xung quanh điểm đón.
FR18	Lọc tài xế đang hoạt động	Hệ thống chỉ lựa chọn các tài xế đang ở trạng thái Online/Available.
FR19	Lọc theo loại xe	Hệ thống chỉ lựa chọn tài xế có phương tiện phù hợp với loại xe khách hàng đã chọn.
FR20	Xác định khoảng cách	Hệ thống xác định khoảng cách hoặc thời gian dự kiến từ tài xế đến điểm đón.
FR21	Xếp hạng tài xế	Hệ thống ưu tiên tài xế phù hợp dựa trên các tiêu chí vận hành đã được doanh nghiệp xác định.
FR22	Ưu tiên tài xế có đánh giá cao	Hệ thống có thể ưu tiên tài xế có rating cao nếu đây là tiêu chí được doanh nghiệp phê duyệt.
FR23	Lựa chọn tài xế	Hệ thống lựa chọn tài xế phù hợp nhất từ danh sách tài xế đủ điều kiện.
FR24	Gửi yêu cầu nhận chuyến	Hệ thống gửi thông báo/yêu cầu nhận chuyến cho tài xế được lựa chọn.
FR25	Chờ phản hồi tài xế	Hệ thống chờ tài xế chấp nhận hoặc từ chối trong khoảng thời gian được quy định.
FR26	Xử lý tài xế chấp nhận	Khi tài xế chấp nhận, hệ thống gán tài xế cho chuyến và cập nhật trạng thái.
FR27	Xử lý tài xế từ chối	Khi tài xế từ chối, hệ thống loại tài xế khỏi lần tìm kiếm hiện tại và tiếp tục tìm tài xế khác.
FR28	Xử lý tài xế không phản hồi	Khi tài xế không phản hồi trong thời gian quy định, hệ thống xác định request timeout và tiếp tục tìm tài xế khác.
FR29	Tìm tài xế tiếp theo	Hệ thống tiếp tục lựa chọn tài xế khác khi tài xế trước đó từ chối hoặc timeout.
FR30	Thông báo không tìm được tài xế	Nếu không còn tài xế phù hợp, hệ thống thông báo cho khách hàng rằng không tìm được tài xế.

Luồng của BR04
BR04 – Tự động tìm tài xế
              │
              ▼
       FR16 Xác định vị trí
              │
              ▼
       FR17 Xác định phạm vi
              │
              ▼
       FR18 Lọc Driver Online
              │
              ▼
       FR19 Lọc loại xe
              │
              ▼
       FR20 Tính khoảng cách/ETA
              │
              ▼
       FR21 Xếp hạng Driver
              │
              ▼
       FR23 Chọn Driver
              │
              ▼
       FR24 Gửi request
              │
              ▼
        FR25 Chờ phản hồi
          /          \
     ACCEPT       REJECT/TIMEOUT
       ↓                ↓
 FR26 Assign       FR29 Driver tiếp theo
       ↓                │
       │          ┌─────┘
       │          ↓
       │      Có Driver?
       │       /       \
       │     Có        Không
       │      ↓          ↓
       │   Gửi request  FR30
       │                No Driver
       ↓
  Driver Assigned

5. BR05 – Phân công tài xế
Mã	Tên Function Requirement	Mô tả
FR31	Gán tài xế cho chuyến	Hệ thống gán tài xế khi tài xế chấp nhận chuyến.
FR32	Cập nhật trạng thái chuyến	Hệ thống cập nhật chuyến sang trạng thái Driver Assigned.
FR33	Thông báo cho khách hàng	Hệ thống thông báo cho khách hàng thông tin tài xế đã nhận chuyến.
FR34	Thông báo cho tài xế	Hệ thống cung cấp thông tin chuyến cho tài xế sau khi được phân công.

6. BR06 – Quản lý chuyến đi
Mã	Tên Function Requirement	Mô tả
FR35	Driver đang đến	Hệ thống cập nhật trạng thái tài xế đang di chuyển đến điểm đón.
FR36	Driver đã đến	Tài xế có thể cập nhật trạng thái đã đến điểm đón.
FR37	Đã đón khách	Tài xế cập nhật trạng thái đã đón khách.
FR38	Đang thực hiện chuyến	Hệ thống cập nhật trạng thái chuyến đang thực hiện.
FR39	Hoàn thành chuyến	Tài xế có thể xác nhận hoàn thành chuyến.
FR40	Hủy chuyến	Hệ thống xử lý việc hủy chuyến theo chính sách doanh nghiệp.

7. BR07 – Theo dõi chuyến
Mã	Tên Function Requirement	Mô tả
FR41	Xem trạng thái chuyến	Customer có thể xem trạng thái hiện tại của chuyến.
FR42	Xem thông tin tài xế	Customer có thể xem tài xế đã được phân công.
FR43	Xem vị trí tài xế	Customer có thể theo dõi vị trí tài xế trong phạm vi được cho phép.
FR44	Xem ETA	Hệ thống cung cấp thời gian dự kiến tài xế đến điểm đón.

8. BR09 – Tính cước & BR10 – Thanh toán
Mã	Tên Function Requirement	Mô tả
FR45	Tính cước chuyến	Hệ thống tính số tiền phải trả dựa trên quy tắc tính cước đã được xác nhận.
FR46	Chọn phương thức thanh toán	Customer có thể chọn tiền mặt hoặc thanh toán điện tử/chuyển khoản.
FR47	Xử lý thanh toán điện tử	Hệ thống gửi yêu cầu thanh toán tới Payment Provider.
FR48	Nhận kết quả thanh toán	Hệ thống nhận và cập nhật trạng thái giao dịch thành công/thất bại.
FR49	Xử lý thanh toán thất bại	Hệ thống thông báo cho Customer và cho phép xử lý lại theo chính sách doanh nghiệp.
FR50	Lưu lịch sử giao dịch	Hệ thống lưu thông tin giao dịch phục vụ tra cứu và đối soát.

9. BR11 – Thông báo
Mã	Tên Function Requirement	Mô tả
FR51	Thông báo tạo booking	Gửi thông báo khi yêu cầu đặt chuyến được tiếp nhận.
FR52	Thông báo tài xế nhận chuyến	Gửi thông báo khi tài xế đã nhận chuyến.
FR53	Thông báo tài xế đến	Gửi thông báo khi tài xế đến điểm đón.
FR54	Thông báo hoàn thành	Gửi thông báo khi chuyến hoàn thành.
FR55	Thông báo thanh toán	Gửi kết quả thanh toán cho khách hàng.
FR56	Thông báo cho tài xế	Gửi thông báo về chuyến mới hoặc thay đổi liên quan đến chuyến.

10. BR12 – Đánh giá
Mã	Tên Function Requirement	Mô tả
FR57	Đánh giá tài xế	Customer có thể đánh giá tài xế sau khi chuyến hoàn thành.
FR58	Lưu đánh giá	Hệ thống lưu kết quả đánh giá để phục vụ lịch sử và báo cáo.

11. BR13 – Quản lý vận hành
Mã	Tên Function Requirement	Mô tả
FR59	Quản lý Customer	Operator có quyền xem và quản lý thông tin khách hàng theo quyền được cấp.
FR60	Quản lý Driver	Operator có quyền xem và quản lý thông tin tài xế.
FR61	Quản lý Vehicle	Operator có quyền quản lý thông tin phương tiện.
FR62	Theo dõi chuyến đang chạy	Operator có thể xem các chuyến đang diễn ra và trạng thái hiện tại.
FR63	Xử lý chuyến lỗi	Operator có thể hỗ trợ xử lý các trường hợp chuyến gặp sự cố theo quyền được cấp.
FR64	Tra cứu giao dịch	Operator có quyền xem lịch sử giao dịch theo quyền được cấp.

12. Cách trình bày B7 trong bài
Bạn có thể lấy BR04 – Tự động tìm tài xế làm ví dụ phân rã chính:

BR04 – Tự động tìm tài xế
│
├── FR16 – Xác định vị trí khách hàng
├── FR17 – Xác định phạm vi tìm kiếm
├── FR18 – Lọc tài xế Online/Available
├── FR19 – Lọc theo loại xe
├── FR20 – Xác định khoảng cách/ETA
├── FR21 – Xếp hạng tài xế
├── FR22 – Ưu tiên tài xế có rating cao
├── FR23 – Chọn tài xế
├── FR24 – Gửi yêu cầu nhận chuyến
├── FR25 – Chờ phản hồi
├── FR26 – Xử lý Accept
├── FR27 – Xử lý Reject
├── FR28 – Xử lý Timeout
├── FR29 – Tìm tài xế tiếp theo
└── FR30 – Thông báo không tìm được tài xế

Lưu ý: FR22 – Ưu tiên tài xế có đánh giá cao hiện mới là yêu cầu bạn đề xuất, chưa phải requirement đã được khách hàng xác nhận. Vì đề bài nói “một số tiêu chí vận hành khác” nhưng chưa chốt cụ thể. Khi làm tài liệu chính thức, nên đánh dấu Pending Confirmation cho tiêu chí rating, khoảng cách, timeout và cách ranking.

B8 – Business Rules
Mã	Quy định nghiệp vụ	Mô tả
BRULE01	Chỉ tài xế sẵn sàng mới được nhận chuyến	Chỉ những tài xế có trạng thái Available/Online mới được hệ thống đưa vào danh sách tìm kiếm và phân công chuyến.
BRULE02	Tài xế phải phù hợp loại xe	Tài xế chỉ được nhận chuyến nếu phương tiện đáp ứng loại xe/dịch vụ mà khách hàng đã lựa chọn.
BRULE03	Tài xế phải nằm trong phạm vi tìm kiếm	Hệ thống chỉ tìm những tài xế nằm trong phạm vi/khu vực tìm kiếm được cấu hình.
BRULE04	Ưu tiên tài xế phù hợp	Hệ thống ưu tiên tài xế dựa trên các tiêu chí vận hành đã được doanh nghiệp xác nhận, ví dụ khoảng cách hoặc ETA.
BRULE05	Một chuyến chỉ có một tài xế	Một booking chỉ được gán cho một tài xế tại một thời điểm.
BRULE06	Tài xế phải xác nhận chuyến	Tài xế phải Accept chuyến trước khi hệ thống chính thức phân công chuyến cho tài xế đó.
BRULE07	Thời gian phản hồi tài xế	Tài xế được 30 giây để Accept hoặc Reject chuyến.
BRULE08	Timeout tài xế	Nếu sau 30 giây tài xế không phản hồi, hệ thống xem request là Timeout và chuyển sang tài xế tiếp theo.
BRULE09	Tài xế từ chối chuyến	Nếu tài xế Reject, hệ thống không gửi lại cùng request cho tài xế đó và tiếp tục tìm tài xế khác.
BRULE10	Không tìm được tài xế	Nếu không còn tài xế phù hợp, hệ thống thông báo cho khách hàng rằng chưa tìm được tài xế.
BRULE11	Không tạo lại booking	Khi tài xế từ chối hoặc timeout, khách hàng không cần tạo lại booking; hệ thống tự động tiếp tục quá trình tìm kiếm.
BRULE12	Tài xế được gán phải chuyển trạng thái	Sau khi Accept và được phân công, tài xế phải chuyển từ Available sang trạng thái đang thực hiện chuyến/Busy.
BRULE13	Không cho tài xế nhận nhiều chuyến đồng thời	Một tài xế đang thực hiện chuyến không được nhận thêm chuyến mới nếu chính sách doanh nghiệp không cho phép.
BRULE14	Chỉ được đánh giá sau khi hoàn thành	Khách hàng chỉ được đánh giá tài xế sau khi chuyến đã hoàn thành.
BRULE15	Chỉ tính cước khi chuyến hoàn thành	Hệ thống thực hiện tính cước chính thức sau khi chuyến chuyển sang trạng thái Completed.

B8.1 – Quy tắc tìm tài xế
Đây là phần quan trọng nhất của bài CAB.

Luồng nghiệp vụ
Customer tạo chuyến
        ↓
Xác định điểm đón
        ↓
Tìm Driver
        ↓
Lọc Driver
        │
        ├── Available?
        ├── Đúng loại xe?
        ├── Trong phạm vi?
        └── Đủ điều kiện?
        ↓
Xếp hạng Driver
        ↓
Chọn Driver A
        ↓
Gửi request
        ↓
     Chờ 30s
        ↓
   Driver phản hồi?
      /        \
   Accept    Reject/Timeout
     ↓            ↓
  Assign       Driver B
     ↓            ↓
Thông báo      Gửi request
Customer       cho B

B8.2 – Exception Handling
Đây là phần bạn hỏi về “khi xảy ra ngoại lệ thì phải làm sao?”

Mã	Ngoại lệ	Cách xử lý
EX01	Không có tài xế Available	Hệ thống thông báo cho khách hàng hiện chưa tìm được tài xế và kết thúc quá trình tìm kiếm.
EX02	Tài xế A không phản hồi trong 30 giây	Hệ thống đánh dấu request của A là Timeout và tự động chuyển sang tài xế tiếp theo.
EX03	Tài xế A từ chối	Hệ thống loại A khỏi danh sách của booking hiện tại và tìm tài xế khác.
EX04	Tài xế đang được đề xuất chuyển sang Offline	Hệ thống hủy request đối với tài xế đó và tìm tài xế khác.
EX05	Tài xế không còn phù hợp	Hệ thống kiểm tra lại trạng thái tài xế trước khi phân công; nếu không phù hợp thì bỏ qua và tìm tài xế khác.
EX06	Không còn tài xế phù hợp	Hệ thống thông báo khách hàng không tìm được tài xế và kết thúc booking theo chính sách doanh nghiệp.
EX07	Khách hàng hủy khi đang tìm tài xế	Hệ thống dừng quá trình tìm kiếm và hủy các request đang chờ phản hồi.
EX08	Mất kết nối của khách hàng	Hệ thống vẫn duy trì booking trong thời gian quy định; khi khách hàng kết nối lại thì hiển thị trạng thái mới nhất.
EX09	Mất kết nối của tài xế	Hệ thống kiểm tra trạng thái tài xế; nếu không đáp ứng điều kiện nhận chuyến thì chuyển sang tài xế khác.
EX10	Payment thất bại	Hệ thống ghi nhận giao dịch thất bại, thông báo khách hàng và cho phép thanh toán lại theo chính sách.

B8.3 – Trường hợp bạn đưa ra: Driver A không Accept trong 30 giây
Đây nên được viết thành Business Rule cụ thể:

BRULE07: Tài xế được 30 giây để phản hồi yêu cầu nhận chuyến.

BRULE08: Nếu tài xế không phản hồi trong 30 giây, hệ thống xác định yêu cầu là Timeout, thu hồi yêu cầu khỏi tài xế A và chuyển sang tài xế tiếp theo phù hợp.

Flow:
Customer
   │
   │ Create Booking
   ↓
CAB
   │
   │ Find Driver
   ↓
Driver A
   │
   │ Request Trip
   ↓
┌───────────────────────┐
│       Wait 30s        │
└───────────┬───────────┘
            ↓
      Driver Response?
        /           \
      YES            NO
       ↓             ↓
   Accept?        TIMEOUT
    /   \            ↓
  YES   REJECT    Driver A
   ↓      ↓       removed
Assign    │           ↓
Driver    │       Find Driver B
   │      │           ↓
   │      └──────→ Send Request
   │                  │
   ↓                  ↓
Notify Customer     Wait 30s
   │                  │
   ↓                  ↓
Driver arriving    ...

B8.4 – Một điểm cần chốt với khách hàng
Có một vấn đề BA không nên tự quyết định:

Sau khi Driver A timeout, hệ thống có được gửi request đồng thời cho A, B, C hay phải gửi tuần tự A → B → C?

Đề bài hiện tại nghiêng về tuần tự, nhưng cần xác nhận.

Phương án 1 – Tuần tự
Driver A → 30s → Driver B → 30s → Driver C

Ưu: dễ kiểm soát, tránh nhiều tài xế cùng Accept.

Phương án 2 – Song song
       ┌→ Driver A
Booking├→ Driver B
       └→ Driver C
              ↓
       Ai Accept trước
              ↓
        Assign Driver

Ưu: tìm tài xế nhanh hơn.

Nhưng: phải có cơ chế xử lý khi nhiều tài xế cùng Accept.

👉 Với MVP 7 tuần, mình khuyên đề xuất tuần tự để giảm độ phức tạp, sau đó ghi nhận Parallel Driver Dispatch là phương án có thể mở rộng trong tương lai.

Bộ B8 hoàn chỉnh nên có:
Business Rules
→ BRULE01–BRULE15

Business Exceptions
→ EX01–EX10

Open Questions cần khách hàng xác nhận
→ Timeout 30s, bán kính tìm kiếm, tiêu chí ưu tiên, tuần tự/song song, số lần retry, thời gian tối đa tìm tài xế.

Đây sẽ là nền rất tốt để sang B9 – Use Case / Activity Diagram cho quy trình Customer đặt chuyến → Driver Matching → Driver Accept/Reject/Timeout.

bước 9:
B9 – Data Modeling
1. Data Model tổng quan
Mã	Data Model	Dữ liệu cần quản lý
DM01	Customer	Thông tin khách hàng
DM02	Driver	Thông tin tài xế
DM03	Vehicle	Thông tin phương tiện
DM04	Vehicle Type	Loại xe/dịch vụ
DM05	Booking	Yêu cầu đặt chuyến
DM06	Trip	Chuyến xe thực tế
DM07	Driver Location	Vị trí tài xế
DM08	Fare	Thông tin tính cước
DM09	Payment	Thông tin thanh toán
DM10	Rating	Đánh giá tài xế
DM11	Notification	Thông báo
DM12	Operator	Nhân viên vận hành
DM13	Role	Vai trò/phân quyền
DM14	Audit Log	Lịch sử thao tác

2. Chi tiết từng Data Model
DM01 – Customer
CUSTOMER
-------------------------
PK customer_id
   full_name
   phone
   email
   address
   status
   created_at
   updated_at

Mục đích: quản lý người đặt xe.

Quan hệ dự kiến:

Customer 1 — N Booking

DM02 – Driver
DRIVER
-------------------------
PK driver_id
   full_name
   phone
   email
   license_number
   status
   rating
   created_at

Status:

OFFLINE
AVAILABLE
BUSY
SUSPENDED

Quan hệ:

Driver 1 — N Trip

DM03 – Vehicle
VEHICLE
-------------------------
PK vehicle_id
FK driver_id
FK vehicle_type_id
   plate_number
   brand
   model
   color
   status

Quan hệ:

Driver 1 — N Vehicle

Vehicle Type 1 — N Vehicle

DM04 – Vehicle Type
VEHICLE_TYPE
-------------------------
PK vehicle_type_id
   type_name
   description
   status

Ví dụ:

4 chỗ
7 chỗ
Premium
DM05 – Booking
Đây là một Entity rất quan trọng.

BOOKING
-------------------------
PK booking_id
FK customer_id
FK vehicle_type_id
   pickup_address
   pickup_latitude
   pickup_longitude
   destination_address
   destination_latitude
   destination_longitude
   booking_time
   status
   created_at

Quan hệ:

Customer 1 — N Booking

Vehicle Type 1 — N Booking

Ví dụ:

Customer A
     │
     ├── Booking 001
     ├── Booking 002
     └── Booking 003

DM06 – Trip
Booking = yêu cầu đặt xe

Trip = chuyến xe thực tế

TRIP
-------------------------
PK trip_id
FK booking_id
FK driver_id
   status
   start_time
   pickup_time
   completed_time
   created_at

Quan hệ:

Booking 1 — 0..1 Trip

Driver 1 — N Trip

Ví dụ:

Customer
   ↓
Booking
   ↓
Driver tìm thấy
   ↓
Trip được tạo

DM07 – Driver Location
DRIVER_LOCATION
-------------------------
PK location_id
FK driver_id
   latitude
   longitude
   recorded_at

Quan hệ:

Driver 1 — N Driver Location

Ví dụ:

Driver A
  │
  ├── Location 08:00
  ├── Location 08:01
  ├── Location 08:02
  └── Location 08:03

Data này phục vụ:

tìm tài xế gần khách
tính khoảng cách
ETA
tracking
DM08 – Fare
FARE
-------------------------
PK fare_id
FK trip_id
   base_fare
   distance_fare
   duration_fare
   surcharge
   discount
   total_amount
   calculated_at

Quan hệ:

Trip 1 — 1 Fare

DM09 – Payment
PAYMENT
-------------------------
PK payment_id
FK trip_id
   payment_method
   transaction_reference
   amount
   status
   payment_time
   failure_reason

Status:

PENDING
SUCCESS
FAILED

Có thể có:

Trip
 │
 ├── Payment #1 → FAILED
 │
 └── Payment #2 → SUCCESS

nếu khách hàng thanh toán lại.

DM10 – Rating
RATING
-------------------------
PK rating_id
FK trip_id
FK customer_id
FK driver_id
   score
   comment
   created_at

Quan hệ:

Customer 1 — N Rating

Driver 1 — N Rating

Trip 1 — 0..1 Rating

DM11 – Notification
NOTIFICATION
-------------------------
PK notification_id
   recipient_id
   type
   title
   content
   channel
   status
   sent_at
   created_at

Ví dụ:

BOOKING_CREATED
DRIVER_ASSIGNED
DRIVER_ARRIVED
TRIP_COMPLETED
PAYMENT_SUCCESS
PAYMENT_FAILED

DM12 – Operator
OPERATOR
-------------------------
PK operator_id
FK role_id
   full_name
   email
   phone
   status

DM13 – Role
ROLE
-------------------------
PK role_id
   role_name
   description

Ví dụ:

ADMIN
OPERATOR
SUPERVISOR
FINANCE

DM14 – Audit Log
AUDIT_LOG
-------------------------
PK audit_id
FK operator_id
   action
   entity_name
   entity_id
   old_value
   new_value
   created_at

Ví dụ:

Operator A
     ↓
Cancel Trip
     ↓
AUDIT_LOG

3. Từ Data Model → xác định Entity
Sau khi xây dựng Data Model, ta có danh sách Entity:

Customer
Driver
Vehicle
Vehicle Type
Booking
Trip
Driver Location
Fare
Payment
Rating
Notification
Operator
Role
Audit Log

Đây chính là các hình chữ nhật Entity mà bạn sẽ đưa vào ERD.

4. Xác định Relationship trước khi vẽ MOMES
Đây là phần rất quan trọng.

Entity A	Quan hệ	Entity B
Customer	1 — N	Booking
Vehicle Type	1 — N	Booking
Booking	1 — 0..1	Trip
Driver	1 — N	Trip
Driver	1 — N	Vehicle
Vehicle Type	1 — N	Vehicle
Driver	1 — N	Driver Location
Trip	1 — 1	Fare
Trip	1 — N	Payment
Trip	1 — 0..1	Rating
Customer	1 — N	Rating
Driver	1 — N	Rating
Role	1 — N	Operator
Operator	1 — N	Audit Log

5. ERD để vẽ trên MOMES
Khi đưa vào MOMES, mình khuyên đầu tiên chỉ vẽ ERD Core, tránh quá nhiều Entity:

                    ┌──────────────┐
                    │   CUSTOMER   │
                    └──────┬───────┘
                           │
                           │ 1:N
                           ▼
                    ┌──────────────┐
                    │   BOOKING    │
                    └──────┬───────┘
                           │
                         1:0..1
                           │
                           ▼
                    ┌──────────────┐
                    │     TRIP     │
                    └────┬────┬────┘
                         │    │
                    N:1  │    │ 1:1
                         │    │
                  ┌──────▼┐  ┌▼─────────┐
                  │DRIVER │  │   FARE   │
                  └───┬───┘  └──────────┘
                      │
                 ┌────┴─────────┐
                 │              │
                1:N            1:N
                 │              │
          ┌──────▼─────┐ ┌──────▼─────────┐
          │  VEHICLE   │ │DRIVER_LOCATION │
          └──────┬─────┘ └────────────────┘
                 │
                N:1
                 │
          ┌──────▼────────┐
          │ VEHICLE_TYPE  │
          └───────────────┘

                 TRIP
                  │
             ┌────┴─────┐
             │          │
            1:N        1:0..1
             │          │
        ┌────▼────┐ ┌───▼─────┐
        │ PAYMENT │ │ RATING  │
        └─────────┘ └─────────┘

6. Khi vẽ bằng MOMES
Bạn có thể tạo lần lượt các Entity:

Customer → Booking → Trip → Driver → Vehicle → Vehicle Type → Driver Location → Fare → Payment → Rating

Sau đó nối Relationship.

Ví dụ Entity CUSTOMER:

┌─────────────────────────┐
│        CUSTOMER         │
├─────────────────────────┤
│ PK customer_id         │
│    full_name            │
│    phone                │
│    email                │
│    address              │
│    status               │
│    created_at            │
└─────────────────────────┘

Entity BOOKING:

┌─────────────────────────┐
│        BOOKING          │
├─────────────────────────┤
│ PK booking_id           │
│ FK customer_id          │
│ FK vehicle_type_id      │
│    pickup_address       │
│    pickup_latitude      │
│    pickup_longitude     │
│    destination_address  │
│    destination_latitude │
│    destination_longitude│
│    booking_time         │
│    status               │
└─────────────────────────┘

Sau đó nối:

CUSTOMER 1 ───────── N BOOKING

Điểm BA cần nhớ ở B9
Data Modeling không phải chỉ là liệt kê bảng database.

Bạn đang trả lời 3 câu hỏi:

Nghiệp vụ có những đối tượng nào? → Entity.
Mỗi đối tượng cần lưu thông tin gì? → Attribute.
Các đối tượng liên hệ với nhau thế nào? → Relationship/Cardinality.
Sau khi trả lời 3 câu hỏi này, bạn mới có đủ cơ sở để vẽ ERD trên MOMES.

b10:
B10 – Non-Functional Requirements
        Mã	Nhóm NFR	Yêu cầu
    NFR01	Performance	Hệ thống phải phản hồi các thao tác thông thường của người dùng trong thời gian tối đa 2 giây trong điều kiện tải bình thường.
    NFR02	Performance	Khi khách hàng tạo booking, hệ thống phải bắt đầu quá trình tìm tài xế trong tối đa 3 giây sau khi booking hợp lệ được xác nhận.
    NFR03	Scalability	Hệ thống phải có khả năng mở rộng để đáp ứng số lượng khách hàng và tài xế tăng lên mà không cần thiết kế lại toàn bộ hệ thống.
    NFR04	Availability	Hệ thống phải hoạt động ổn định, đặc biệt trong thời gian nhu cầu đặt xe cao.
    NFR05	Reliability	Lỗi của một thành phần như Payment hoặc Notification không được làm cho toàn bộ chức năng Booking bị dừng.
    NFR06	Security	Người dùng phải được xác thực trước khi sử dụng các chức năng yêu cầu tài khoản.
    NFR07	Authorization	Chức năng quản trị phải được phân quyền theo vai trò; nhân viên không có quyền không được thực hiện thao tác nhạy cảm.
    NFR08	Data Security	Thông tin cá nhân, thông tin tài xế, phương tiện, vị trí và giao dịch phải được bảo vệ khỏi truy cập trái phép.
    NFR09	Payment Security	Hệ thống CAB không được lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản thanh toán.
    NFR10	Auditability	Các thao tác quản trị và thao tác quan trọng phải được ghi nhận vào Audit Log để phục vụ kiểm tra.
    NFR11	Maintainability	Các module của hệ thống phải được thiết kế độc lập tương đối để có thể bảo trì và thay đổi mà hạn chế ảnh hưởng đến các module khác.
    NFR12	Extensibility	Hệ thống phải cho phép bổ sung loại dịch vụ, loại xe, phương thức thanh toán hoặc nhà cung cấp thông báo mới mà không phải xây dựng lại toàn bộ hệ thống.
    NFR13	Availability/Resilience	Khi Notification Provider gặp lỗi, các chức năng cốt lõi như tạo booking và quản lý trip vẫn phải tiếp tục hoạt động.
    NFR14	Integration	Hệ thống phải có khả năng tích hợp với các hệ thống bên ngoài như Payment Provider, Map/Location Provider và Notification Provider.
    NFR15	Data Integrity	Dữ liệu booking, trip, fare và payment phải đảm bảo tính chính xác và nhất quán, đặc biệt khi xảy ra lỗi hoặc timeout.
    NFR16	Backup & Recovery	Dữ liệu quan trọng phải được sao lưu và có khả năng khôi phục khi xảy ra sự cố.
    NFR17	Usability	Giao diện Customer, Driver và Operator phải dễ sử dụng và phù hợp với nghiệp vụ của từng nhóm người dùng.
    NFR18	Monitoring	Hệ thống phải có khả năng giám sát trạng thái hoạt động và phát hiện 


b11:



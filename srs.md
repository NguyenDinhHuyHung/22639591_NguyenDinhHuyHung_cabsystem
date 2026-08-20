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

bước 5

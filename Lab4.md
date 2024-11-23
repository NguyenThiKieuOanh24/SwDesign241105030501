# Ca sử dụng Login
## 1. Describe Interaction Among Design Objects
- Người dùng nhập thông tin tài khoản và mật khẩu.
- Giao diện Đăng nhập (LoginForm) gửi thông tin đăng nhập đến Bộ điều khiển Đăng nhập (LoginController).
- Bộ điều khiển Đăng nhập xác thực thông tin người dùng thông qua Hệ thống bảo mật (SecuritySubsystem).
- Nếu hợp lệ, hệ thống chuyển hướng đến trang chính. Nếu không, thông báo lỗi được hiển thị.

## 2. Simplify Sequence Diagrams Using Subsystems
### Mô tả: 
- Chuyển LoginController và SecuritySubsystem thành một gói duy nhất, gọi là SecuritySubsystem.

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/L8yn3i8m34LtdyBgm5QnTq1TojG1gU808RLG14agsr7Lip5m9Av0qWo8nRA-t_zV_hpUlQXXJVu9yd01EGg1iHePhq8CIpuwwnOJ59intbquH_OD6i6nRF_0H3QnqsrADzb4gO9PpG902SJsL8qT3a6fjWJZ2GzuCI9hv1bse93LsM4UtYdk_L15R7z9kvuXQqdaE317Xfx2NBxw0W00__y30000)

## 3. Describe Persistence-Related Behavior
### Mô tả:
- Database lưu trữ thông tin người dùng (tên đăng nhập và mật khẩu).
- SecuritySubsystem xử lý xác thực, không lưu mật khẩu gốc.

![Biểu đồ lớp](https://www.planttext.com/api/plantuml/png/T9112i8m44NtESKi5Um5if0YBjmN3p1j1mscYMIIIX5Fvi8ZUGMJMYDOt0r__d_pa-VzKR97vqEd1P-K0MUPHAEH6VPC3gu2e80GHuCTIQYyK-OmYkTekbZNxf2FUN4JKxgY9ZZbXohKFB2dRaG1zAXLYvuMlynL1dwKfOIDjPhGVB5Rz5WZqqHp59tKK-ew8yPyqbDutgOerkyNobo9_zZoJPdliIZ9jEdNNW000F__0m00)

## 4. Refine the Flow of Events Description
### 4.1 Basic Flow:

- Người dùng mở giao diện đăng nhập.
- Nhập tên người dùng và mật khẩu.
- Nhấn nút "Đăng nhập".
- Hệ thống xác thực thông tin, nếu hợp lệ, người dùng được cấp quyền truy cập.
### 4.2 Alternative Flow:

- Nếu tên người dùng hoặc mật khẩu không hợp lệ:
  - Hiển thị thông báo lỗi.
  - Cho phép người dùng nhập lại thông tin.
- Người dùng có thể chọn "Hủy" để quay lại giao diện chính.
### Lý Do:
- Việc chi tiết hóa giúp các nhà phát triển hiểu rõ luồng công việc, đặc biệt là trong các trường hợp lỗi hoặc hủy bỏ.

## 5. Unify Classes and Subsystems
### Hợp nhất các lớp và hệ thống con:
- LoginForm và LoginController được gộp vào SecuritySubsystem.
- SecuritySubsystem bao gồm cả lớp xác thực (Validator) và kết nối cơ sở dữ liệu.

![Biểu đồ](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTnTcQUGb5-SIfNGM9oTc9wga9mQd9fKMP9PN1fKd5bSKbgha8rbu92SavYSR62JtvwPfvRVb4kgeXpVbv9KNvEJceHN3miCISp9R4a7o7YabYIc9G8jAYMYmjkZeAUdXs66MXyi1g4UN0MM1nkgaDgNWh8Gm00003__mC0)

## Lý Do:
- Việc hợp nhất giúp nhóm các thành phần liên quan chặt chẽ lại với nhau, tăng tính mô-đun và dễ quản lý.
# Ca sử dụng Run Payroll
## 1. Describe Interaction Among Design Objects
### Mô tả:
- Quy trình tính lương chạy tự động vào các ngày cố định.
- Hệ thống tính toán tiền lương dựa trên bảng chấm công, đơn hàng, và thông tin nhân viên.
- Sau đó, phiếu lương được gửi qua PrintService hoặc BankSystem.

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/P991ZiCW34NtdCBglXV8ObIbxJuglG0b7WqAWSWubNAsBkP8SuKnIJiDcHKIVlx-t_3p-3uaDiHZxrNgN02A2PMn70dqb1XxRR-m7JsI6eHprWqcCEmQCr7q_XW3vnDf1oP1SsJo9NXrFLf3hHvlQHQSmUjHbzYv7toS44-6pSqadAdpgIwfseHElrNgZKX3Bh16kZkx23HQgKqCs7yiDYlGEJayay1b36ekP4ByLN119eTtX5S6oExUaDXRGQy42oG2i7-FAXMaSLqiEvNn32T7QEN08IR72k1lQ2t66eeMK_fFrSNGvpt88tqwwh5Lw1F2lAKSMrPYkxLsCsklgocN2z6blf8ChNgjHAZDjglrUgLBaY9Brq7Qyf_x1G00__y30000)

## 2. Simplify Sequence Diagrams Using Subsystems
### Mô tả: 
- Gom các lớp như TimecardSubsystem và EmployeeDatabase vào BusinessServicesSubsystem.

![Biểu đồ](https://www.planttext.com/api/plantuml/png/N91D2iCW44RtdcBelXV8eeGq1v1w0ci6AZ4gCvD2pjP5ZzGhL4FeJvRwFTuJNuzdos99vYae7dq4IepAEaa4Pc71oRWR3dD0Khbmtlbiey11suLI26Q-yeeTm3BeSlp7EXj7ymKwixEGZsAGxjxXPb1gruNZQHKtOEfBOIl3POwgtjUzCmreIWwPeVU4Jg37dDZB1z4hKd9LKDnkv6qhuoxP_4RWdAOSK71GBSQX_jGR003__mC0)

## 3. Describe Persistence-Related Behavior
### Mô tả:
- Thông tin chấm công và nhân viên được lưu trong cơ sở dữ liệu.
- Kết quả tính toán phiếu lương được lưu để báo cáo.

![Biểu đồ lớp](https://www.planttext.com/api/plantuml/png/V94nQWD134NxEONAkDWBR15SE4MwW0EfjJl2E-pCo4YQm19yCXS-KgwGh1a6uiGfzVN_WozzdYzRDHGhAJgTGmPX9JT6L8NNa6X4yV3X03gmEZxlUjYRX7ouofIEaHUY6tdY8lh6CfFlmNCP8hcJg-IdcgdaEmZ5YBAqz2eDcEST6OQepTgeBxYC4urpfHxhU4F5n2NR3seYczZ_2HIESLy6NTGeNS40KdBTF6nwUEVWrqYxLjSz_axsK9JKjUB_cLgFEwO3PHAqR-UMiby_zmK00F__0m00)

## 4. Refine the Flow of Events Description
### 4.1 Basic Flow:

- Hệ thống tự động bắt đầu quy trình tính lương vào ngày đã định.
- Tải dữ liệu chấm công và thông tin nhân viên từ cơ sở dữ liệu.
- Tính toán phiếu lương dựa trên thông tin chấm công, đơn hàng, và các khoản khấu trừ.
- Gửi phiếu lương qua ngân hàng (nếu sử dụng gửi trực tiếp) hoặc in phiếu lương (nếu không).
- Kết thúc quy trình khi tất cả phiếu lương đã được xử lý.
### 4.2 Alternative Flow:

- Nếu hệ thống ngân hàng không khả dụng:
  - Hệ thống thử gửi lại giao dịch trong một khoảng thời gian.
- Nếu không thể gửi lương qua ngân hàng, hệ thống thông báo lỗi.
### Lý Do:
- Việc tinh chỉnh giúp giảm rủi ro và đảm bảo các tình huống ngoại lệ được quản lý tốt.

## 5. Unify Classes and Subsystems
### Hợp nhất các lớp và hệ thống con:
- Gom nhóm Timecard, Paycheck, và Employee thành PayrollSubsystem.
- Các lớp tích hợp (BankSystem, PrintService) được nhóm vào IntegrationSubsystem.

![Biểu đồ](https://www.planttext.com/api/plantuml/png/RCyz2W9138RXVawH4-m1B6GHBEo4yG9nDgp3_2r9LXZ4arbu9A-WRZ4MRliI7hwy7izU55dd58q4du6Ba9dG1Hm9ZbYvn6ZdirHHId0p02wY29ny8eSyjF2vTHToeOLzccAfHEPk6dZ8IYEZ-fBNq1tcO9VuOzbdjSHNxnRfRrBNRTVP3Sn2OdhAm_UxDm000F__0m00)

### Lý Do:
- Hợp nhất các lớp liên quan giúp giảm sự phức tạp và tăng khả năng tái sử dụng của hệ thống.


# Ca Sử Dụng Maintain Timecard

## 1. Describe Interaction Among Design Objects

### Mô tả:
- Nhân viên cập nhật giờ làm việc vào bảng chấm công, liên kết với thông tin dự án được lấy từ hệ thống quản lý dự án.
- Dữ liệu chấm công sau đó được lưu vào cơ sở dữ liệu.

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/V98zRiCm38LtdOB8dWjuA0B7_V7Ke4xHcRMPGeqigHHTm6Vhq2Fr2fL_KiU8qusWFZw-1-hdwtiJ15cQsgXmr1RO1L9OYcEuhRrnBP7o4T2bzcW5LdjTKubStJckLu01zjkkN8QspWexOuX7T6hC1tRitgcKeWr2TMw5tXX5EzkFxOfyJcSe-8g1-jSiLUfa5TOtevy47ZrPE1c1tkFmD42JamIUwAEX832wW4vVdIFTI7IHm3rDL6uFJiKkh2y4_n4wSvZfu0ssStenoxElK0WUNCC1NXmVgReQfi1F-ijzaI9B8n6lEo73sYnTY17hWuuxEidhCVg58zeVJMt8LjsF-WK00F__0m00)

## 2. Simplify Sequence Diagrams Using Subsystems
### Mô tả: 
- Thay vì biểu diễn từng chi tiết cho từng lớp, chúng ta nhóm các lớp liên quan vào các hệ thống con:
  - TimecardSubsystem: Gồm TimecardForm và TimecardController.
  - ProjectManagementSubsystem: Tương tác với ProjectSystemIntegration.
  - DatabaseSubsystem: Lưu trữ dữ liệu chấm công.

![Biểu đồ](https://www.planttext.com/api/plantuml/png/P91D3e9034RtSuh6FHTWOOnWuePe10zGe9fHvoSpnOIpkV18Ni516GswxVU-rwQFsttX6HrtwYByMMfmnfF0Xes3bR8NqnC96m3PI8kQOLP9HGswjkngtticDGFqK6Nb5DiwSwA62zHu94MQf_os-E5pPApHqnJBbwKGyGv8viEU53QMDCGxH1WDIJ2ci2Dsagu4uteOj294aCJo9FbJxssBJB0sdVFH78v8eSHW_UmCewynC_eWdNeXxqv8edbiZWooD5eiIBV3mvy0003__mC0)

## 3. Describe Persistence-Related Behavior
### Mô tả:
- DatabaseSubsystem xử lý lưu trữ dữ liệu liên quan đến Timecard và Project.
- Dữ liệu được ánh xạ từ đối tượng Timecard vào các bảng TimecardRecords và ProjectRecords.
- DatabaseSubsystem sử dụng phương thức storeTimecard() để lưu dữ liệu chấm công.

![Biểu đồ lớp](https://www.planttext.com/api/plantuml/png/R50x3i8m3Drp2eymz08PK8SkB0W99EQqiThIf45sKWaXJiR0aRW2_OCeYoM_Px_dvzVZ6RDNv8CrWgko1dAC8ZEA6OwbnKoHXfi0YC2FxJQHSF1KrdaFexqOTqNyWRNoA25fQzyMBX2V75Me9MWNKZFW5t9dpFpNybsCzlk16jsNWnsQ5Ofot0MR8YqLMdULAiPU0e2z8vn2hQOuSiwvbj2uKdVxS_Gesdna9B1gK4o7_UDYh7NtopS0003__mC0)

## 4. Refine the Flow of Events Description
### 4.1 Basic Flow:

- Nhân viên mở giao diện bảng chấm công.
- Hệ thống hiển thị danh sách các dự án và mã chi phí liên quan từ hệ thống quản lý dự án.
- Nhân viên chọn mã dự án và nhập số giờ làm việc.
- Hệ thống lưu dữ liệu chấm công vào cơ sở dữ liệu và hiển thị thông báo thành công.
### 4.2 Alternative Flow:

- Nếu danh sách dự án không khả dụng:
  - Hệ thống hiển thị thông báo lỗi và cho phép nhân viên nhập lại giờ làm việc cho mã dự án đã tồn tại.
- Nếu thông tin nhập vào không hợp lệ (ví dụ: số giờ vượt quá 24 giờ/ngày):
  - Hệ thống hiển thị thông báo lỗi và yêu cầu nhân viên nhập lại dữ liệu hợp lệ.
- Nhân viên có thể chọn hủy thao tác và quay lại giao diện chính.
### Lý Do:
- Việc tinh chỉnh các bước luồng sự kiện đảm bảo rằng tất cả các trường hợp ngoại lệ và các tình huống không mong muốn được xử lý đầy đủ, tránh sai sót trong quy trình.

## 5. Unify Classes and Subsystems
### Hợp nhất các lớp và hệ thống con:
- TimecardSubsystem:

  - Bao gồm các thành phần:
    - TimecardForm: Giao diện người dùng để nhập và chỉnh sửa thông tin chấm công.
    - TimecardController: Xử lý logic liên quan đến quản lý chấm công.
    - Database: Lưu trữ dữ liệu chấm công.
  - Mục tiêu: Nhóm các thành phần liên quan chặt chẽ để tối ưu hóa việc quản lý.
- ProjectManagementSubsystem:

  - Bao gồm các thành phần:
    - ProjectSystemIntegration: Lấy thông tin về mã dự án từ hệ thống quản lý dự án bên ngoài.
  - Mục tiêu: Đảm bảo tích hợp dễ dàng và tách biệt rõ ràng giữa hệ thống nội bộ và các hệ thống bên ngoài.
![Biểu đồ](https://www.planttext.com/api/plantuml/png/V9112i9034NtSugSm0Eua88Yk124Ue5q6ihOcKn9Ka74axdmI5x1LgMRYily_tdv_EVzKQYXM9-YqpOmI5Po7VeM6u9ZIEHHwhAlzA962QuEm4TKdRnjbZGJrvbDSemaaxL1mme7-CrD_8Fa4tdR8mzN8hPVZxwXygtlsAWHj91v1CqBBXQhVzWb29a4EfD2zub1FJHp1N4zZl02003__mC0)

### Lý Do:
- Việc nhóm các thành phần vào các hệ thống con giúp giảm sự phức tạp trong thiết kế, tăng khả năng tái sử dụng và mở rộng, đồng thời đảm bảo phân tách trách nhiệm rõ ràng.

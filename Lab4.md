# Ca sử dụng Login
## Mô tả ca sử dụng:
  ### Actor: Employee, PayrollAdministrator.
  ### Mục đích: Xác thực người dùng để truy cập vào hệ thống.
  ### Luồng chính:
    1. Người dùng mở giao diện đăng nhập.
    2. Người dùng nhập tên đăng nhập và mật khẩu.
    3. Hệ thống gửi thông tin đăng nhập đến SecuritySubsystem để xác thực.
    4. Nếu xác thực thành công, hệ thống chuyển đến giao diện chính.
    5. Nếu không thành công, thông báo lỗi được hiển thị.
## Các lớp tham gia:
  - Boundary Class: LoginForm
  - Control Class: LoginController
  - Entity Class: User, SecuritySubsystem
## Biểu đồ tuần tự:

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aK9eSMeHLr9-QLvAOb6bWaz-UcQUMtvHBbToVbv9KNuEHCGPmia1AatDAyaigLG8JaqkBG8oWakJYYkBIr9pkRX09YdesY7Ci5BmotYuQss1Gad6uIrvwGebcNaAHoOUQGOoyy0IN72bS7q8cwmKt1_kNfj9G3D2FSW835TPAKGSNfWCDEFXxet9I4PnOQXKqCNcX92YXxiMAsG_tBM_HA6m5CIkG9Y7wG9KttjaFjpTd0TMt8rYXaP8nk45UHaAoI3dw8S0lREqH27fuQw5cPfS3gbvAQ3O0G000F__0m00)

# Ca sử dụng Maintain Timecard
## Mô tả ca sử dụng:
### Actor: Employee.
  ### Mục đích: Nhân viên cập nhật giờ làm việc của mình vào hệ thống.
  ### Luồng chính:
  1. Nhân viên mở giao diện thẻ chấm công (TimecardForm).
  2. Nhân viên nhập số giờ làm việc và mã dự án (nếu có).
  3. TimecardForm gửi thông tin tới TimecardController.
  4. TimecardController lưu thông tin vào Timecard.
  5. TimecardController có thể yêu cầu thông tin dự án từ ProjectManagementDatabase nếu cần.
  6. Sau khi lưu, thông báo thành công sẽ được hiển thị.
## Các lớp tham gia:
  - Boundary Class: TimecardForm
  - Control Class: TimecardController
  - Entity Class: Timecard, ProjectManagementDatabase
## Biểu đồ tuần tự:

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/V94xJiGm48Pxds9AABX02hGIpm8G1HTm72iniiShxsIbr1GKd04fAuIeLWA9AYwsiCGzV0AkW2C82OAbiVpFuvj_x7U_cIs8EwgDPboGTN1avjesKhBSrbXmry2LCb9mLnnRPvYmICxgx-31fzRICOcaQ2mVzAMprrBGEKTUIfE2XvnupXUIiM4MxEt_c9B1HHMxzHnA5VqzwD0QMARhhM3JicdRw2E3a-ZN2gWAhrW2AVm7CxPDOHcSlJtNKy8oj3Rfs7aGwNmq8FhS5ixMbHCuDJTWmWCKqRz0M27iOEmsDOZOFU7kdyHVptEQjhZ1tf2_6spcOTLR32rMN-Pc4el-Opy0003__mC0)

# Ca sử dụng Run Payroll
## Mô tả ca sử dụng:
### Actor: PayrollAdministrator.
  ### Mục đích: ính toán và xử lý lương cho nhân viên.
  ### Luồng chính:
  1. Quản trị viên khởi động quy trình tính lương.
  2. Hệ thống thu thập dữ liệu từ Timecard và EmployeeDatabase.
  3. PayrollController tính lương thông qua Payroll.
  4. Kết quả được gửi đến BankSystem hoặc PrintService để xử lý thanh toán hoặc in phiếu lương.
## Các lớp tham gia:
  - Boundary Class: PayrollUI.
  - Control Class: PayrollController.
  - Entity Class:Employee, Timecard, Payroll, BankSystem, PrintService.
## Biểu đồ tuần tự:

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/Z5BDIiD04BxlKymBz0LoaFg753q8hU1rcopDqisaRYR5F85dZvwaYWY5eWTF2TB3IjzZdy1NS8FTf9G8tcQ-dM_c-sRskrhtC-AQyaGn7bAguP8NEbNgC4eaoemqTo0Rfpb6N1V-zMh0mXJ9XHuv_asLq4mWIIhWD9cfj13YX1CVyqnuV2GJ4N8T-NpRmAT77AV38YEHD0LQ8Ws5dijGCDQb3te7hR80pcDRFKhukhVL0qxWrbOhKEOJrEPziy09QqftUAt-0CuSGK9XbZc4jdpDWSmAutrwowZRxBiDuCAMBmLGR3wS1f8869idXBaqI-pkuJVZkP6jta19Mzqv8R634WZhRjtiBHZ0g4ijzBgzZhGjds5gopN1JLx7_p3RtYY0QxzTYhdZKMeMVzZRlMC00uHPBDtSl9dL5nZL7_47003__mC0)

# Lý do thiết kế:
  1. Tính mô-đun và phân tách rõ ràng: Các lớp được phân chia theo nguyên lý SOLID, tách biệt rõ ràng giữa giao diện, điều khiển và xử lý dữ liệu, giúp hệ thống dễ mở rộng và bảo trì.
  2. Tính tái sử dụng cao: Các lớp Controller có thể dễ dàng tái sử dụng trong các tính năng khác, ví dụ, PayrollController có thể xử lý các yêu cầu thanh toán cho các hệ thống khác nhau (chuyển khoản, in phiếu lương).
  3. Quản lý lỗi tốt: Các luồng thay thế (ví dụ: thông báo lỗi khi xác thực không thành công) giúp xử lý các tình huống không mong muốn hiệu quả. 

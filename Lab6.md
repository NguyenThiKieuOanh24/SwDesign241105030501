# 1. Xác định các Operations
## Lớp LoginController
- Mô tả: Quản lý đăng nhập, đăng xuất.
- Operations:
  + login(username: String, password: String): Xác thực người dùng.
  + logout(): Kết thúc phiên làm việc.
## Lớp User
- Mô tả: Đại diện cho người dùng trong hệ thống.
- Operations:
  + authenticate(password: String): boolean :Kiểm tra tính hợp lệ của mật khẩu.
## Lớp TimecardController
- Mô tả: Quản lý thông tin chấm công.
- Operations:
  + addTimecard(employeeId: String, date: Date, hoursWorked: Float): Thêm thông tin chấm công mới.
  + updateTimecard(timecardId: String, hoursWorked: Float): Cập nhật số giờ làm việc.
  + viewTimecards(employeeId: String): Lấy danh sách các thẻ chấm công của một nhân viên.
## Lớp PayrollController
- Mô tả: Điều phối quá trình tính lương.
- Operations:
  + runPayroll(): Thực hiện tính lương cho tất cả nhân viên.
  + calculatePay(employee: Employee): Tính toán số tiền lương của một nhân viên.
## Lớp Paycheck
- Mô tả: Đại diện cho phiếu lương.
- Operations:
  + createPaycheck(employeeId: String, amount: Float): Tạo phiếu lương mới.
## Lớp BankTransaction
- Mô tả: Xử lý giao dịch ngân hàng.
- Operations:
  + processTransaction(employeeId: String, amount: Float): Thực hiện giao dịch chuyển tiền lương.
# 2. Xác định các trạng thái
## Lớp User
- Trạng thái:
  + LoggedOut: Người dùng chưa đăng nhập.
  + LoggedIn: Người dùng đã đăng nhập.
- Biểu đồ trạng thái:

  [].(https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWaz-UdfgYdzf2HUSXIJkcQTWfP2JdvwPfw49LU2PXweFeY2_j4H3ayiXDIy5P3W0003__mC0)

 ## Lớp Timecard
- Trạng thái:
  + Created: Thẻ chấm công mới được tạo.
  + Updated: Thẻ chấm công được cập nhật.
- Biểu đồ trạng thái:

[].(https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdDHQc99QWeNb0QBXHQaWDbM2gLWbaT-QL6nXYQNGsfU2aWl0000__y30000)

## Lớp Paycheck
- Trạng thái:
  + Generated: Phiếu lương được tạo.
  + Processed: Phiếu lương đã được gửi qua ngân hàng hoặc in.
- Biểu đồ trạng thái:

[].(https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdjgNcfHOabg2XUS1HOFACfFJYqkJarHi58eWB0rDBaSKlDIGBe10000__y30000)

# 3. Xác định các thuộc tính
## Lớp User
- Thuộc tính:
  + userId: String
  + username: String
  + passwordHash: String
  + role: String
## Lớp Timecard
- Thuộc tính:
  + timecardId: String
  + employeeId: String
  + date: Date
  + hoursWorked: Float
## Lớp Paycheck
- Thuộc tính:
  + paycheckId: String
  + employeeId: String
  + amount: Float
## Lớp BankTransaction
- Thuộc tính:
  + transactionId: String
  + employeeId: String
  + amount: Float
# 4. Xác định các phụ thuộc và quan hệ kết hợp
- Phụ thuộc:
  + LoginController: phụ thuộc vào User để xác thực thông tin đăng nhập.
  + TimecardController: phụ thuộc vào Timecard và Employee để thêm và quản lý dữ liệu chấm công.
  + PayrollController: phụ thuộc vào Paycheck và BankTransaction để thực hiện thanh toán.
- Quan hệ kết hợp:
  + User - Session: Một người dùng có thể có một phiên làm việc.
  + Employee - Timecard: Một nhân viên có thể có nhiều thẻ chấm công.
  + Employee - Paycheck: Một nhân viên có thể nhận nhiều phiếu lương.
  + Paycheck - BankTransaction: Một phiếu lương có thể dẫn đến một giao dịch ngân hàng.
5. Biểu đồ lớp chi tiết với các phụ thuộc và quan hệ kết hợp

[].(https://www.planttext.com/plantuml/png/f5HBQiCm4Dtx58DNCIGNqAA4afPqLqXArrDvY4LioMZ6AQ7qP5tqIBr2SIBBZkD2e4k_UVFcpKV--VfUig2NfYeJNI8pl31v-4W001RGCFcdNC56lB6x0MYneX5S8_Exy_aQkHY5l2ilsG3OI45MZ4QXMPVQSJ85RywLX3RvJ8Al3J4RPwCrFdzFkbEdBa8bxGc5Glgi3sUgqmn48LyPE-1c2WxEvBs7hQb8ey-Z2Gd0bGkgwj8TYQu2EGefMA5G00hNU7vrVa-vWiVIeLpuxahEhXNd0x7vX4wcek4WsTHjnhfbpYRvb-q-X9AntJ-xcZe7nqQCiwEzxqWwsHK9cfBRCGTAhFoCHrsGtiVATG1k7pHMhh4oDT9EV7Aa5scPYavwR_TezrkFbb6t_VMtq6F_SrbxfubvKECcfuCNSth3YyLTV3GAqW8vJU96ss2yvdCKAhJ74INkGK7gIPCv4AT9H5lAU1mAKl5cjoFFQR8acxU_bby0003__mC0)

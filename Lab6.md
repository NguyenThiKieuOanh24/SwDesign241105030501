# 1. Xác định các Operations
## Lớp LoginManager
- Mô tả: Quản lý yêu cầu đăng nhập và đăng xuất từ người dùng.
- Operations:
  + signIn(username: String, password: String): Kiểm tra thông tin đăng nhập của người dùng.
  + signOut(sessionId: String): Kết thúc phiên làm việc.
## Lớp Authentication
- Mô tả: Xử lý xác thực thông tin người dùng.
- Operations:
  + validateCredentials(username: String, password: String): Xác minh thông tin đăng nhập.
## Lớp AttendanceManager
- Mô tả: Quản lý việc chấm công và sửa thông tin chấm công.
- Operations:
  + recordTime(employeeId: String, date: Date, hoursWorked: Float): Ghi nhận giờ làm việc.
  + editTimecard(timecardId: String, hoursWorked: Float): Chỉnh sửa thông tin giờ làm việc.
  + retrieveTimecards(employeeId: String): Lấy danh sách chấm công của một nhân viên.
## Lớp PayrollProcessor
- Mô tả: Điều phối quy trình tính lương.
- Operations:
  + initiatePayroll(): Bắt đầu quy trình trả lương.
  + computeSalary(employee: Staff): Tính số tiền lương dựa trên thông tin nhân viên.
# 2. Xác định các trạng thái
## Lớp Authentication
- Trạng thái:
  + Idle: Không có hoạt động.
  + Authenticating: Đang xử lý xác thực thông tin.
  + Authenticated: Xác thực thành công.
- Biểu đồ trạng thái:

![](https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWcTAJYeNY03p74jBCbBpIZAJ4qioyz8Lh1IACzFpFFCqDBdGPD0KfwQ0r9Oc9wSM5sDJ2hR0IY4jCJEdj2WLMKLg2h82a7N-fIKQcbmEgNaf87S20000__y30000)
## Lớp AttendanceRecord
- Trạng thái:
  + New: Bản ghi mới được tạo.
  + Modified: Bản ghi được chỉnh sửa.
- Biểu đồ trạng thái:
    
![](https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWbzgEPTVQZcOxPkVafcMcPgYOAMGcf9P4fAPcvgSM9IYeSdba9gN0j850000__y30000)
## Lớp SalaryPayment
- Trạng thái:
  + Pending: Lương đang chờ xử lý.
  + Completed: Lương đã được xử lý.
- Biểu đồ trạng thái:
  
  ![](https://www.planttext.com/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTGa1gNafcNZeNb0QBEUVd5kIabgIcA5Wf51Jb9wSM5mSaLkQcvfLeQ78vfEQbW0m00000__y30000)
# 3. Xác định các thuộc tính
## Lớp Staff
  + staffId: String
  + fullName: String
  + role: String
  + hourlyRate: Float
## Lớp AttendanceRecord
  + recordId: String
  + employeeId: String
  + workDate: Date
  + hoursWorked: Float
## Lớp SalaryPayment
  + paymentId: String
  + employeeId: String
  + amount: Float
## Lớp BankService
  + transactionId: String
  + bankAccount: String
  + paymentAmount: Float
# 4. Xác định các phụ thuộc và quan hệ kết hợp
- Phụ thuộc:
  + LoginManager: phụ thuộc vào Authentication để kiểm tra thông tin người dùng.
  + AttendanceManager: phụ thuộc vào AttendanceRecord để lưu trữ thông tin chấm công.
  + PayrollProcessor: phụ thuộc vào SalaryPayment để xử lý phiếu lương.
- Quan hệ kết hợp:
  + Staff - AttendanceRecord: Một nhân viên có thể có nhiều bản ghi chấm công.
  + Staff - SalaryPayment: Một nhân viên có thể nhận nhiều phiếu lương.
  + SalaryPayment - BankService: Một phiếu lương có thể dẫn đến một giao dịch ngân hàng.
5. Biểu đồ lớp với các phụ thuộc và quan hệ kết hợp

  ![](https://www.planttext.com/plantuml/png/b9HDZjim38NtFeNWbGCa5_1YC6a70mpGJeF9eckEJ3j2PCeWwGoCeYVheaVg5GexYd-IB5el38Yat_j4KVxpw_UZAB2sjK-i1n7p9LIElW91XMn-96Pun5NqGbaho0GrvcQlxAXQcmP4FW8NbyWgD-yXU0IQVVcjrKnGn0LwcLUUWYkIdqaqthPwG59dGLsWqVe4tXMW-9cnwDFWvVyuHeEzGbb6tOsHVZNXn6ZPUlywKuvX3luwT0Wj--uD57Fpx0DevArGdr31USbMuoVJ9bMH2Y2BRsW35oCE3yiR7gmR7ph4cyH7uEFJODw_PqpoFV0HYoMKPGIDbjcjvlfARdr7QPNVm4_Rsa77mViT1uiYOHeSHquTACQ2x7Bg4IlKJQku1m_SZLmz5PJbwhA5wG27kXrqDPAEdMlEwtzl7TIX9Lqsg3cJH-titlXy0ZhkaK_EukYj32HW-u6ziNa7EcwjFNijCf5uUuTZ42oHdrigXW6QOInkvcRpS7rZSfF25459a_F43wNNSvURz01YQg1kNhTiSMvIHelkD8WjKdtnl2EvIIzdBMdoY5JqlvI_0000__y30000)

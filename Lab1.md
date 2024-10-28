1. Phân tích kiến trúc
* Đề xuất kiến trúc:
  - User Interface (UI): Giao diện cho người dùng tương tác với hệ thống, nơi người dùng nhập thông tin và nhận kết quả.
  - Business Logic Layer: Xử lý các quy tắc và nghiệp vụ liên quan đến thanh toán tiền lương, và quản lý thông tin thời gian.
  - Data Access Layer : Quản lý các hoạt động liên quan đến cơ sở dữ liệu, bao gồm việc lưu trữ và truy xuất thông tin.
* Giải thích lý do lựa chọn: 
  - Dễ bảo trì: Kiến trúc 3 lớp tách biệt các thành phần, giúp việc bảo trì và mở rộng hệ thống trở nên dễ dàng hơn.
  - Khả năng mở rộng: Hệ thống có thể dễ dàng mở rộng khi cần thêm chức năng mới mà không làm ảnh hưởng đến các thành phần khác.
  - Bảo mật: Tách biệt các lớp giúp bảo vệ thông tin nhạy cảm và giảm thiểu rủi ro từ các cuộc tấn công.
* Ý nghĩa từng thành phần:
  - User Interface (UI): Cung cấp giao diện cho nhân viên và quản lý để thực hiện các chức năng như xem báo cáo thanh toán và quản lý thời gian.
  - Business Logic Layer: Chứa các quy tắc tính lương, kiểm tra thời gian làm việc của nhân viên, và xử lý các thông tin cần thiết để tính toán tiền lương.
  - Data Access Layer: Chịu trách nhiệm lưu trữ và truy xuất dữ liệu từ cơ sở dữ liệu, đảm bảo tính toàn vẹn và chính xác của dữ liệu.
* Biểu đồ package:
  
  ![](https://www.planttext.com/api/plantuml/png/X5DBJiCm4Dtd55PNiEWLK86oG2fIHU40WpD45evjZIULBDIJiU18N04x7xNDK36BMUIzpBpt9ldv-bv51kAkjLK0_G4DgiKM4dbhrIv5ndQXFYkLwmWJHdGCRBnJ6qX84wMKjX2ZUer8ZuwHta7Z2JfKRMAma9unUE9uTJs3ZGiTlvWMxu7g4_HG3VrSpbqNZSEyS-CReoy96ZrjoUlCzIGqQR2wiy2u0mkKXAWzM5Dd-AAkuww7DbYVKFfkaDV8OApqt8KoNABpsTb7cyCNeyDWR8J5-0OTKbumHFvlfcjWKBTQzx7-7MYXl4749t3v5PbdX3qMZf12o6HGW9EGqljs_WajbpVYXZrD7BOmfmjSPen1JOG-q_9yPgiwL2jqTVazVW400F__0m00)
  
2. Cơ chế phân tích
  * Persistency: Lưu trữ thông tin bảng chấm công, phương thức thanh toán và lương vào cơ sở dữ liệu.
  * Transaction Management: Đảm bảo tính nhất quán dữ liệu khi ghi nhận thanh toán.
  * Security: Đảm bảo rằng chỉ những nhân viên được phân quyền mới có thể thay đổi thông tin bảng chấm công hoặc nhận thanh toán.
  * Error Handling: Quản lý các lỗi phát sinh khi giao dịch không thành công.
  * Authentication and Authorization: Xác thực và phân quyền cho các thao tác khác nhau, ví dụ: chỉ quản lý có thể duyệt và sửa đổi phương thức thanh toán.
    
3. Phân tích ca sử dụng Payment
  * Các lớp phân tích cho ca sử dụng Payment
    - Boundary Class: PaymentUI
      + Mô tả: Quản lý giao diện người dùng cho việc thực hiện thanh toán.
      + Nhiệm vụ: Thu thập thông tin thanh toán từ khách hàng và hiển thị kết quả thanh toán.
      + Các phương thức chính:
         - getPaymentInfo(): Thu thập thông tin thanh toán từ người dùng.
         - displayPaymentResult(): Hiển thị kết quả thanh toán.
    
    - Control Class: PaymentController
      + Mô tả: Xử lý logic thanh toán.
      + Nhiệm vụ: Điều phối các bước thực hiện thanh toán và tương tác giữa các lớp khác.
      + Các phương thức chính:
          - processPayment(): Điều phối quá trình thanh toán, gọi các phương thức cần thiết từ lớp Payment và Order.
        
    - Entity Class: Payment
      + Mô tả: Lớp này đại diện cho thông tin thanh toán.
      + Nhiệm vụ: Lưu trữ thông tin thanh toán, chẳng hạn như số tiền, phương thức thanh toán và trạng thái thanh toán.
      + Các thuộc tính:
          - amount: Số tiền thanh toán.
          - method: Phương thức thanh toán.
          - status: Trạng thái của thanh toán (ví dụ: thành công, thất bại).
      + Phương thức chính:
          - updateStatus(): Cập nhật trạng thái thanh toán.
          - savePaymentInfo(): Lưu thông tin thanh toán.
    
    - Entity Class: Order
      + Mô tả: Lớp này đại diện cho đơn hàng mà khách hàng đang thanh toán.
      + Nhiệm vụ: Lưu trữ thông tin chi tiết của đơn hàng.
      + Các thuộc tính:
          - orderID: ID của đơn hàng.
          - totalAmount: Tổng số tiền của đơn hàng.
          - items: Danh sách các mặt hàng trong đơn hàng.
      + Phương thức chính:
          - getOrderDetails(): Lấy thông tin chi tiết của đơn hàng.
        
  * Biểu đồ sequence
    
![](https://www.planttext.com/api/plantuml/png/UhzxVq1YPMvgNacefuAkdGAKuvoVLrAKdvEJMgHWfP2UMW8LzinBozVGvC9K1DJfNvG2KmrckgIM96Rc5EDI3XK4QYWeoazEBIw62Y3Kut9EQK5AOabgS4bYIIaXqu5-ib98oImko4ciX0e5fHQNve1i0G000F__0m00)
    
  * Nhiệm vụ của từng lớp phân tích
    - PaymentUI: Nhận đầu vào từ người dùng và hiển thị kết quả thanh toán.
    - PaymentController: Điều phối toàn bộ quá trình thanh toán và tương tác với các lớp Payment và Order.
    - Payment: Lưu trữ và cập nhật thông tin thanh toán.
    - Order: Cung cấp thông tin về đơn hàng.
  * Một số thuộc tính và quan hệ giữa các lớp phân tích
    - Payment và Order có mối quan hệ một-nhiều: Một Order có thể chứa nhiều Payment cho các đơn hàng lớn thanh toán từng phần.
    - PaymentController đóng vai trò như trung gian, quản lý quá trình thanh toán giữa các lớp.
      
  * các biểu đồ lớp
    
![](https://www.planttext.com/api/plantuml/png/T591JiCm4Bpx5Nk4GpuGeQg8NY8XKL7n01DlMqksD_AkWoh4opZm9Bw0qrf9MrBVTcPsFRFsx_VFaaL7ITwfrcbcMEk3no1l3NmgoAU27Ke1cx2bktkeeITh2ciiTquVYk8LEJcPD5_gSkmJ1Oda7CPnV1UfHUOYkDqwDcXFAPSr64hl3WlgKVPaChgHQCEke3cS9Bv6KsUquER8NUTXtUDitD7FIpHdzccecbLMsI054nBj7cTjMa4_-7csB0zDBXRJbe-3LoZQEhwuTtgJgbhChBA6nCZgFt4cFnd4g5jX-B2olo4_fQiXOjuOziYvRKkmZUILMc8mmrVv0m00__y30000)

    * Giải thích:
    - PaymentUI kết nối với PaymentController để điều phối thông tin đầu vào và hiển thị kết quả.
    - PaymentController điều phối thông tin thanh toán giữa Payment và Order.
    - Order lưu giữ thông tin chi tiết về đơn hàng và được PaymentController gọi để lấy thông tin khi cần thiết.
    
4. Phân tích ca sử dụng Maintain Timecard
   
   * Các lớp phân tích cho ca sử dụng Maintain Timecard
    - Boundary Class: TimecardUI
      + Mô tả: Quản lý giao diện người dùng để nhập và hiển thị thông tin bảng chấm công.
      + Nhiệm vụ: Nhận dữ liệu chấm công từ người dùng và hiển thị kết quả lưu trữ hoặc cập nhật thông tin.
        
    - Control Class: PaymentController
      + Mô tả:  Xử lý logic nghiệp vụ cho quy trình duy trì bảng chấm công.
      + Nhiệm vụ: Điều phối quá trình nhập, chỉnh sửa và lưu thông tin chấm công; xử lý các yêu cầu từ TimecardUI và tương tác với lớp Employee và Timecard.
      
    - Entity Class: Timecard
      + Mô tả: Đại diện cho bảng chấm công của một nhân viên.
      + Nhiệm vụ:  Lưu trữ dữ liệu chấm công, bao gồm ngày làm việc, số giờ làm, và trạng thái (xác nhận hoặc chờ xác nhận).
    
    - Entity Class: Employee
      + Mô tả: Đại diện cho thông tin nhân viên.
      + Nhiệm vụ: Lưu giữ thông tin cơ bản của nhân viên (ID, tên, chức vụ) để tham chiếu khi lưu trữ chấm công.
      
  * Biểu đồ sequence
    
    ![](https://www.planttext.com/api/plantuml/png/X90z3i8m38Ntd28Z3Br01rG965Y1ifl6I97oKpbEfPwDWIDn1HBKeYmHYuVdz_az-VryTO61E5eZO61FiWz8GkGfcvsyQei3aEfFifNe66bL3i2msOh2KDZttZ5vOzAHLePujvehNE5C_D6Eni-8YPgGz6DUXKJyTaqj21V7BQCQLJLcLNCvcB1IhHx4YtX9yF-Kx--K3gE1EHDd3D5mmaI7JkNFVm000F__0m00)
    
  * Nhiệm vụ của từng lớp phân tích
    -TimecardUI: Nhận dữ liệu từ người dùng và gửi đến TimecardController để xử lý. Sau khi xử lý xong, TimecardUI hiển thị kết quả cho người dùng.
    - TimecardController: Làm trung gian điều phối các yêu cầu từ TimecardUI, bao gồm xác minh nhân viên và lưu trữ dữ liệu chấm công vào Timecard.
    - Timecard: Lưu trữ chi tiết chấm công và trả lại kết quả cho TimecardController.
    - Employee: Xác minh danh tính nhân viên dựa trên ID được nhập từ TimecardController.
      
  * Một số thuộc tính và quan hệ giữa các lớp phân tích
    - TimecardUI:
      + Phương thức: enterTimecardData(), displaySaveResult()
    - TimecardController:
      + Phương thức: submitTimecardData(), verifyEmployee(), saveTimecardData()
    - Timecard:
      + Thuộc tính: date, hoursWorked, status
      + Phương thức: saveTimecardData()
    - Employee:
      + Thuộc tính: employeeID, name, position
      + Phương thức: verifyEmployee()
  * các biểu đồ lớp
    
![](https://www.planttext.com/api/plantuml/png/Z59BJiCm4Dtx55xIHIwG1Qf4MNHBGQoTUA0ZR4_a6GT55ITZmP6u0eOwQHLIX9VlCs_yxC_tZpMBYPAyKwqppFeUFRGcseUjFYYTJwKX2CGHtnWnLojTwvxG5e55xfmPTgQ7E-3av2HuKxEvDnGaadCGf_cS6e_oLq0F4P-6Mzyv6W1-s8R8ZVwSk-p-bJvbMYEGLLaE1TbJYln8yGLi9YobnerKhaWIPtGd4SFp_sF7ZKzL5c2xoLeCKk1WFCp7TyGeI66EN-eYXvwzNLLTBrLUwyJ0Qe4vDnntWsXQOVsAihzacEvN7zT2A7grXc2_FzKN0000__y30000)

  * Giải thích:
    - TimecardUI:
      +  Là lớp giao diện người dùng, có nhiệm vụ nhận dữ liệu từ người dùng và hiển thị kết quả lưu trữ.
      + Phương thức chính là enterTimecardData() để nhập thông tin chấm công và displaySaveResult() để hiển thị kết quả.
    - TimecardController:
      + Là lớp điều khiển xử lý logic cho việc duy trì bảng chấm công.
      + Nó tương tác với Timecard và Employee để xác minh nhân viên và lưu dữ liệu chấm công.
      + Các phương thức quan trọng gồm submitTimecardData() để xử lý dữ liệu từ UI, verifyEmployee() để xác minh danh tính nhân viên, và saveTimecardData() để lưu thông tin chấm công.
    - Timecard:
      + Là lớp thực thể đại diện cho bảng chấm công của một nhân viên.
      + Nó lưu trữ các thuộc tính như date (ngày), hoursWorked (số giờ làm việc), và status (trạng thái chấm công).
      + Phương thức saveTimecardData() dùng để lưu thông tin chấm công vào cơ sở dữ liệu.
    - Employee:
      + Đại diện cho thông tin nhân viên, bao gồm employeeID, name, và position.
      + Phương thức verifyEmployee() dùng để xác minh nhân viên dựa trên ID.
    - Mối Quan Hệ
      + TimecardUI sử dụng TimecardController để truyền dữ liệu.
      + TimecardController tương tác với Timecard để lưu trữ thông tin chấm công.
      + TimecardController cũng xác minh thông tin với Employee.
5. Hợp nhất kết quả phân tích
  * Kiến trúc hệ thống
    - Hệ thống "Payroll System" được thiết kế với cấu trúc kiến trúc theo mô hình 3 lớp (Three-tier Architecture), bao gồm:
      + Presentation Layer (Lớp giao diện): Chịu trách nhiệm tương tác với người dùng qua các lớp như PaymentUI và TimecardUI.
      + Business Logic Layer (Lớp logic nghiệp vụ): Chứa các lớp điều khiển như PaymentController và TimecardController để xử lý các nghiệp vụ thanh toán và quản lý bảng chấm công.
      + Data Layer (Lớp dữ liệu): Lưu trữ và quản lý dữ liệu trong các lớp thực thể như Payment, Order, và Timecard.
  * Biểu đồ package mô tả kiến trúc:

    ![](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWb90KMfnQbv9OabcVfw2Js9bQf6IGZMNWa9qG69bBb0Yr3CMn0l9p4rDJYnA0N5hkH3QdKgBC_DIYuiLVFBJCvEn6U2SdrTIb9-Jarg4OX2oCBA1BeabYTYC0MlsBqf1CmRCSSqjoCclJ4q5cUIGcfS2yY00003__mC0)
    
  * Biểu đồ lớp:

![](https://www.planttext.com/api/plantuml/png/X9GxJiD048PxdsAK1YXy0GkXI8I22aI2g3VUmLbb7zO-8bae9w7A2Q1FGO6KU-G4N86rMJ_YEC6Lzv_PVsQ_MVjd-pKsbcZh18zoaYv9XZ1w98L0QM5Q68jY16yHGCg9CH0Yp_ULLZv-XJh84xI4SNDv5MAKcPoJ8aIVq3Xkg-0wwZlUAccruXnruvnhbQ8n8Q4nNH7EAB7OrO_zWaiCH2WdRG9KkJd780gq2qKJc5hDP1P4py4wSo026B8wLUb1qwRR65IvkfyamAGD4lFm0fAEwpho7Wtg6HEO4aq7MDUXFknQdn1B-gYdljrXplMk0T36pGMpWxOhrEork1CvLmNYASy6GZcN1Bn33NgXd3OlIY-HzaPmalPH7vs2TIDDGGp28NX91FQS1m_YdIzWjllSRMG6zdkJGiRssmy2QVdEzzltF3g-dt5yqtu72JY3vdpMsPpg5YL__J6V5GqCginhRqEm-oVlV5ODebkuXo9TE4zlOFzrvsYjd42g_3V0f1z-M_OWsRUKqoeyHadBFyul0000__y30000)

  * Biểu đồ tuần tự:
    
![](https://www.planttext.com/api/plantuml/png/X99D3i8W48Ntd8AbBhn05yP4NRZI67i0qexQX48pJ6CycmkFv1KioFJ7sBeX3FFUyFZ2w_5SEL98TQc5oiYYJ1sW47wLYwKyg7i9Xj9T8WjJrHJhdJdRsLoqtPvqRGsXrHemaHNQ39oBdSxGQNh6H5w0vs-0LA7Tc6EFkH_VwCDkc6Oa2mBLQ6GLHVdd1X46J5jia1JD9PFvFIDtjRTO7i7Lsh-vPNagIiWKvYrCFeZvktvV_OCdjtgUOI8-3OYuw9Z-DctBIjixG31nyHLjB5WaHInZkZpcZmzO5Y1FluanSzroNe79_JT-0m00__y30000)




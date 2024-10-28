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
          getPaymentInfo(): Thu thập thông tin thanh toán từ người dùng.
          displayPaymentResult(): Hiển thị kết quả thanh toán.
    
    - Control Class: PaymentController
      + Mô tả: Xử lý logic thanh toán.
      + Nhiệm vụ: Điều phối các bước thực hiện thanh toán và tương tác giữa các lớp khác.
      + Các phương thức chính:
             processPayment(): Điều phối quá trình thanh toán, gọi các phương thức cần thiết từ lớp Payment và Order.
        
    - Entity Class: Payment
      + Mô tả: Lớp này đại diện cho thông tin thanh toán.
      + Nhiệm vụ: Lưu trữ thông tin thanh toán, chẳng hạn như số tiền, phương thức thanh toán và trạng thái thanh toán.
      + Các thuộc tính:
          amount: Số tiền thanh toán.
          method: Phương thức thanh toán.
          status: Trạng thái của thanh toán (ví dụ: thành công, thất bại).
      + Phương thức chính:
          updateStatus(): Cập nhật trạng thái thanh toán.
          savePaymentInfo(): Lưu thông tin thanh toán.
    
    - Entity Class: Order
      + Mô tả: Lớp này đại diện cho đơn hàng mà khách hàng đang thanh toán.
      + Nhiệm vụ: Lưu trữ thông tin chi tiết của đơn hàng.
      + Các thuộc tính:
          orderID: ID của đơn hàng.
          totalAmount: Tổng số tiền của đơn hàng.
          items: Danh sách các mặt hàng trong đơn hàng.
      + Phương thức chính:
          getOrderDetails(): Lấy thông tin chi tiết của đơn hàng.
        
  * Biểu đồ sequence
    ![](https://www.planttext.com/api/plantuml/png/UhzxVq1YPMvgNacefuAkdGAKuvoVLrAKdvEJMgHWfP2UMW8LzinBozVGvC9K1DJfNvG2KmrckgIM96Rc5EDI3XK4QYWeoazEBIw62Y3Kut9EQK5AOabgS4bYIIaXqu5-ib98oImko4ciX0e5fHQNve1i0G000F__0m00)
  * Nhiệm vụ của từng lớp phân tích
    -PaymentUI: Nhận đầu vào từ người dùng và hiển thị kết quả thanh toán.
    - PaymentController: Điều phối toàn bộ quá trình thanh toán và tương tác với các lớp Payment và Order.
    - Payment: Lưu trữ và cập nhật thông tin thanh toán.
    - Order: Cung cấp thông tin về đơn hàng.
  * Một số thuộc tính và quan hệ giữa các lớp phân tích
    - Payment và Order có mối quan hệ một-nhiều: Một Order có thể chứa nhiều Payment cho các đơn hàng lớn thanh toán từng phần.
    - PaymentController đóng vai trò như trung gian, quản lý quá trình thanh toán giữa các lớp.
  * các biểu đồ lớp
![](https://www.planttext.com/api/plantuml/png/T591JiCm4Bpx5Nk4GpuGeQg8NY8XKL7n01DlMqksD_AkWoh4opZm9Bw0qrf9MrBVTcPsFRFsx_VFaaL7ITwfrcbcMEk3no1l3NmgoAU27Ke1cx2bktkeeITh2ciiTquVYk8LEJcPD5_gSkmJ1Oda7CPnV1UfHUOYkDqwDcXFAPSr64hl3WlgKVPaChgHQCEke3cS9Bv6KsUquER8NUTXtUDitD7FIpHdzccecbLMsI054nBj7cTjMa4_-7csB0zDBXRJbe-3LoZQEhwuTtgJgbhChBA6nCZgFt4cFnd4g5jX-B2olo4_fQiXOjuOziYvRKkmZUILMc8mmrVv0m00__y30000)
   
4. Phân tích ca sử dụng Maintain Timecard
   
6. Hợp nhất kết quả phân tích



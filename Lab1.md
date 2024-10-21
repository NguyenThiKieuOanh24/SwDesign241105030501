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
  

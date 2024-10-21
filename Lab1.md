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
*  Cơ chế tính toán lương (Salary Calculation Mechanism)
  Lý do: Mục tiêu chính của hệ thống là tính toán lương dựa trên thời gian làm việc, loại công việc, mức lương, và các yếu tố khác như thuế, bảo hiểm xã hội, tiền thưởng, và tiền phạt. Cơ chế này cần thiết để đảm bảo việc tính toán lương được chính xác và nhanh chóng.
* Cơ chế quản lý thời gian làm việc (Timecard Management Mechanism)
  Lý do: Hệ thống phải theo dõi và quản lý thông tin thời gian làm việc của từng nhân viên để đảm bảo việc tính lương dựa trên thời gian thực tế. Cơ chế này bao gồm việc ghi nhận và xử lý thông tin từ các thẻ thời gian (timecards) hoặc hệ thống chấm công điện tử.
* Cơ chế lựa chọn phương thức thanh toán (Payment Method Selection Mechanism)
Lý do: Mỗi nhân viên có thể lựa chọn các phương thức thanh toán khác nhau như chuyển khoản ngân hàng, tiền mặt, hoặc qua séc. Cơ chế này cho phép nhân viên hoặc quản lý lựa chọn và điều chỉnh phương thức thanh toán phù hợp.
* Cơ chế xác thực và phân quyền (Authentication and Authorization Mechanism)
Lý do: Để đảm bảo tính bảo mật, hệ thống cần có cơ chế xác thực và phân quyền, nhằm đảm bảo chỉ những người có thẩm quyền mới có thể truy cập và thực hiện các hành động quan trọng, chẳng hạn như chỉnh sửa thông tin thanh toán hoặc xem báo cáo lương.
* Cơ chế lưu trữ và truy xuất dữ liệu (Data Storage and Retrieval Mechanism)
Lý do: Hệ thống cần quản lý dữ liệu lớn về nhân viên, thời gian làm việc, tiền lương, và các giao dịch thanh toán. Cơ chế lưu trữ và truy xuất dữ liệu cần hiệu quả và an toàn để đảm bảo tính toàn vẹn và khả năng truy cập nhanh chóng.
* Cơ chế xuất báo cáo (Reporting Mechanism)
Lý do: Quản lý cần theo dõi và kiểm tra các báo cáo liên quan đến lương nhân viên, bao gồm báo cáo tổng lương hàng tháng, báo cáo về thời gian làm việc, và các báo cáo tài chính khác. Cơ chế này giúp tổng hợp dữ liệu và xuất báo cáo một cách dễ dàng và chính xác.


# Ca sử dụng Login
## 1. Describe Interaction Among Design Objects
### Mô tả ca sử dụng:
- Actor: Employee, PayrollAdministrator.
- Mục đích: Xác thực người dùng để truy cập vào hệ thống.
- Luồng chính:
+ Người dùng mở giao diện đăng nhập.
+ Người dùng nhập tên đăng nhập và mật khẩu.
+ Hệ thống gửi thông tin đăng nhập đến SecuritySubsystem để xác thực.
+ Nếu xác thực thành công, hệ thống chuyển đến giao diện chính.
+ Nếu không thành công, thông báo lỗi được hiển thị.
### Các lớp tham gia:
- Boundary Class: LoginForm
- Control Class: LoginController
- Entity Class: User, SecuritySubsystem
### Biểu đồ tuần tự:

![Biểu đồ squence](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aK9eSMeHLr9-QLvAOb6bWaz-UcQUMtvHBbToVbv9KNuEHCGPmia1AatDAyaigLG8JaqkBG8oWakJYYkBIr9pkRX09YdesY7Ci5BmotYuQss1Gad6uIrvwGebcNaAHoOUQGOoyy0IN72bS7q8cwmKt1_kNfj9G3D2FSW835TPAKGSNfWCDEFXxet9I4PnOQXKqCNcX92YXxiMAsG_tBM_HA6m5CIkG9Y7wG9KttjaFjpTd0TMt8rYXaP8nk45UHaAoI3dw8S0lREqH27fuQw5cPfS3gbvAQ3O0G000F__0m00)

I.Phân tích các ca sử dụng trong hê thống Payment System.
  1. Phân tích ca sử dụng Create Administrative Report.
    * Các lớp phân tích cho ca sử dụng Create Administrative Report:
      - Actor: PayrollAdministrator
      - Boundary Class: ReportUI
      - Control Class: ReportControlle
      - Entity Class: Report
      - Entity Class: Employee
    * Biểu đồ sequence:

![](https://www.planttext.com/api/plantuml/png/Z9D1JiCm44NtFeMNxQ8NO86Ae4ALG495i1_YQHdXscKygPIpiU18N04xSTAaj2LUMChel__7O-VdwtiU15ZAhLNXWvnc7r118Pxr4rJihRqnMt8KX24MrPildG6kz0ftdkLbgMwzawZBXVnbaTN22KahLEgKdPvTTqRwIZD-bXWaEp62a7UJgUeadVmG4x4Do3joIv4W4tHKJzdHaTc39GE2V_HwTZea0x6X5ORIYW8h-ZKLTUkXT5mNKpVeC1uScyAaoE2qHvxBvxfqdmtCPFfFMZrGGs5deSfn3L9lgVbds6DxEpglyPUKw87lePsp5nLsMD2wIkY3BzhR7S9d9XSESJQZn-JboQLGCogjFxb4HSsQUDjl5sr0VKUX03R78xnu3DCmWy6XCwesNBhwaUauyaSAWTncxDFgjxnWzXoja-qyRkdN_WK00F__0m00)

    * Nhiệm vụ của từng lớp phân tích
      - ReportUI: Nhận các thông tin từ Payroll Administrator như loại báo cáo, thời gian và tên nhân viên, hiển thị kết quả báo cáo và cung cấp tùy chọn lưu trữ.
      - ReportController: Điều phối các yêu cầu từ ReportUI, xác thực và kiểm tra thông tin, xử lý tạo và lưu trữ báo cáo khi cần thiết.
      - Report: Tạo ra và lưu trữ dữ liệu của báo cáo, bao gồm loại báo cáo và thông tin chi tiết từ các nhân viên được yêu cầu.
    
    * Một số thuộc tính và quan hệ giữa các lớp phân tích:
      - ReportUI
        + Phương thức: requestReportCreation(), displayReport(), requestSaveReport().
      - ReportController
        + Phương thức: gatherReportCriteria(), validateCriteria(), generateReport(), specifySaveLocation(), saveReport(), discardReport().
      - Report
        + Thuộc tính: reportType, beginDate, endDate, employeeList, location.
        + Phương thức: generateReport(criteria), saveReport(location), discardReport().
      - Employee
        + Thuộc tính: employeeID, name, totalHoursWorked, payYearToDate.
        + Phương thức: provideEmployeeData().
        
    * Các biểu đồ lớp:

    ![](https://www.planttext.com/api/plantuml/png/h5FBRi8m4BpdAtni3_m0gX0IL2eIfq9LzRZ42rWuNdUzYHHL_R8U-adzXJhWX4Uek3GN9plZdV5a_VFrFGu2B6LXix0pJZ45p78B8QXdzCJoCbCVcTe_ZEyb1ZdK9umWXjpTlHggYenE96s2jr0VI9TWwh202Yy9dzcPx8ISC5cBtCblGBR8hReHP0EN0XLOeq7m35yHsRO7EkI8dwWVNXCUFEPcNJS6vvHVFM0uchU94WaBOUCs_InoO7tZgEc0WvXEyxciFNOD4xB2ZN7Jw3i2pPBAwFILOk4jrOXp4oGYpVBmc6gZnEaPlnvFdbBin_H_6RJMkXHQ_xDfv1edgUoWwCKY962VgEJmIhn37N5DvSgsKNYetn1uIIcb4r0fprGPZQr-fC2PlMxy1uDHVoY7gWmOibxzI8wKlBaZ61GulO_i3tuNmL2jKV9jt15d6DIQgSYoSVpBpVNy1G00__y30000)


    * Giải thích:
    - ReportUI (Boundary Class)
      + requestReportCreation(): Bắt đầu quy trình tạo báo cáo khi Payroll Administrator yêu cầu.
      + displayReport(): Hiển thị báo cáo sau khi được tạo.
      + requestSaveReport(): Cho phép Payroll Administrator yêu cầu lưu báo cáo.
    - ReportController (Control Class)
      + gatherReportCriteria(): Thu thập các tiêu chí báo cáo từ ReportUI.
      + validateCriteria(): Kiểm tra xem thông tin đầu vào từ người dùng có đủ và đúng không.
      + generateReport(): Tạo báo cáo dựa trên các tiêu chí đã xác thực.
      + specifySaveLocation(): Thu thập thông tin về tên và vị trí lưu trữ báo cáo.
      + saveReport(location : String): Lưu báo cáo vào vị trí và tên mà người dùng chỉ định.
      + discardReport(): Huỷ bỏ báo cáo nếu Payroll Administrator không yêu cầu lưu.
    - Report (Entity Class)
      + Thuộc tính:
          reportType: Loại báo cáo (giờ làm việc tổng cộng hoặc lương tính đến hiện tại).
          beginDate và endDate: Khoảng thời gian mà báo cáo bao phủ.
          employeeList: Danh sách các nhân viên được báo cáo.
          location: Vị trí lưu trữ báo cáo.
      + Phương thức:
          generateReport(criteria): Tạo báo cáo dựa trên tiêu chí từ ReportController.
          saveReport(location : String): Lưu báo cáo theo thông tin vị trí do ReportController cung cấp.
          discardReport(): Huỷ báo cáo nếu không cần lưu.
    - Employee (Entity Class)
      + Thuộc tính:
          employeeID: ID duy nhất của nhân viên.
          name: Tên của nhân viên.
          totalHoursWorked: Tổng giờ làm việc của nhân viên.
          payYearToDate: Lương tính đến thời điểm hiện tại của nhân viên.
      + Phương thức:
          provideEmployeeData(): Cung cấp dữ liệu của nhân viên cho lớp Report khi cần tạo báo cáo.

I. Phân tích các ca sử dụng trong hê thống Payment System.
  1. Phân tích ca sử dụng Create Administrative Report.
    * Các lớp phân tích cho ca sử dụng Create Administrative Report:
      - Actor: PayrollAdministrator
      - Boundary Class: ReportUI
      - Control Class: ReportController
      - Entity Class: Report
      - Entity Class: Employee
    * Biểu đồ sequence:

![](https://www.planttext.com/api/plantuml/png/Z9D1JiCm44NtFeMNxQ8NO86Ae4ALG495i1_YQHdXscKygPIpiU18N04xSTAaj2LUMChel__7O-VdwtiU15ZAhLNXWvnc7r118Pxr4rJihRqnMt8KX24MrPildG6kz0ftdkLbgMwzawZBXVnbaTN22KahLEgKdPvTTqRwIZD-bXWaEp62a7UJgUeadVmG4x4Do3joIv4W4tHKJzdHaTc39GE2V_HwTZea0x6X5ORIYW8h-ZKLTUkXT5mNKpVeC1uScyAaoE2qHvxBvxfqdmtCPFfFMZrGGs5deSfn3L9lgVbds6DxEpglyPUKw87lePsp5nLsMD2wIkY3BzhR7S9d9XSESJQZn-JboQLGCogjFxb4HSsQUDjl5sr0VKUX03R78xnu3DCmWy6XCwesNBhwaUauyaSAWTncxDFgjxnWzXoja-qyRkdN_WK00F__0m00)


    * Nhiệm vụ của từng lớp phân tích
      - ReportUI: Nhận các thông tin từ Payroll Administrator như loại báo cáo, thời gian và tên nhân viên, hiển thị kết quả báo cáo và cung cấp tùy chọn lưu trữ.
      - ReportController: Điều phối các yêu cầu từ ReportUI, xác thực và kiểm tra thông tin, xử lý tạo và lưu trữ báo cáo khi cần thiết.
      - Report: Tạo ra và lưu trữ dữ liệu của báo cáo, bao gồm loại báo cáo và thông tin chi tiết từ các nhân viên được yêu cầu.
      - Employee: Cung cấp dữ liệu chi tiết của nhân viên để Report có thể tạo báo cáo đúng với yêu cầu của Payroll Administrator.
    
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
        
2. Phân tích ca sử dụng Create Employee Report.
    * Các lớp phân tích cho ca sử dụng Create Employee Report:
      - Actor: Employee
      - Boundary Class: ReportUI
      - Control Class: ReportController
      - Entity Class:
        + Report
        + ProjectManagementDB
        + Employee
    * Biểu đồ sequence:

![](https://www.planttext.com/api/plantuml/png/Z5HBJiCm4Dtd55PNPS45AXKLMYIG024e1nYI8JLoF64ygTIpiU18N05RiPj-NDGk8lLbthmtRqRv_VwPEG6MhZ45b4AiRflMq0QnQ3siIzs25VM2BR6ytMV0ELbXCWOvyt8FUcRwn58UmKAD3LfPt1H5abENLrkLYMBywj19L604qMJ75qMg6Ae7-OcgGLR8YQG5MSEMD1G6Sf8za5fkMhosrG84FV7OswvQoxJM5UQ8O5800LVJgHejIS2eE-hOgGyVSmnZL2Z_opdCfEKdH8duV0LSurFNl2CxBndQP2XvwupIiSsrE2khZ8L8Fokn0nxQAhkY7WipMsIVQ_z_NCR5fhsUcZ0WVXtmJ-zmQPLshO5DR3xG-YLkvobNH0wT4b8ErhYJLN-CHncz-ge7AjFXviC91c8egNQ10jhih-FKlGSdqRY9zDDRJ746qavvI7_c7-43y0S00F__0m00)


    * Nhiệm vụ của từng lớp phân tích
      - ReportUI: Thu thập tiêu chí báo cáo từ nhân viên, hiển thị báo cáo được tạo, và xử lý yêu cầu lưu báo cáo từ nhân viên.
      - ReportController: Xử lý các bước tạo báo cáo, lấy thông tin về dự án (nếu cần), và thực hiện lưu báo cáo khi được yêu cầu.
      - Report: Tạo ra và lưu trữ dữ liệu của báo cáo, bao gồm loại báo cáo và thông tin chi tiết từ các nhân viên được yêu cầu.
      - ProjectManagementDB: Cung cấp danh sách mã số dự án và dữ liệu liên quan cho lớp Report khi cần tạo báo cáo.
      -  Employee:Cung cấp dữ liệu nhân viên để lớp Report sử dụng trong quá trình tạo báo cáo.
      
    * Một số thuộc tính và quan hệ giữa các lớp phân tích:
    - Report:
      + Thuộc tính:
        reportTypeSelection: Loại báo cáo.
        dateRangeSelection:	Ngày bắt đầu và kết thúc cho báo cáo.
      + Phương thức:
        requestReportCreation() : Yêu cầu tạo báo cáo.
        displayReport() : Hiển thị báo cáo cho nhân viên.
        requestSaveLocation() : Yêu cầu thông tin vị trí lưu trữ báo cáo.
    - ReportController
      + Thuộc tính:
        criteria : Tiêu chí để tạo báo cáo (bao gồm loại báo cáo, ngày, mã dự án nếu có).
      + Phương thức:
        gatherReportCriteria() : Thu thập tiêu chí báo cáo từ ReportUI.
        validateCriteria() : Kiểm tra tính hợp lệ của các tiêu chí.
        generateReport() : Tạo báo cáo dựa trên tiêu chí.
        saveReport() : Lưu báo cáo tại vị trí do nhân viên chỉ định.
    - Report:
      + Thuộc tính:
        reportType : Loại báo cáo (Tổng số giờ làm việc, số giờ làm cho dự án, thời gian nghỉ phép/bệnh, lương tính đến hiện tại).
        beginDate : Ngày bắt đầu của báo cáo.
        endDate : Ngày kết thúc của báo cáo.
        employeeData : Danh sách nhân viên có trong báo cáo.
        chargeNumber : Mã dự án khi tạo báo cáo dự án.
      + Phương thức:
        generateReport(): Tạo báo cáo dựa trên các tiêu chí cung cấp.
        save(): Lưu báo cáo vào vị trí do nhân viên chỉ định.
    - Employee
      + Thuộc tính:
        employeeID : ID của nhân viên.
        name : Tên nhân viên.
        totalHoursWorked : Tổng số giờ làm việc.
        payYearToDate : Lương tích lũy tính đến hiện tại.
      + Phương thức:
        provideEmployeeData():Cung cấp dữ liệu cần thiết của nhân viên cho báo cáo.
    - ProjectManagementDB
      + Phương thức:
      getChargeNumbers() :Truy xuất danh sách mã dự án có sẵn từ cơ sở dữ liệu.
  
    * Các biểu đồ lớp:

   ![](https://www.planttext.com/api/plantuml/png/h5J1ZjD03BtdAqOz0L8FN2jKhMYHM6b1Y5s4EBepRZhBP1myJgK8yMKS-2H-0IUTfDict3QNIVoUxUSdJ_x-_dEJ15YQAXGsG4hcCzR4ykNM_2nC_p3-Q339XX44J-YBbsPbZkHTfZYVwW3jF9Zpx-68TsH1FCKpvLTnqNP3KPX2G1xRbo07v0op5sGFrosE4BnJTHVuZYWCDJ0YNwe_lMOyrMZzlfsNc2cAvVIGAKgu5_QndBfXWTsr6rUZvW6Nwa_t-T3ME1RCo0vB7xUgMu7ko66CRYPOrO5Qn3kVH97kUFCknzQPCn4-Ru_DBavjUZuF1ccZ2uF-swroVPGSZb1DR14I2E-fuVIL-3iwnHqrkp1OKKFx3O4VABlq13IcPZfwXqD_fS2Cl4zCZsZb0qGeiS8esxVdXKJP781B_DXKE-JKf_T-drIkkpBZBLekrzFTNfacOIecyJDPARQ_SCb0TBtp_-6FJgxC7iKUD4El0fWzKpMVCJUSkeIrBXP6sveziR7zY2QUPio5pEBreY-nUBLusbWj8-lxXIYA6otJ_Kx-0G00__y30000)

 3. Phân tích ca sử dụng Maintain Employee Information:
    * Các lớp phân tích:
      - Boundary Class: EmployeeUI
      - Control Class: EmployeeController
      - Entity Class:
        + Employee
        + EmployeeDatabase
        + PayrollSystem
        + IDGenerator
    * Biểu đồ sequence:
  -  Thêm nhân viên:
![](https://www.planttext.com/api/plantuml/png/Z59BRi8m4Dtx5Bv0Bz058ceGogP2L3c0YmUmwinGPz8eP-kYH-8As8A0JJxgpXwzpyoREV_-BMjMZflA2hLZSdAZEaVMPheoQ6fsoXS581lkvAewMUe0okAvyaR8WGO3xFC_Lwm-LNsl5_aQ4AusOinSlYmYO_agj_3TGCsIIMPQFumYK4HvTEQf7u0w8VLYOWG-vNld5hWdLoasXFyntpZwCHhc-Qb_58uNkBr1bcXyAv5GBcBaL0DRuCPXGCzFsw_8KvAiGbqCG5DksUuBgRMW3n1apCoOISnzJE_G9XEc2OzUYb_maTe1S-ct7Wxy0W00__y30000)

- Cập nhật nhân viên:

![](https://www.planttext.com/api/plantuml/png/b9D1Si8m34NtFeKlq0kmO62W2tPC6GuWi6WzjIsgA30v6mkEn1LmcWb9ZIbXQLbFNr-MBwVpf11WARrJi1LYlOIAoRcfyJROGXXYK64GAvL-ztj75U9waKPc5AJ6y2utFSz1O0C5AfLJqc_ZdeeUwG_yAR4GBQJNUmE2NU5UNe_gEedq2eD9kRQaoX2Fr6_iOZv4Tibqi0QpM5wjdSglfh35GvyEEs8FOYceE-1H3x5CoQ4hKWElM6wcPhBY0wp_XpyTGVfYVtf_wdow_GvqT6W-spQ6-8vNEyi-9HghsLMDw_L5nnPiB4xYmjL_wGe00F__0m00)
  
- Xóa nhân viên:

![](https://www.planttext.com/api/plantuml/png/b9DDReCm48NtFeKlq0jaKIKghPH5gwXH3p0nGsDXFAaP4d6sBdgaNg66a63-15qocc_UlCVuz_jddJCuBZ8ZG34vkOFIaJ6REDDMv-p05mLQrbpAv-nag4JysFOhJsIvmd3Gs_-EWE40-RtUwEtBd34JOanUFZm6qd8bt_6hm9mbaupG86Eh5lG5LBkUf_Teupvt6ob6Y2drExkDbiZk79rrZAFOkDejgbgJdSPpIDk4N0QioOe1CBM37rCusmwfWFzOzYs9RbJRz9UuRyWh4UuyQ_qLNDfkx4qFPypwtgZKqiLW_8bp6tJkqQDln3efQzqNRS5K3Ug8AXNTpYNIzIojO440TUoJeLs37dqh_hwFTEdyAR7s5r-zy3y0003__mC0)

    * Nhiệm vụ của từng lớp phân tích
      - EmployeeUI: Quản lý giao diện cho Payroll Administrator để thực hiện các chức năng thêm, cập nhật và xóa thông tin nhân viên.
      - EmployeeController: Điều phối quá trình thêm, cập nhật và xóa nhân viên, xử lý logic và giao tiếp với EmployeeDatabase.
      - Employee: Lưu trữ thông tin nhân viên, bao gồm các thuộc tính cá nhân và mức lương.
      - EmployeeDatabase: Lưu trữ, truy xuất, và quản lý dữ liệu nhân viên trong hệ thống.
      - PayrollSystem: Quản lý và cập nhật bảng lương liên quan đến nhân viên, đặc biệt là việc xử lý nhân viên đã xóa.
      - IDGenerator: Tạo ID duy nhất cho nhân viên mới trong quá trình thêm.
    
    * Một số thuộc tính và quan hệ giữa các lớp phân tích:
     - Các Thuộc Tính
      + EmployeeUI
        functionSelection : Lựa chọn thêm, cập nhật hoặc xóa nhân viên.
        employeeInfoInput :  Thông tin nhân viên nhập vào.
        confirmationResponse : Xác nhận xóa từ Payroll Administrator.
      + EmployeeController
        currentEmployee : Thông tin của nhân viên hiện tại trong quá trình cập nhật/xóa.
        actionType : Loại hành động đang thực hiện (Add, Update, Delete).
      + Employee:
        employeeID : Mã ID nhân viên.
        name : Tên nhân viên.
        employeeType : Loại nhân viên (theo giờ, lương cứng, có hoa hồng).
        address : Địa chỉ của nhân viên.
        socialSecurityNumber : Số bảo hiểm xã hội của nhân viên.
        hourlyRate : Lương theo giờ (dành cho nhân viên theo giờ).
        salary :  Mức lương cứng (dành cho nhân viên lương cứng hoặc hoa hồng).
        commissionRate : Tỷ lệ hoa hồng (dành cho nhân viên có hoa hồng).
      + EmployeeDatabase
        employees : Danh sách các nhân viên hiện có trong hệ thống.
      + PayrollSystem
        markedForDeletion : Danh sách các nhân viên đã bị đánh dấu để xóa.
        finalPaycheckProcessing() : Xử lý lần trả lương cuối cùng cho nhân viên bị xóa.
      + IDGenerator:
        generateID() : int — Tạo mã ID duy nhất cho nhân viên mới.
    - Quan Hệ Giữa Các Lớp:
      + EmployeeUI uses EmployeeController: EmployeeUI gửi yêu cầu tới EmployeeController để điều phối quá trình thêm, cập nhật, hoặc xóa nhân viên.
      + EmployeeController manages Employee: EmployeeController quản lý việc thêm, cập nhật, và xóa thông tin của một đối tượng Employee.
      + EmployeeController stores in EmployeeDatabase: EmployeeController lưu hoặc cập nhật thông tin nhân viên vào EmployeeDatabase.
      + EmployeeController coordinates with PayrollSystem: EmployeeController tương tác với PayrollSystem khi cần xử lý việc trả lương cho nhân viên bị xóa.
      + IDGenerator generates ID for EmployeeController: IDGenerator cung cấp ID duy nhất cho nhân viên mới qua EmployeeController.
    * Các biểu đồ lớp:

   ![](https://www.planttext.com/api/plantuml/png/X9HBZjH038RtEOMN8D4NA8r68n50BV4OJSC1d9JJNKmzed9bK8Gu6GkEn1LmXIHq9nqcgwZysV7_svNVFt_TSSAOEcUBsY8pl76j3JtHbpryBq2U7JIThvC9_a2MXXS5XnIDFuvn6bFslWbxttP9mGTiR_uoh-1JzLNIRaUu3hunqM6kyq3S1i-ae0h14lg10T26MulzrChR4DsBbmgUWj6NnEkpOZFnerX84Ih5O2t5MLBTnKW-JOIQsJ6EWyxFVKiNMW5GwmbTjDIr6XDj1BLOToMuQdLkSFQqL61y6ayzEjemVzNhBlSQYNbnog4sQ0ya5fZKV-nSHN61d48NRVyWSXJeq5LsieNHOkmNXtLmpZ3dUIup08uqcrnIGcCvYn-_jf9VOi8AUMs3Y7XlEDrCuErOdl7fdwkqckP_9_GSlfZPDZxBkCS-xzcXvqHkrk0mFfAM9IvpmU7wNDNI68zMIjGdgX_lOwXbTkBIUbdsvJlo5365QQ6ppyE9x4lcyyO8VdQNTxjhrq51nyJ5bSWPBvH3ZyTdmNbw2bXw8vO-Db8kdLAoGo5gqPyawPj9f-9SurRla-Ri23GX5dVaTVwJ_G400F__0m00)

4. Phân tích ca sử dụng Run Payroll
    * Các lớp phân tích cho ca sử dụng Create Employee Report:
      - Boundary Class: PayrollUI
      - Control Class: PayrollController
      - Entity Class:
        + Employee
        + Timecard
        + Payroll
        + BankTransaction
    * Biểu đồ sequence:

![](https://www.planttext.com/api/plantuml/png/b9DDReCm48NtFeKlq0jaKIKghPH5gwXH3p0nGsDXFAaP4d6sBdgaNg66a63-15qocc_UlCVuz_jddJCuBZ8ZG34vkOFIaJ6REDDMv-p05mLQrbpAv-nag4JysFOhJsIvmd3Gs_-EWE40-RtUwEtBd34JOanUFZm6qd8bt_6hm9mbaupG86Eh5lG5LBkUf_Teupvt6ob6Y2drExkDbiZk79rrZAFOkDejgbgJdSPpIDk4N0QioOe1CBM37rCusmwfWFzOzYs9RbJRz9UuRyWh4UuyQ_qLNDfkx4qFPypwtgZKqiLW_8bp6tJkqQDln3efQzqNRS5K3Ug8AXNTpYNIzIojO440TUoJeLs37dqh_hwFTEdyAR7s5r-zy3y0003__mC0)


    * Nhiệm vụ của từng lớp phân tích
      - PayrollUI: Khởi tạo quá trình xử lý bảng lương và hiển thị trạng thái hoặc kết quả cho người dùng.
      - Employee: Đại diện cho từng nhân viên và lưu trữ các thông tin chi tiết như mức lương, phương thức thanh toán và trạng thái xóa.
      - Timecard: Quản lý giờ làm việc của từng nhân viên để cung cấp dữ liệu tính lương.
      - Payroll: Thực hiện các phép tính cho lương ròng và áp dụng các khoản khấu trừ hợp pháp.
      - BankTransaction: Xử lý giao dịch ngân hàng cho các khoản thanh toán qua chuyển khoản.
      - PayrollController: Điều phối toàn bộ quy trình chạy bảng lương, lấy danh sách nhân viên, tính toán và thực hiện thanh toán dựa trên phương thức đã chọn.
    * Một số thuộc tính và quan hệ giữa các lớp phân tích:
    - PayrollUI:
      + Phương thức:
        runPayroll(): Gửi yêu cầu chạy bảng lương tới PayrollController.
        printPaycheck(empInfo: Employee, netPay: Float): In phiếu lương cho nhân viên.
        displayPayrollStatus(status: String): Hiển thị trạng thái quá trình chạy bảng lương.
    - PayrollController
      + Phương thức:
        runPayroll(): Quản lý toàn bộ quá trình chạy bảng lương.
        getEligibleEmployees(): List: Lấy danh sách nhân viên đủ điều kiện nhận lương.
        processEmployeePay(employee: Employee): Tính toán và xử lý thanh toán cho từng nhân viên.
        markForDeletionIfNeeded(employee: Employee): Đánh dấu xóa nhân viên nếu cần.
    - Employee
      + Thuộc tính:
        employeeID : ID của nhân viên.
        name : Tên nhân viên.
        totalHoursWorked : Tổng số giờ làm việc.
        payYearToDate : Lương tích lũy tính đến hiện tại.
      + Phương thức:
        provideEmployeeData():Cung cấp dữ liệu cần thiết của nhân viên cho báo cáo.
    - ProjectManagementDB
      + Phương thức:
      getChargeNumbers() :Truy xuất danh sách mã dự án có sẵn từ cơ sở dữ liệu.
    - Employee
      + Thuộc tính:
          employeeId: String
          salary: Float
          paymentMethod: String
          markedForDeletion: Boolean
      + Phương thức:
        isEligibleForPayroll(currentDate: Date): Boolean: Kiểm tra điều kiện nhận lương.
        getPaymentDetails(): Payment: Lấy thông tin thanh toán của nhân viên.
    - Timecard
      + Thuộc tính:
        employeeId: String
        hoursWorked: Float
        date: Date
      + Phương thức:
        getHours(employeeId: String): Float: Lấy số giờ làm việc của nhân viên.
    - Payroll
      + Phương thức:
        calculateNetPay(empInfo: Employee, hoursWorked: Float): Float: Tính lương ròng.
        applyDeductions(empInfo: Employee): Float: Áp dụng các khoản khấu trừ hợp pháp.
    - BankTransaction
      + Thuộc tính:
          transactionId: String
          amount: Float
    - Phương thức:
        processTransaction(empInfo: Employee, netPay: Float): Boolean: Thực hiện giao dịch ngân hàng.
  
    * Các biểu đồ lớp:

   ![](https://www.planttext.com/api/plantuml/png/T5FBJiCm4BpdAto4GtyWGgZb8HM9Yaejuhor5sBLiIFlkYX2V1a7FebVm6wYfExZ5izCPiUpoT_FxvGOF8VQ5D80aLX2wvqngvOOQ_5L225yi3rwTIrAiNDQ9LY2aS40OoGpel5E8b64QxHC8_TTz4CUwyQu5h7pn_xqz125sdB2BDGOJolssduaWC20RoEaNDWOJD06BRvhfWW-Q-ARJdoRA8KgIDREdf13XhMkKO9NbpDKBdXwStwBAflhTkWvlZrF_CWCpilWPGM4BrwXx-nTUZpqFZTlBvhLBbW-vzhLkK2kN1-wwQ1rs-HTAMJGXaPiCBa3kprSRR-g1AyzM89zQTd6yWzYCXcNLue5MFX0EjKCvPRYbSu9yeukgh8xNr8TNAeKzoxMg6tyB4byQgwA8MuUQmwKKSU1PaHEwcYZEfiyol7KVR0fMfL-f7y0003__mC0)

II. Code java mô phỏng ca sử dụng Maintain Timecard.
import java.util.ArrayList; import java.util.Date; import java.util.Scanner;

// Lớp đại diện cho thông tin của một nhân viên class Employee { private String employeeId; private String name;

public Employee(String employeeId, String name) {
    this.employeeId = employeeId;
    this.name = name;
}

public String getEmployeeId() {
    return employeeId;
}

public String getName() {
    return name;
}
}

// Lớp đại diện cho thông tin thẻ chấm công (timecard) class Timecard { private String employeeId; private Date date; private float hoursWorked;

public Timecard(String employeeId, Date date, float hoursWorked) {
    this.employeeId = employeeId;
    this.date = date;
    this.hoursWorked = hoursWorked;
}

public String getEmployeeId() {
    return employeeId;
}

public Date getDate() {
    return date;
}

public float getHoursWorked() {
    return hoursWorked;
}

@Override
public String toString() {
    return "Timecard{" +
            "employeeId='" + employeeId + '\'' +
            ", date=" + date +
            ", hoursWorked=" + hoursWorked +
            '}';
}
}

// Lớp đại diện cho bộ điều khiển quản lý thẻ chấm công class TimecardController { private ArrayList timecards = new ArrayList<>();

// Phương thức để ghi lại thông tin thẻ chấm công
public void addTimecard(String employeeId, Date date, float hoursWorked) {
    Timecard timecard = new Timecard(employeeId, date, hoursWorked);
    timecards.add(timecard);
    System.out.println("Timecard đã được ghi nhận: " + timecard);
}

// Phương thức để xem thẻ chấm công của nhân viên
public void viewTimecards(String employeeId) {
    System.out.println("Danh sách thẻ chấm công của nhân viên ID: " + employeeId);
    for (Timecard tc : timecards) {
        if (tc.getEmployeeId().equals(employeeId)) {
            System.out.println(tc);
        }
    }
}
}

public class Main { public static void main(String[] args) { Scanner scanner = new Scanner(System.in); TimecardController timecardController = new TimecardController();

    // Danh sách nhân viên mẫu
    Employee employee1 = new Employee("E001", "John Doe");
    Employee employee2 = new Employee("E002", "Jane Smith");

    // Ghi thẻ chấm công cho nhân viên
    System.out.println("Nhập số giờ làm việc của nhân viên " + employee1.getName() + ":");
    float hoursWorked1 = scanner.nextFloat();
    timecardController.addTimecard(employee1.getEmployeeId(), new Date(), hoursWorked1);

    System.out.println("Nhập số giờ làm việc của nhân viên " + employee2.getName() + ":");
    float hoursWorked2 = scanner.nextFloat();
    timecardController.addTimecard(employee2.getEmployeeId(), new Date(), hoursWorked2);

    // Xem thẻ chấm công
    System.out.println("\nDanh sách thẻ chấm công của " + employee1.getName() + ":");
    timecardController.viewTimecards(employee1.getEmployeeId());

    System.out.println("\nDanh sách thẻ chấm công của " + employee2.getName() + ":");
    timecardController.viewTimecards(employee2.getEmployeeId());

    scanner.close();
}
}

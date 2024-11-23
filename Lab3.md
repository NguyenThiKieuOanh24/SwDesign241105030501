# 1.	Subsystem context diagrams

## Biểu đồ ngữ cảnh 
### BankSystem
![Biểu đồ ngữ cảnh](https://www.planttext.com/api/plantuml/png/h591JiCm4BplArQvj4YaWciKHHKLXzuGVO59jgeLnuwyJaK4l8m3J-8BnAPkJNh5fz7Exipioj-VNsjsmhgXKy2jr6WD4opmIOpMA8KRevq7PA5MWZaIbpg-0OPd1tqYbpVm0PF8Wz0jxaPsrE5kUE60G6f7TYzgmgrlEF5HfQ7Ui7HBCMdL1wfRB332MvncJL0jWlXMxutjX9D6UylVX8beMNAqnTwQrx6g_iLeskrHE-b6t7XBuijnmdoI99dqOy-a0kQ3x1ckZvdThLRt6UPvXH6dLoemQwIbsiNu6FmOZr9aa7QMxtcUd0BEMvP_wxECSpgLzA7E6yw9grtNf1l_gtu0003__mC0)


Giải Thích cho BankSystem

- PayrollController: Thành phần điều phối việc gửi lệnh chuyển khoản cho nhân viên thông qua hệ thống ngân hàng.

- IBankSystem: Interface của BankSystem, qua đó PayrollController gửi yêu cầu chuyển khoản.

- BankSystem: Hệ thống con thực tế xử lý các giao dịch chuyển khoản trực tiếp vào tài khoản ngân hàng của nhân viên.

- Paycheck: Đối tượng chứa thông tin về lương của nhân viên, được sử dụng để xác định số tiền cần chuyển khoản.

- BankInformation: Đối tượng chứa thông tin tài khoản ngân hàng của nhân viên, cần thiết cho giao dịch chuyển khoản.
### PrintService
![Biểu đồ ngữ cảnh](https://www.planttext.com/api/plantuml/png/Z951JWCn34NtFeNLJSjYBb2DHfKg5kmGFK4OZ1erJQQs1n4LJiQYH-eL60-DXfODMLdVty_-oldhj19rhFq-WEnyH4v2CCT7bpc5WEiKrGfYQ8CJAOr9noFW-BYFb-RY3Zx18EoZueRupRU4c_vPiYZjOL29NzsWFOoMuYYapiH5vtAxfNQ7IriwbiQzdF5xhgwbi8VPz9wRvd-iuSRxg5upherACeKSFMPuek3KfoXRtmdyZLzLpKsC9SwO3Zs9_cp7idq6ryRwewgkajpq3JsTigBuOj_q3G00__y30000)

Giải Thích cho PrintService
- PayrollController: Đây là thành phần điều phối việc in phiếu lương và gửi yêu cầu in tới PrintService.

- IPrintService: Đây là interface của PrintService giúp đảm bảo tính trừu tượng. PayrollController tương tác với IPrintService để in phiếu lương.

- PrintService: Đây là hệ thống con thực tế thực hiện việc in phiếu lương (paycheck).

- Paycheck: Đây là đối tượng phiếu lương cần được in ra. PrintService sẽ nhận Paycheck từ PayrollController thông qua IPrintService và in nó.

### ProjectManagementDatabase subsystems
![Biểu đồ ngữ cảnh](https://www.planttext.com/api/plantuml/png/Z95DJiD038NtFeNL3MMH2rHHLAbbqGKIWXEumOM1YQUo7KG4d8m5H-8AT4fI_eBKMOtc-RtFzho_litDIRrj8jXz4DHa32TuGPsc676HnFE55Uf8PeFmzOvFWFkZhVJYz1HU88TekkFQyPo4RhXXSRngrzQPSmD1d7L3DUEgh_jMTiXary0FFDr-bgoME1jYCwJlwRT_IKvhCiQoj068kuZ7hggEpjuDS2OUlCD5fh3zf6NzaYDvI6AtOMlmTpL5KOrDDyF90CSUZa4sIPjzsWH6FELpKVm_w9WZmm-zpbckynz_0000__y30000)

Giải Thích cho ProjectManagementDatabase
- PayrollController: Thành phần điều phối việc lấy thông tin dự án cho quá trình tính lương.

- IProjectManagement: Interface của ProjectManagementDatabase qua đó PayrollController lấy thông tin dự án.

- ProjectManagementDatabase: Hệ thống con thực tế lưu trữ và cung cấp thông tin dự án của nhân viên.

- Project: Đối tượng dự án được ProjectManagementDatabase lưu trữ và truy xuất để hỗ trợ tính lương.

# 2.	Analysis class to design element map

| Analysis Class             | Design Element                  |
|----------------------------|----------------------------------|
| LoginForm                  | LoginForm                       |
| MaintainEmployeeForm       | MainEmployeeForm                |
| TimecardForm               | TimecardForm                    |
| MainApplicationForm        | MainApplicationForm             |
| TimecardController         | TimecardController              |
| SystemClockInterface       | SystemClockInterface            |
| PayrollController          | PayrollController               |
| Paycheck                   | Paycheck                        |
| Employee                   | Employee                        |
| BankSystemInterface        | IBankSystem, BankSystem         |
| PrintServiceInterface      | IPrintService, PrintService     |
| ProjectManagementSystem    | IProjectManagement, ProjectManagementDatabase |
| PayrollReportGenerator     | PayrollReportGenerator          |
| EmployeeDatabase           | EmployeeDatabase                |


# 3.	Design element to owning package map

| Design Element        | "Owning" Package                            | 
|-----------------------|---------------------------------------------|
| LoginForm             | Middleware::Security::GUI Framework         |
| MainEmployeeForm      | Applications::Employee Activities           |
| TimecardForm          | Applications::Employee Activities           |
| MainApplicationForm   | Middleware::Security::GUI Framework         |
| TimecardController    | Applications::Employee Activities           |
| SystemClockInterface  | Applications::Payroll                       |
| PayrollController     | Applications::Payroll                       |
| Paycheck              | Business Services::Payroll Artifacts        |
| Employee              | Business Services::Employee Management      |
| IBankSystem           | External Interfaces::Banking                |
| BankSystem            | External Interfaces::Banking                |
| IPrintService         | External Interfaces::Printing               |
| PrintService          | External Interfaces::Printing               |
| IProjectManagement    | External Interfaces::Project Management     |
| ProjectManagementDatabase | External Interfaces::Project Management |

# 4.	Architectural layers and their dependencies

![](https://www.planttext.com/api/plantuml/png/V59BJiCm4Dtx55OFq1DKKMa1AL8hHIgxYiNW3i7O7aTZjrA4E1aBZiGLI9poIPfqPS_p-BtdD_xw-5o621oFpefWD4ds0KK5oa29SbOm1gG8KNkI6wYHPtAniEqco-IRa7A_yQMcUy_kiQsseEdELTRNYB_WWtQeW0-zhfkgibebvWv_5t-w_mudP0kesLkxzXJR5RcdD81tTOZerjOharD4VWQ5VS7LCMZ24EGE-QGLXcbPzOBA9DgVX_QfMeMIhtdFLq2cyvHu1cLUiAPuDfAG2w1fyQ-euXQeqNJDYCvz0_GM8Zn1w1oEJdC-pyRY5cCZIBrJIOdf3DEzorZ44kdGV3mflW400F__0m00)

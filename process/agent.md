# Tổng quan về Zabbix Agent
Được triển khai trên mục tiêu giám sát để chủ động giám sát các tài nguyên và ứng dụng cục bộ(Disk, Storage, Tống kê CPU, v.v)

Agent thu thập thông tin hoạt động cục bộ và báo cáo dữ liệu cho máy chủ Zabbix để xử lý thêm. Trong trường hợp có lỗi (chẳng hạn như đĩa cứng đang chạy đầy hoặc quá trình dịch vụ bị lỗi), máy chủ Zabbix có thể chủ động cảnh báo cho quản trị viên của máy cụ thể đã báo cáo lỗi.

## PASSIVE CHECK AND ACTIVE CHECK
* PASSIVE Check: Zabbix Agent phản hồi một yêu cầu dữ liệu. Zabbix server yêu cầu dữ liệu **=>** Zabbix Agent gửi lại dữ liệu
* ACTIVE Check: Yêu cầu xử lý phức tạp hơn. Trước tiên, agent phải truy xuất các danh sách **iterm** từ máy chủ Zabbix để xử lý độc lập. sau đó, nó sẽ định kỳ gửi các giá trị mới đến máy chủ.

Việc thực hiện ACTIVE Check hay PASSIVE check được cấu hình bằng cách chọn loại **Iterm** giám sát tương ứng. Agent xử lý các Iterm  thuộc loại agent hoặc active

## Cài đặt Zabbix Agent

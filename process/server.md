# Tổng quan về server trong Zabbix
Server thực hiện việc polling và trapping của dữ liệu, nó tính toán các trigger, gửi thông báo đến người dùng. Là thành phần trung tâm mà các Zabbix agent và ptoxies báo cáo dữ liệu về tính khả dụng và tính toàn vẹn của hệ thống. Máy chủ có thể tự kiểm tra từ xa các dịch vụ các kết đến mạng Internet( chẳng hạn như Webserver và Mail servers) bằng cách sử dụng các kiểm tra dịch vụ đơn giản.

Server là kho lưu trữ trung tâm, trong đó tất cả dữ liệu cấu hình, thống kê và hoạt động được lưu trữ và chính thực thể trong Zabbix sẽ chủ động cảnh báo cho quản trị viên khi có vấn đề phát sinh trong bất kỳ hệ thống được giám sát nào.

Hoạt động của một máy chủ Zabbix cơ bản được chia thành ba thành phần riêng biệt;
* Zabbix Server 
* Web frontend
* Database storage

Tất cả thông tin cấu hình cho Zabbix được máy chủ lưu trữ trong cơ sở dữ liệu mà cả máy chủ và frontend đều tương tác.Ví dụ: Khi bạn tạo một mục mới bằng cách sử dụng Frontend, nó sẽ được thêm và table trong table của database. Sau đó, khoảng một phút một lần, Zabbix server sẽ truy vấn đến table để biết danh sách các item đang hoạt động sau đó lưu trữ trong bộ đệm của Zabbix server. Đây là lý do tại sao có thể mất tới hai phút để bất kỳ thay đổi nào được thực hiện trong Zabbix Frontend hiện thị trong phần dữ liệu mới nhất
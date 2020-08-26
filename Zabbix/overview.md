# Giới thiệu tổng quan về Zabbix

Zabbix là một giải pháp giám sát phân tán mã nguồn mở cấp doanh nghiệp

Zabbix là phần mềm giám sát nhiều thông số của mạng cũng như tình trạng và tính toàn vẹn của máy chủ. Zabbix sử dụng cơ chế thông báo linh hoạt cho phép người dùng cấu hình cảnh báo dựa trên email  cho hầu hết sự kiện. Điều này cho phép phản ứng nhanh với các sự cố máy chủ. Zabbix cung cấp các tính năng báo cáo và hiển thị dữ liệu tuyệt vời dựa trên dữ liệu được lưu trữ. 

Tất cả các báo cáo và thống kê của Zabbix, cũng như các thông số cấu hình, đều được truy cập thông qua giao diện người dùng dựa trên Web. Giao diện người dùng dựa trên web đảm bảo rằng trạng thái của mạng và tình trạng của máy chủ có thể được đánh giá từ bất kỳ đâu. Được cấu hình phù hợp, Zabbix có thể giám sát cơ sở hạ tầng công nghệ thông tin.

## Thu thập dữ liệu
* Kiểm tra tính khả dụng và hiệu suất 
* Hỗ trợ SNMP, IPMI, LMX, giám sát VMware 
* Kiểm tra tùy chỉnh
* Thu thập dữ liệu mong muốn ở các khoản thời gian tùy chỉnh
* Được thực hiện bởi máy chủ server/proxy và agent

## Định nghĩa ngưỡng cảnh báo linh hoạt
Bạn có thể định nghĩa các ngưỡng vấn đề cảnh báo, tham chiếu các giá trị từ backend database 
## Cấu hình cho cảnh báo
* Các thông báo có thể được tùy chỉnh cho lịch trình báo cáo, người nhận, media type.
## Đồ thị thời gian thực
Các items được giám sát được lập biểu đồ bằng chức năng vẽ đồ thị tích hợp
## Khả năng giám sát web 
Zabbix có thể theo dõi đường dẫn của các cú nhấp chuột mô phỏng trên trang web và kiểm tra chức năng cũng như thời gian phản hồi.
## Các tùy chọn hình ảnh hóa mở rộng
* Khả năng tạo biểu đồ tùy chỉnh có thể kết hợp nhiều mục vào một chế độ xem duy nhất
* Network map
* Màn hình tùy chỉnh và trình chiếu để có tổng quan kiểu bảng điều khiển 
* Báo cáo
## Lưu trữ dữ liệu lịch sử
* Dữ liệu được lưu trữ trong cơ sở dữ liệu
* Lịch sử có thể được cấu hình
* Được xây dựng sẵn khả năng dọn dẹp
## Cấu hình dễ dằng
* THêm các thiết bị được giám sát làm máy chủ
* Máy chủ được chọn để theo dõi, một khi trong cơ sở dữ liệu
* Áp dụng mẫu cho các thét bị được giám sát
## Sử dụng các TemPlate
* Nhóm lại các checks TemPlate
* TemPlate có thể thừa kế từ TemPlate khác
## Discovery Network
* Tự động Discovery các thiết bị mạng
* Tự động đăng ký các agent
* Discovery hệ thống tệp, Giao diện mạng và SNMP OID
## Giao diện web nhanh gọn
* Một giao web được xây dựng bởi PHP
* Có thể truy cập từ mọi nơi
* audit log
## API Zabbix 
Cung cấp giao diện có thể lập trình cho z\ để thao tác hàng loạt, tích hợp phần mềm của bên thứ 3 và các mục đích khác
## Hệ thống phân quyền
* Xác thực người dùng an toàn
* Một số người dùng nhất định có thể bị giới hạn một số chế độ xem nhất định
## Agent có đầy đủ tính năng dễ dàng mở rộng
* Triển khai trên các mục tiêu giám sát
* Triển khai trên cả linux và Window 
# Deamon nhị phân
* Được viết bằng ngôn ngữ C, cho hiệu suất cao và dung lượng bộ nhớ thấp
* dễ dàng di chuyển
## Sẵn sàng giám sát các môi trường phức tạp
* Giám sát từ xa dễ dàng bằng cách sự dụng poxy Zabbix

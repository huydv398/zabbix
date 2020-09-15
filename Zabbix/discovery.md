# Auto Discovery 
Giám sát môi trường lớn có thể là một cơn ác mộng nếu không có tự động hóa. Zabbix cung cấp một số cách tự động hóa việc quản lý các môi trường như vậy. Các thiết bị và phần tử của thiết bị, Chẳng hạn như hệ thống tệp và web interface, có thể được them và xóa tự động khi chúng đến và rời khỏi một tổ chức.

Có 3 cách tiếp cận chính để khai phá tự động và quản lý các yếu tố môi trường trong Zabbix: Khám phá mạng, Khai phá cấp thấp và đăng ký tự động Agent, mỗi cách phục vụ lĩnh vực riêng của nó.

## Network Discovery
Chức năng này cho phép quét mạng định kỳ để tìm các dịch vụ bên ngoài(external services) hoặc các Zabbix Agent(Passive) và thực hiện các hành động được xác định trước khi phát hiện ra các dịch vụ đó.

![huydv](/images/Screenshot_25.png)

Quá trình Discovery bắt đầu bằng việc chạy các quy tắc khám phá mạng:
* Scan theo dải IP
* Cần tìm các dịch vụ bên ngoài(FTP, SSH, WEB, POP3, IMAP, TCP, v.v)
* Thông tin nhận được từ Zabbix Agent
* Thông tin nhận được từ một SNMP Agent

Sau đó hàm khai phá sẽ tạo ra một Discovery Events; có thể là cơ sở cho một hành động có liên quan, được xác định trước.
* Gửi thông báo cho người dùng
* Thêm xóa máy chủ
* Bật & tắt máy chủ
* Thêm hoặc xóa máy chủ lưu trữ vào một nhóm;
* Liên kết hoặc hủy liên kết máy chủ lưu trữ với một mẫu
* Thực thi lệnh từ xa

Các hành động có thể được cấu hình để tính toán đến loại thiết bị, IP, trạng thái, thời gian hoạt động/ thời gian ngường hoạt động và các thông số khác.

## Low-level discovery (LLD)
Cung cấp cách tự động tạo các thư mục, trình kích hoạt và biểu đồ cho các phần tử khác nhau trên thiết bị. Ví dụ: Zabbix có thể tự động bắt đầu giám sát hệ thống tệp hoặc giao diện mạng trên máy mà không cần phải tạo các thư mục cho từng hệ thống tệp hoặc giao diện mạng theo cách thủ công.

![huydv](/images/Screenshot_26.png)

Zabbix hỗ trợ một số loại item discovery:
* File systems
* network interfaces
* CPUs và CPU cores
* nhiều SNMP OIDs
* Sử dụng câu truy vấn
* Windows Services 

Hơn nữa người dùng có thể tạo các Low-level Discovery Rules tùy chỉnh, khám phá bất kỳ loại thực thể nào- Ví dụ: CDSL trên máy chủ MySQL

## Tự động đăng ký lại Agent đang hoạt động

Chức năng này cho phép máy chủ Zabbix tự động bắt đầu giám sát thiết bị mới nếu thiết bị này có cài đặt Zabbix Agent(đang hoạt động). Điều này cho phép thêm máy chủ Zabbix thủ công cho từng máy chủ đơn lẻ. Khi thêm một máy chủ mới vào môi trường được giám sát, chỉ cần cài đặt một Zabbix Agent(đang hoạt động) và trỏ nó đến một máy chủ Zabbix.

![huydv](/images/Screenshot_27.png)

Chức năng đăng ký tự động rất tiện dụng để giám sát tự động các nodes Cloud mới. Ngay sau khi bạn có một nút mới trong CLoud, Zabbix sẽ tự động bắt đầu thu thập dữ liệu về hiệu suất và tính khả dụng của nút đó.

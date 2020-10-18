# Host
Máy chủ Zabbix diển hình là thiết bị bạn muốn giám sát(server, Workstation, switches,...)

Tạo máy chủ là một trong những nhiệm vụ giám sát đầu tiên trong Zabbix. Ví dụ: nếu bạn muốn theo dõi một số thông tin từ máy chủ "x". Trước tiên phải tạo một máy chủ và sau dó bạn có thể tìm cách thêm Item để giám sát vào máy chủ đó.

### Configuration host
Thông tin về máy chủ được cấu hình trong Zabbix có sẵn trong:

**Configuration** => **Hosts**

![](/images/Screenshot_49.png)

![](/images/Screenshot_50.png)
|Tham số|Sự miêu tả|
|-|-|
|Host name|Nhập tên máy chủ là duy nhất. Lưu ý: với Zabbix Agent đang chạy trên máy chủ cấu hình, tham số tệp cấu hình Agent Hostname phải có cùng giá trị với host name  được nhập ở đây. Tên trong tham số là cần thiết trong quá trình kiểm tra hoạt động.|
|Visible name|Tên được hiển thị trong lists, maps, etc.|
|Groups|Chọn nhóm máy chủ mà host sở hữu. Host phải thuộc ít nhất một nhóm máy chủ.|
|New host group|Một nhóm máy chủ mới có thể được tạo và liên kết với host|
|Interfaces|một số loại Interfaces được hỗ trợ cho máy chủ: Agent, SNMP, JMX  và IPMI. Để thêm Interfaces mới nhập `add` và thêm thông tin cho IP/DNS kết nối đến và port info. Lưu ý: không thể xóa các giao diện được sử dụng trong bất kỳ iterm nào và `link Remove` có màu xám|
|IP address|Địa chỉ IP host|
|DNS name|Địa chi DNS host|
|Connect to|Chọn loại tương ứng để Zabbix biết cách sử dụng để lấy dữ liệu từ các Agent|
|Port|Số port UDP/TCP. Giá trị mặc định là 10050 cho Zabbix Agent, 161 cho SNMP Agent. 12344 cho JMX và 623 cho IPMI|
|Default|Kiểm tra để đặt Interfaces mặc định|
|Monitored by proxy|Host có thể được giám sát bởi Zabbix server hoặc một trong các Zabbix Proxy.|
### Configuration Templates
![](/images/Screenshot_51.png)

Cho phép bạn liên kết các Templates với host. Tất cả các thành phần(items, trifers, graphs and application) sẽ được kế thừa từ template.

### IPMI

Tab IPMI chứa các thuộc tính quản lý IPMI
|Tham số|Miêu tả|
|-|-|
|Authentication algorithm|Chọn thuật toán xác thực|
|Privilege level|Mức đặc quyền|
|Username|Tên dùng để xác thực|
|Password|Mật khẩu dùng để xác thực|
### Macros
Tab cho phép bạn xác định máy chủ Macros dùng

User Macros có thể được sử dụng trong:
* item names
* Thông số item key
* Tên trigger và miêu tả
* Các tham số và hằng số biểu thức trigger

### Encryption 
Các tab Encryption cho phép bạn yêu cầu mã hóa kết nối tới máy chủ
|Tham số|Miêu tả|
|-|-|
||Các Zabbix server hoặc Proxy kết nối với các Zabbix Agent trên máy chủ: Không mã hóa(mặc định), sử dụng PSK(pre-shared key), hoặc certificate|
||Chọn loại kết nối được phép từ máy chủ(tức là từ agent và sender). Một số kiểu kết nối có thể được chọn cùng một lúc(hữu ích cho việc thử nghiệm và chuyển sang kiểu kết nối khác. Mặc định là không mã hóa|
||Chứng chỉ được xác thực đầu tiên với CA(certificate authority- tổ chức phát hành chứng chỉ). Nếu nó hợp lệ, được ký duyệt bởi CA, thì Issuer có thể được sử dụng để hạn chế hơn nữa CA được phép. Trường này được thiết kế được sử dụng nếu cài đặt zabbix của bạn sử dụng chứng chỉ từ nhiều CA. Nếu trường này trống thì bất kỳ CA nào cũng được chấp nhận.|
||Đối tượng được phép của chứng chỉ. Chứng chỉ được xác thực đầu tiên với CA. Nếu nó hợp lệ được ký bởi CA, thi Subject có thể được sử dụng để chỉ cho phép một giá trị của chuỗi Subject. Nếu trường này trống thì bất kỳ chứng chỉ hợp lệ nào được ký bởi CA đã được cấu hình đều được chấp nhận.|
||Chuỗi nhận dạng Pre-shared key. Không đưa thông tin nhạy cảm vào PSK identity, nó được truyền không được mã hóa qua mạng để thông báo cho người nhạn biết PKS sẽ sử dụng|

## Tạo một host groups
# Bảo mật và xác thực
## Phương pháp xác thực

Giao diện người dùng web Zabbix hỗ trợ một số phương pháp xác thực 
* Internal database- Cơ sở dữ liệu nội bộ
* HTTP basic authentication- Xác thực cơ bản HTTP
* Xác thực LDAP

Nếu LDAP được sử dụng làm phương thức xác thực và nó không khả dụng vì bất cứ lý do gì, các nhóm người dùng vẫn có thể xác thực nội bộ để truy cập giao diện người dùng web Zabbix

## Mã hóa giữa các thành phần Zabbix

![huydv](/images/Screenshot_22.png)

Với hỗ trợ mã hóa, có thể bảo mật thông tin liên lạc giữa các thành phần Zabbix riêng biệt(chẳng hạn như máy chủ Zabbix, proxy, agent và các command plugin) bằng cách sử dụng giao thức Transport Layer Security(TLS)- Bảo mật lớp truyền tải v.1.2. 

Mã hóa dựa trên pre-shared(Khóa chia sẻ trước) và Certificate-based(dựa trên chứng chỉ) được hỗ trợ. Mã hóa là tùy chọn và có thể cấu hình cho các thành phần riêng lẻ.

## User permissions - Phân quyền người dùng
Zabbix có một lược đồ quyền người dùng linh hoạt, có thể được sử dụng hiệu quả để quản lý quyền người dùng trong một lần cài đặt Zabbix hoặc trong một môi trường phân tán
## User types
Zabbix hỗ trợ một số kiểu người dùng. Kiểu người dùng được sử dụng để xác định quyền truy cập vào chức năng quản trị và chỉ ddingj các quyền mặc định.
|Loại người dùng|Miêu tả|
|-|-|
|Người dùng Zabbix|Người dùng có quyền truy cập vao Menu giám sát. Người dùng không có quyền truy cập vào bất kỳ tài nguyên nào theo mặc định. Quyền cho các nhóm lưu trữ phải quy định rõ ràng.|
|Admin Zabbix|Người dùng có quyền truy cập vào Giám sát và Cấu hình. Không có quyền truy cập vào các nhóm máy chủ nào theo mặc định. Quyền đối với các nhóm lưu trữ phải được cấp một cách rõ ràng.|
|Admin Super Zabbix|Người dùng có quyền truy cập vào mọi thứ: Giám sát, Cấu hình và Quản trị. Người dùng có quyền truy cập vào đọc ghi đối với tất cả các nhóm máy chủ. Không thể thu hồi quyền bằng cách từ chối quyền truy cập vào các nhóm máy chủ cụ thể|

## Cấp quyền truy cập cho máy chủ
Quyền được cấp cho các nhóm người dùng ở cấp độ nhóm máy chủ. Dó đó, quyền truy cập vào máy chủ phụ thuộc vào loại quyeenfmaf nhóm người dùng có đối với nhóm máy chủ mà máy chủ đó thuộc về. 

Có 3 loại quyền để truy cập máy chủ hoặc nhóm máy chủ:
* Read-write – a read-write access; Quyền truy cập được phép đọc ghi dữ liệu
* Read-only – a read-only access; Quyền truy cập chỉ được phép đọc
* Deny – access denied; Từ chối quyền truy cập

**RW/RO/denied**
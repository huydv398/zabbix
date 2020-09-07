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
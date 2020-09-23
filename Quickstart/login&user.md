# Đăng nhập và thiết lập người dùng trong hệ thống

## Login
![](/images/Screenshot_41.png)

Đây là màn hình "Welcome" của Zabbix. Khi đăng nhập lần đầu. Nhập tên người dùng là **Admin** và mật khẩu là **zabbix** để đăng nhập với tư cách là superuser.

Chỉ Superuser mới có quyền truy cập vào **Configuration** và **Administration**

![](/images/Screenshot_42.png)

### Ngăn chặn tấn công BRUTE FORCE 
Trong trường hợp 5 lần đăng nhập không thành công liên tiếp, giao diện Zabbix sẽ tạm dừng trong 30 giây để ngăn chặn các tấn công.

Địa chỉ IP của lần đăng nhập không thành công sẽ được hiển thị khi đăng nhập thành công.

## Adding User 

Để xem thông tin về các user,

**Administration** => **Users** 

![](/images/Screenshot_43.png)

Ban đầu chỉ có 2 người dùng được xác định trong Zabbix:
* Admin: Zabbix Superuser, có đầy đủ các quyền.
* Guest: là người dùng mặc định đặc biệt. Nếu bạn chưa đăng nhập, bạn đang truy cập Zabbix với quyền 'guest' và không có quyền đối với các đối tượng Zabbix.

### Thêm người dùng mới
click **Create user**

![](/images/Screenshot_44.png)

Điền đầy đủ thông tin cho User mới:

![](/images/Screenshot_45.png)

Mặc định, người dùng không có phương thức thông báo nào được xác định cho họ. Để tạo chuyển đến tab **Media**

![](/images/Screenshot_47.png)

Chỉ định khoảng thời gian hoạt động của phương thức cảnh báo 

### Thêm quyền cho User 
Theo mặc định, Người dùng mới không có quyền truy cập máy chủ. Để cấp quyền người dùng, hãy chọn nhóm cho user 

![](/images/Screenshot_48.png)
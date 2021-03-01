# Cấu hình Zabbix Server gửi cảnh báo qua Gmail 

Việc gửi cảnh báo tình trạng của hệ thống là một điều không thể thiếu đối với công cụ Monitor hiện nay. Chúng ta có rất nhiều hình thức để gửi cảnh báo qua các phương tiện truyền thông và Email là một trong số nhưng phương tiện truyền thông phổ biến nhất.

## Mục lục
[Mô hình triển khai](#mohinh)
[Cấu hình Postfix](#Postfix)
[Cấu hình trên CentOS-7](#cent7)
[Test gửi cảnh báo](#test)


## Mô hình triển khai

## Cấu hình Postfix

Postfix là là một phần mềm nguồn mở được dùng để gửi mail (Mail ranfer Agent-MTA). Được phát hành bởi IBM với mục tieu thay thế trình gửi mail phổ biến là sendmail. 

Trong bài viết sẽ hướng dẫn cài đặt Postfix để gửi Mail trên CentOS-7.

### Remove Sendmail
Trước tiên cần kiểm tra xem sendmail đã được cài đặt chưa bằng câu lệnh

`rpm -qa | grep sendmail`

Nếu có kết quả trả về chứng tỏ sendmail đã được cài đặt. Ta cần remove nó

`yum remove sendmail*`

Nếu máy không cài đặt sendmail thì cài đặt Postfix

### Install postfix
Cài đặt postfix và một số gói liên quan

`yum -y install postfix cyrus-sasl-plain mailx`

Đặt postfix như MTA mặc định của hệ thống, (MTA tạm hiểu là tác nhân chuyển thư. Đây là dịch vụ xử lý các tin nhắn trực tuyến: chuyển thư từ máy tính đến một nơi khác)

`alternatives --set mta /usr/sbin/postfix`

Nếu câu lệnh bị lỗi và trả về output `/usr/sbin/postfix has not been configured as an alternative for mta` thì thực hiện lệnh sau:

`alternatives --set mta /usr/sbin/sendmail.postfix`

Restart và enable postfix

```
systemctl restart postfix
systemctl enable postfix
```

### Configure Postfix
Mở file `main.cf` để chỉnh sửa

`vi /etc/postfix/main.cf`

Thêm vào cuối file những dòng sau:

```
myhostname = hostname.example.com
relayhost = [smtp.gmail.com]:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-bundle.crt
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
```

### Configure Postfix SASL Credentials
Tạo file `/etc/postfix/sasl_passwd` và thêm vào dòng sau

`[smtp.gmail.com]:587 username:password`

Trong đó:
* username: địa chỉ Email dùng để gửi mail cảnh báo đi
* password: Là password Email dùng để gửi mail cảnh báo đi

Phân quyền cho file vừa tạo:

```
postmap /etc/postfix/sasl_passwd
chown root:postfix /etc/postfix/sasl_passwd*
chmod 640 /etc/postfix/sasl_passwd*
systemctl reload postfix
```

### Cho phép ứng dụng truy cập gmail
Nếu bạn sử dụng gmail làm địa chỉ người gửi thì bạn phải vho phép ứng dụng truy cập gmail của bạn

Đăng nhập Gmail trên URL và tiếp tục chạy tiếp URL sau: https://myaccount.google.com/lesssecureapps

Bật chế độ cho phép ứng dụng truy cập

![Imgur](https://i.imgur.com/o1Phrb4.png)

### Kiểm tra

Kiểm tra lại xem đã gửi mail thành công chưa

`echo "Đã gửi thành công" | mail -s "Mail kiểm tra" huydv398@gmail.com`

![Imgur](https://i.imgur.com/WjXsu8w.png)

Như vậy đã cài đặt thành công Postfix cho Server chuyển xang cài Cảnh báo

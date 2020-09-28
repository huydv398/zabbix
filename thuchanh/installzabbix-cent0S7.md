# Cài đặt Zabbix Server lên CentOS7

## Mô hình
## Chuẩn bị
## Lưu ý khi cài đặt
* Cài đặt kho lưu trữ
* Cài đặt server/agent/Frontend
* Tạo cơ sở dữ liệu ban đầu, nhập dữ liệu ban đầu
* Cấu hình cơ sở dữ liệu cho Zabbix
* Cấu hình PHP cho giao diện người dùng Zabbix(Zabbix Frontend)
* Khởi động các process server/agent
* Cấu hình giao diện người dùng Zabbix
## Cài đặt
Cài đặt **LAMP** [tại đây](https://github.com/huydv398/Linux-tutorial/blob/master/CentOS-7/LAMP.md)

Cài đặt Kho lưu trữ Zabbix:

```
rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
yum clean all
```
Cài đặt Zabbix server và Agent

`yum install -y zabbix-server-mysql zabbix-agent`

Cài đặt Zabbix frontend

`yum-config-manager --enable rhel-server-rhscl-7-rpms`

Chỉnh sửa file `/etc/yum.repos.d/zabbix.repo` và enable  zabbix-frontend repository.

`vi /etc/yum.repos.d/zabbix.repo`

chỉnh sửa
```
[zabbix-frontend]
...
enabled=0
...
```

Sửa `0` thành `1`

```
[zabbix-frontend]
...
enabled=1
...
```

![](/images/Screenshot_30.png)

Lưu và thoát
### Install Zabbix frontend packages.

`yum install -y zabbix-web-mysql-scl zabbix-apache-conf-scl`

Đối với một số máy tới bước này gặp lỗi như sau:
#### Error: Package: zabbix-web-deps-scl-5.0.3-1.el7.noarch (zabbix-frontend)

![](/images/Screenshot_31.png)

Cách sử lý :
* Cài đặt kho lưu trữ CentOS SCLo RH:
    * `yum install -y centos-release-scl-rh`
* Cài đặt gói rpm rh-php72-php-common:
    * `yum install -y rh-php72-php-common`
### Cài đặt Zabbix Frontend packages.

` yum install -y zabbix-web-mysql-scl zabbix-apache-conf-scl`

Chạy lại lệnh
### Tạo database ban đầu 
```
mysql -uroot -p
< nhập password của user root mysql`

mysql> create database [Name_database] character set utf8 collate utf8_bin;
mysql> create user [Username]@localhost identified by '[password]';
mysql> grant all privileges on [Username].* to zabbix@localhost;
mysql> quit;
```

Trong đó:

* `mysql -uroot -p`: Đăng nhập vào mysql để tạo cơ sở dữ liệu ban đầu cho zabbix
* `[Name_database]`: Tên database mà bạn muốn đặt
* `[Username]`và `[password]`: Thay đổi bằng tên user và pass mà bạn muốn đặt cho zabbix.

```
[root@cmk-server ~]# mysql -uroot -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 5.5.65-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database zabbix character set utf8 collate utf8_bin;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]>  create user huyzabbix@localhost identified by 'huydv';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all privileges on zabbix.* to huyzabbix@localhost;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> exit
Bye
```
* Database name: `zabbix`
* Username: `huyzabbix`
* password: `huydv`
* Phân quyền: có quyền đối với database `zabbix.*`

Trên máy chủ lưu trữ Zabbix nhập lược đồ và dữ liệu ban đầu. Bạn sẽ được nhắc nhập mật khẩu mới tạo của mình.

`zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -u[Username] -p [Database name]`

![](/images/Screenshot_35.png)

### Cấu hình cho máy chủ Zabbix
`vi /etc/zabbix/zabbix_server.conf`

```
DBPassword=[password]
```


![](/images/Screenshot_36.png)
Lưu và thoát

### Cấu hình PHP cho giao diện người dùng Zabbix
Chỉnh sửa tệp

`vi /etc/opt/rh/rh-php72/php-fpm.d/zabbix.conf`

bỏ ghhi chú và điền múi giờ phù hợp.

`; php_value[date.timezone] = Europe/Riga`

Sửa thành

`php_value[date.timezone] = Asia/Ho_Chi_Minh`

Lưu và thoát

### Khởi động Zabbix server và agent process
Khởi động và cho nó khởi động cùng hệ thống khi reboot
```
systemctl restart zabbix-server zabbix-agent httpd rh-php72-php-fpm
systemctl enable zabbix-server zabbix-agent httpd rh-php72-php-fpm
```

### Cấu hình Zabbix Frontend
**Bước 1:**

Kết nối đến giao diện web mới được cài đặt.

`http://server_ip_or_name/zabbix`

Giao diện sau khi hoàn thành các bước cài đặt:

![](/images/Screenshot_32.png)

**Bước 2:** Đảm bảo rằng tất cả các điều kiện của phần mềm được đáp ứng.
![](/images/Screenshot_33.png)

**Bước 3:** Nhập thông tin để kết nối cơ sở dữ liệu. Cơ sở dữ liệu Zabbix đã khởi tạo trước đó:

![](/images/Screenshot_34.png)

Bước 4: Nhâp tên cho máy chủ, Tên này sẽ được hiển thị trên thanh menu và tiêu đề trang

![](/images/Screenshot_37.png)

Bước 5: Xem lại tóm tắt cài đặt:

![](/images/Screenshot_38.png)

Bước 6: Hoàn thành cài đặt Zabbix:

![](/images/Screenshot_39.png)

Bươc 7: Giao diện người dùng Zabbix đã sẵn sàng. Tên người dùng là **Admin**, mật khẩu là **zabbix**


Đây là giao diện tổng quan của Phần mềm giám sát mã nguồn mở Zabbix. Chúc các bạn thực hiện thành công

![](/images/Screenshot_40.png)

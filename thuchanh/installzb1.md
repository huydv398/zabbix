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
### Cài đặt **LAMP** 
### 1.Cài đặt Linux
Là cài đặt hệ điều hành hay môi trường để các phần mềm hoạt động. Linux có nhiều bản phân phối như Debian, RedHat,Ubuntu,... Trong bài viết này sử dụng CentOS-7.
### 2.Cài đặt Apache 
* Để cài đặt, trên cửa sổ terminal gõ lệnh:

`yum install -y httpd`

* Cài xong, tiến hành khởi động service:

` systemctl start httpd`

` systemctl enable httpd`

* Kiểm tra trạng thái hoạt động trên server:

`systemctl status httpd`

![Imgur](https://i.imgur.com/Yf1md5D.png)

* Kiểm tra trạng thái hoạt động trên web:

`[Địa chỉ IP Server]`

* Nếu sử dụng hệ điều hành trên máy ảo, tắt firewall để có thể truy cập trên browser máy thực:

`systemctl stop firewalld`


### 3.Cài hệ quản trị cơ sở dữ liệu
`yum remove mariadb-server`

Thêm MariaDB YUM repository vào CentOS 7
```
cat <<EOF | sudo tee /etc/yum.repos.d/MariaDB.repo
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
EOF
```
Clean yum cache index:

`yum makecache fast`

Trên thực tế với LAMP, bạn có thể sử dụng MySQL hoặc Mariadb.

* Trên cửa sổ Terminal, tiến hành cài Mariadb:

`yum -y install MariaDB-server MariaDB-client`
* Kiểm tra phiêm bản sau khi cài

`rpm -qi MariaDB-server`
* Tiến hành khởi động mariadb service: 
```
systemctl start mariadb 
systemctl enable --now mariadb
```

* Cài lại mật khẩu cho root của cơ sở dữ liệu:

`mysql_secure_installation`

* Thiết lập một số cấu hình tại bước này như sau:

* **Enter** khi đã có mật khẩu:

![Imgur](https://i.imgur.com/0kUCDRx.png)

* **Enter** Khi chưa có mật khẩu:

![Imgur](https://i.imgur.com/Jl2d0je.png)

![Imgur](https://i.imgur.com/M3zy1lG.png)

1: Nhấn `y` để cài mật khẩu mới cho root

 2: Nhập mật khẩu mới cho root

 3: Nhập lại mật khẩu cho root

* Nhập `y` xóa bỏ các User khác:

![Imgur](https://i.imgur.com/o5QZlJI.png)

* Không cho phép root đăng nhập từ xa:

![Imgur](https://i.imgur.com/JuAa7ap.png)

* Xóa bỏ database:

![Imgur](https://i.imgur.com/7OLrFFG.png)

* Khởi chạy lại bảng Privileges(Bảng phân quyền)

![Imgur](https://i.imgur.com/252vBxj.png)

Sau khi thiết lập, Kích hoạt mariadb để khởi động cùng hệ thống

### 4.Cài đặt PHP
#### PHP 7.2
* Cài đặt phiên bản mới nhất.Tiến hành thêm kho Remi CentOS:

`yum install -y epel-release`

`yum update -y epel-release`

`rpm -Uvh https://rpms.remirepo.net/enterprise/remi-release-7.rpm`

* Cài Yum-utils vì cần tiện ích yum-config-manager để cài đặt:

`yum -y install yum-utils`

Tiến hành cài đặt PHP. Ở đây ta cần lưu ý về phiên bản cài đặt như sau:

* Ver 7.0:
`yum-config-manager --enable remi-php70`
* Ver 7.1:
`yum-config-manager --enable remi-php71`
* Ver 7.2:
`yum-config-manager --enable remi-php72`
* Ver 7.3:
`yum-config-manager --enable remi-php73`

* Cài đặt các Option php:

`yum -y install php php-opcache php-mysql`

* Tắt firewall và selinux
```
sudo systemctl disable firewalld
sudo systemctl stop firewalld
sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
setenforce 0
```
* Tiến hành kiểm tra kết quả. Ta thêm file sau:

`echo "<?php phpinfo(); ?>" > /var/www/html/info.php`

* Sau khi cài đặt , thực hiện restart lại Apache:

` systemctl restart httpd`

* Vào trình duyệt, gỗ trên thanh URL địa chỉ như sau:

`[Địa chỉ IP]/info.php`



## Cài đặt Zabbix
Cài đặt Kho lưu trữ Zabbix:

```
rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
yum clean all
```
Cài đặt Zabbix server và Agent

`yum install -y zabbix-server-mysql zabbix-agent  zabbix-get`

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
* Password: `huydv`
* Phân quyền: có quyền đối với database `zabbix.*`

Trên máy chủ lưu trữ Zabbix nhập lược đồ và dữ liệu ban đầu. Bạn sẽ được nhắc nhập mật khẩu mới tạo của mình.

`zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -u[Username] -p [Database name]`

![](/images/Screenshot_35.png)

### Cấu hình cho máy chủ Zabbix
`vi /etc/zabbix/zabbix_server.conf`

```
DBHost=localhost
DBName=[Database name]
DBUser=[Username]
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

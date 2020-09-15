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

```rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/7/x86_64/zabbix-release-5.0-1.el7.noarch.rpm
yum clean all
```
Cài đặt Zabbix server và Agent

`yum install zabbix-server-mysql zabbix-agent`
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

Cài đặt Zabbix Frontend packages.

` yum install zabbix-web-mysql-scl zabbix-apache-conf-scl`

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
* 

### Cấu hình PHP cho giao diện người dùng Zabbix
Chỉnh sửa tệp

`vi /etc/opt/rh/rh-php72/php-fpm.d/zabbix.conf`

bỏ ghhi chú và điền múi giờ phù hợp.
### Khởi động Zabbix server và agent process
Khởi động và cho nó khởi động cùng hệ thống khi reboot
```
systemctl restart zabbix-server zabbix-agent httpd rh-php72-php-fpm
systemctl enable zabbix-server zabbix-agent httpd rh-php72-php-fpm
```

### Cấu hình Zabbix Frontend
Kết nối đến giao diện web mới được cài đặt.

`http://server_ip_or_name/zabbix`


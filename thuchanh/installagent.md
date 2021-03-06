# Cài đặt Zabbix Agent lên CentOS-7 và Ubuntu18.04
Zabbix Agent thu thập dữ liệu số liệu như CPU utilization, CPU Load memory and disk utilization và gửi nó đến máy chủ Zabbix server để trực quan quan
## Điều kiện tiên quyết 
Đảm bảo rằng máy chủ phải được cài đặt CentOS-7 hoặc Ubuntu18.04 , sử dụng bằng quyền `root` hoặc `sudo`

Máy chủ phải được kết nối ra môi trường Internet.

## Bước 1 Add Zabbix repository

* Với Ubuntu 18.04:

```
wget https://repo.zabbix.com/zabbix/5.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.0-1%2Bbionic_all.deb

dpkg -i zabbix-release_5.0-1+bionic_all.deb

apt update
```

* Với CentOS-7:

`rpm -ivh https://repo.zabbix.com/zabbix/5.1/rhel/7/x86_64/zabbix-release-5.1-1.el7.noarch.rpm`
## Bước 2 Cài đặt Zabbix agent
* Với Ubuntu 18.04:

`apt install zabbix-agent`

* Với CentOS-7:

`yum install -y zabbix-agent`   
## Bước 3 Cấu hình Zabbix
Chỉnh sửa file cấu hình:

`vi /etc/zabbix/zabbix_agentd.conf`

Thực hiện sửa đổi với các thuộc tính sau:

```
Server= <Thay đổi IP Zabbix server>
ServerActive= <Thay đổi IP Zabbix server>
Hostname= <Tên Zabbix server>
```
## Cấu hình tường lửa cho Zabbix Agent
Zabbix Agent phải có khả năng giao tiếp qua tTCP port 10050
* Với CentOS-7:

```
firewall-cmd --permanent --zone=public --add-port=10050/tcp
firewall-cmd --reload
```
* Với Ubuntu/ Debian:

`sudo ufw allow 10050/tcp`
## Restart và Enable Zabbix agent 
Để thực hiện các thay đổi được thực hiện đối với tệp cấu hình, khởi động lại zabbix agent và kích hoạt trong khi khởi động.

```
systemctl restart zabbix-agent

systemctl enable zabbix-agent
```
Để xác minh rằng zabbix agent đang chạy:

`systemctl status zabbix-agent`

## Kiểm tra việc cài đặt. 

### Sang máy zabbix server thực hiện lệnh

`zabbix_get -s <ZABBIX_AGENT_IP> -k agent.version`

![](/images/Screenshot_52.png)

## Tạo host trên Zabbix web 
`Configuration` -> `Host` -> `Create host`

![](/images/Screenshot_53.png)

Điền thông tin cho Host:

![](/images/Screenshot_54.png)

Chọn template cho host:

![](/images/Screenshot_55.png)
![](/images/Screenshot_56.png)
![](/images/Screenshot_57.png)

Chọn **Add** để thêm host.

Đợi khoảng 1 phút rồi load lại web:

* Availability : **ZBX**- Host đã được add thành công và có thể add thêm các monitor options              

![](/images/Screenshot_58.png)
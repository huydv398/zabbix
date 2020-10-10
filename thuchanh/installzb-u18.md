# Giám sát Server Ubuntu 1804 bằng Zabbix Agent
Cài đặt Agent lên server 

Tìm Agent tại đây: https://repo.zabbix.com/zabbix/5.0/

```
wget https://repo.zabbix.com/zabbix/5.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.0-1%2Bbionic_all.deb

dpkg -i zabbix-release_5.0-1+bionic_all.deb
apt-get update
apt-get install zabbix-agent -y
```
## Cấu hình file Config

`vi /etc/zabbix/zabbix_agentd.conf `

Sửa dòng sau:

```
Server=<IP_ZABBIX_SERVER>
ServerActive=<IP_ZABBIX_SERVER>
Hostname=<ZABBIX_SERVER_HOSTNAME>
```


Ví dụ:

```
Server=10.10.34.114
ServerActive=10.10.34.114
Hostname=zabbix
```

Mở port 10050:
```
root@u18srv1:~# ufw allow 10050
Rules updated
Rules updated (v6)
```

Khởi động dịch vụ:

```
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

Kiểm tra, truy cập Zabbix Server:

`zabbix_get -s [ZABBIX_AGENT_IP] -k agent.version`

```
zabbix_get -s 10.10.35.115 -k agent.version
5.0.4
```
## Add host trên Web:
Tạo host mới

![](/images/Screenshot_59.png)

Điền thông tin cho host:

![](/images/Screenshot_60.png)

Chọn Template cho host:

![](/images/Screenshot_61.png)

Khi ZBX hiện nên màu xanh thì thành công:

![](/images/Screenshot_62.png)

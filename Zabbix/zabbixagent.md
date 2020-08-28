# Zabbix Agent 
Bản chất của Zabbix, được phát triển trên ngôn ngữ lập trình C, có thể hỗ trợ trên các nền tảng khác nhau. Đồng thời thu thập dữ liệu như mức sử dụng CPU, Memory, Disk, Network interface usage from a device.

![huydv](../images/Screenshot_13.png)

## Passive (polling) and Active checks (trapping) Support 
Zabbix thực hiện kiểm tra dựa trên thời gian, cũng có thể lên lịch thời gian cự thể.
### Passive Check (polling)
* Zabbix server (hoặc Proxy) yêu cầu cầu các giá trị từ Zabbix agent
* Agent xử lý yêu cầu và trả về giá trị cho Zabbix
### Active checks (trapping)
* Zabbix agent yêu cầu từ Zabbix một danh sách Active checks cho agent, để agent chủ động kiểm tra hoạt động của danh sách mà Zabbix đưa ra.
* Agent gửi kết quả theo định kỳ cho Zabbix

# Chức năng của Agent
|Device|Agent|Ghi chú|
|-|-|-|
|Network|Packet/bytes transfered||
|-|Errors/dropped packets|-|
||Collisions||
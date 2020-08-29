# Zabbix Agent 

Bản chất của Zabbix, được phát triển trên ngôn ngữ lập trình C, có thể hỗ trợ trên các nền tảng khác nhau. Đồng thời thu thập dữ liệu như mức sử dụng CPU, Memory, Disk, Network interface sử dụng từ một thiết bị.

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
||Errors/dropped packets||
||Collisions||
|CPU|Load average||
||CPU idle/usage||
||CPU utilization data per individual process||
|Memory|Free/used memory|RAM đã sử dụng và trống|
||Swap/pagefile utilization||
|Disk|Space free/used|Dung lượng disk|
||Read and write I/O||
|Service|Process status|Trạng thái các Process đang hoạt động|
||Process memory usage|Các Process đang sử dụng bộ nhớ ram|
||Service status|Giám sát các dịch vụ như http, ssh , ntp, mysql, ftp,...|
||Windows service status|Giám sát các trạng thái dịch vụ của Window|
||DNS resolution||
||TCP connectivity|Các kết nối TCP|
||TCP response time|Thời gian phản hồi TCP|
|File|File size/time|Thời gian sử dụng và kích thước của Fiole|
||Exits|Sự tồn tại của file|
||Checksum|Sự thay đổi của file|
||MD5 hash||
||RegExp search||
|Log|Text log||
||Window Eventlog||
|**Khác**|Thời gian hoạt động của hệ thống||
||Giờ hệ thống||
||Người dùng đã kết nối||
||Bộ đếm hiệu suất(window)||

## Log Monitoring
Hỗ trợ giám sát ký tự log và Window Event Log là một chức năng của Zabbix Agent

Có thể vẽ biểu đồ dữ liệu từ các log items,khi khả năng trích xuất nội dung cụ thể được sử dụng

Log được Zabbix agent phân tích liên tục và khi một mục tìm kiếm xác định được tìm thấy, Zabbix được thông báo và thực hiện một số hành động hoặc tự động gửi thông báo đến người dùng hoặc nhóm
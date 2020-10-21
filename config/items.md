# Tổng quan
Item thu thập dữ liệu từ một host.

Khi bạn đã cấu hình host, bạn cần thêm một số Item để bắt đầu nhận  dữ liệu thực tế.

1 item là 1 metric riêng biệt. Một cách nhanh chóng để thêm nhiều item là đính kèm 1 template được xác định trước vào máy chủ. Tuy nhiên có thể tối ưu hóa hệ thống, bạn có thể cần phải tinh chỉnh các template để có nhiều Item và theo dõi thường xuyên nếu thực sự cần thiết.

Ví dụ thêm 1 mẫu:

![](/images/Screenshot_67.png)

Trong mỗi Item riêng lẻ, bạn chỉ định loại dữ liệu nào sẽ được thu thập từ host.

Vì mục đích đó, bạn sử dụng `itemkey`. Do đó, một mục có tên key là `system.cpu.lod` sẽ thu thập dữ liệu của **processor load**., khi một item có tên `net.if.in` sẽ thu thập thông tin lưu lượng đến.

Để xác định các tham số khác với key, bạn bao gồm các tham số đó trong dấu ngoặc vuông sau `key name`. Do đó, `system.cpu.load[avg5]` sẽ trả về mức trung bình tải 5 phút qua, trong khi `net.if.in[eth0]` sẽ hiện thị giao diện đến trong interface eth0.

Tiến hành tạo và cấu hình một Item
## Creating an Item
### Tổng quan 

Trên Zabbix Frontend: `Configuration` → `Hosts`

### Cấu hình
Tab **Item** chứa các thuộc tính chung của Item

![](/images/Screenshot_68.png)

|Tham số|Miêu tả|
|-|-|
|Name|Tên Item. Lưu ý rằng việc sử dụng vị trí macros ($1, $2...$9- tham chiếu đến tham số thứ nhất, thứ hai// thứ 9 của item key) Hiện không được dùng nữa.</br> Ví dụ, Free disk space on $1. nếu item key là "`vfs.fs.size[/,free]`", mô tả sẽ tự động thay đổi "**Free disk space on /**" |
|Type|Loại Item. Xem các phần Item [type](/config/info/Item-type.md)|
|Key|Tối đa 2048 ký tự.</br>Các Item được hỗ trợ [Item type](/config/info/Item-type.md).</br>Item key phải là duy nhất trong một máy chủ.</br>Nếu khóa là ` Zabbix Agent`,`Zabbix agent (active)`, `Simple check` hoặc `Zabbix aggregate`, Giá trị của key phải được hỗ trợ bởi Zabbix agent hoặc zabbix server  |
|Host interface|Chọn Host interface.</br> Trường này có sẵn khi chỉnh sửa một item ở cấp độ host|
|Type of infomation |Loại dữ liệu được lưu trữ trong cơ sở dữ liệu sau khi chuyển đổi, nếu có:</br> **Numeric (unsigned)**- 64 bit số nguyên không dấu</br> **Numeric (float)**- số nguyên và số dấu phẩy động</br>**Character**- Dữ liệu văn bản ngắn</br>**Log**- Dữ liệu văn bản dài với các thuộc tính liên quan đến log(timestamp, source, mức độ nghiêm trong, logeventid ) |
|Units|Nếu một unit được cài đặt, Zabbix sẽ xử lý bài đăng  vào giá trị nhạn được và hiển thị nó với mã bưu chính unit đã đặt.</br> Mặc định|
|Update interval|Lấy giá trị Item sau N giây. Khoảng thời gian tối đa cho phép là 1 ngày- 86400 giây|
|custom intervals|Bạn có thể tùy chỉnh các quy tắc để tìm kiếm Item:<br> **Flexible**- Tạo một ngoại lệ cho khoản thời gian cập nhật(Update interval) <br>**Scheduling**- Tạo một lịch biểu tùy chỉnh |
|History storage period |Chọn 1 trong 2 trạng thái:<br> **Do not keep history** item history không được lưu trữ. Hữu ích cho các item chính nếu các item phụ thuộc cần lưu giữ lịch sử<br>**Storage period**-giai đoạn lưu trữ: Chỉ định thời hạn lưu trữ lịch sử chi tiết trong cơ sở dữ liệu( 1 giờ đến 25 năm). Dữ liệu cũ hơn sẽ bị loại bỏ.  |
|Trend storage period|Chọn 1 trong 2 tùy chỉnh:<br>**Do not keep trends**: Xu hướng không được lưu trữ<br>**Storage period**: Giai đoạn lưu trữ- Chỉ định khoảng thời gian lưu giữ lịch sử tổng hợp trong cơ sở dữ liệu |
|Show value|Áp dụng ánh xạ giá trị cho Item này. Value mapping không thay đổi các giá trị đã nhận, nó chỉ để hiển thị dữ liệu.<br>Nó hoạt động với các mục Numeric (unsigned), Numeric (float) và Character. Ví dụ: “Windows service states”.|
|Log time fomat|Chỉ áp dụng cho các item thuộc loại log.<br>y: Year (1970-2038)<br>M: Month (01-12)<br>d: Day (01-31)<br>h: Hour (00-23)<br>m: Minute (00-59)<br>s: Second (00-59) |
|New application|Nhập tên Applications mới cho Item|
|Applications|Link liên kết với một hoặc nhiều mục hiện có|
|Populates host inventory field|Bạn có thể chọn trường inventory trên host mà giá trị của item sẽ điền. Điều này hoạt động nếu số lượng automatic inventory được bật cho host. <br> Trường này không khả dụng nếu loại thông tin được đặt thành **Log**|
|Description|Nhập mô tả cho Item|
|Enabled|Đánh dấu vào checkbox để bật item để item đó sẽ được xử lý.|

## Kiểm tra
Có thể kiểm tra một item nếu được cấu hình đúng, đổi lại sẽ nhận được giá trị thực. Kiểm tra có thể xảy ra nhay cả trước khi một item được lưu

Testing có sẵn cho các template item item prototypes và các quy tắc discovery cấp thấp. Test không có sẵn cho các mục đang hoạt động.

Kiểm tra các mục có sẵn cho các loại mục thụ động sau:

* Zabbix agent
* SNMP agent (v1, v2, v3)
* IPMI agent
* SSH checks
* Telnet checks
* JMX agent
* Simple checks (except icmpping*, vmware.* items)
* Zabbix internal
* Zabbix aggregate
* Calculated items
* External checks
* Database monitor
* HTTP agent

Để kiểm tra một Item, click Test
![](/images/Screenshot_69.png)

Biểu mẫu kiểm tra Item có các trường cho các thông số máy chủ được yêu cầu. Các trường này nhận biết ngữ cảnh: 
* Các giá trị được điền trước khi có thể, tức là đối với các item yêu cầu Agent, bằng cách lấy thông tin từ interface của host đã chọn
* Các giá trị phải được điền thủ công cho các template
* Các trường bị disable khi không cần thiết  trong ngữ cảnh của item(ví dụ: trường địa chỉ máy chủ bị vô hiệu hóa đối với các mục được tính toán và tổng hợp, trường proxy vị tắt đối với các item đã được tính toán)

Để kiểm tra Item, click Get value

![](/images/Screenshot_70.png)

Nếu giá trị được truy xuất thành công, nó sẽ điền vào trường value. di chuyển đến giá trị  hiện tại(nếu có) sang trường Previous value đồng thời tính giá trị trước đó.

![](/images/Screenshot_71.png)

Nếu cấu hình không chính xác, một thông báo lỗi sẽ hiển thị mo tả nguyên nhân có thể.

Như hình bên dưới mình đã nhập thông tin sai cho interface

![](/images/Screenshot_72.png)

## Các nút 
![](/images/Screenshot_73.png)
* Add- Thêm Item. Add các item mới
* update- Cập nhật các thuộc tính của Item
* Clone- Tạo ra một bản sao với thuộc tính của bản hiện tại
* Execute now- Thực hiện kiểm tra giá trị Item ngay lập tức. Chỉ hỗ trợ kiểm tra thụ động Passive. Lưu ý rằng khi kiểm tra, cache config sẽ không được update, do đó giá trị sẽ không phản ánh những gì thay đổi gần đây đối với cấu hình item.
* Test- Kiểm tra xem cấu hình Item có chính xác không bằng cách nhận một giá trị 
* Clear history and trends- xóa lịch sử Item và xu hướng
* Delete- xóa Item
* Cancel- hủy chỉnh sửa các thuộc tính của Item.

## Giới hạn dữ liệu văn bản
Giới hạn dữ liệu văn bản phụ thuộc vào phần phự trợ cơ sở dữ liệu. Trước khi lưu trữ các giá trị trong cơ sở dữ liệu, chúng được cắt bớt để phù hợp với giới hạn loại giá trị cơ sở dữ liệu:

![](/images/Screenshot_73.png)


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

![](/images/Screensot_68.png)

|Tham số|Miêu tả|
|-|-|
|Name|Tên Item. Lưu ý rằng việc sử dụng vị trí macros ($1, $2...$9- tham chiếu đến tham số thứ nhất, thứ hai// thứ 9 của item key) Hiện không được dùng nữa.</br> Ví dụ, Free disk space on $1. nếu item key là "`vfs.fs.size[/,free]`", mô tả sẽ tự động thay đổi "**Free disk space on /**" |
|Type|Loại Item. Xem các phần Item [type](/config/info/Item-type.md)|
|Key|Tối đa 2048 ký tự. Các Item được hỗ trợ [Item type](/config/info/Item-type.md). Item key phải là duy nhất trong một máy chủ. Nếu khóa là ` Zabbix Agent`,`Zabbix agent (active)`, `Simple check` hoặc `Zabbix aggregate`, Giá trị của key phải được hỗ trợ bởi Zabbix agent hoặc zabbix server  |
|Host interface|Chọn Host interface. Trường này có sẵn khi chỉnh sửa một item ở cấp độ host|
|type of infomation |Loại dữ liệu được lưu trữ trong cơ sở dữ liệu sau khi chuyển đổi, nếu có: **Numeric (unsigned)**- 64 bit số nguyên không dấu, **Numeric (float)**- số nguyên và số dấu phẩy động, **Character**- Dữ liệu văn bản ngắn, **Log**- Dữ liệu văn bản dài với các thuộc tính liên quan đến log(timestamp, source, mức độ nghiêm trong ) |
|Units||
|Update interval||
|custom intervals||
|History storage period ||
|Trend storage period||
|Show value||
|Log time fomat||
|New application||
|Applications||
|Populates host inventory field||
|Description||
|Enabled||

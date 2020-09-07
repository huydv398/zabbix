# Thông báo
**Được thông báo trong trường hợp có bất kỳ vấn đề nào.**

Thông báo cho những người có trách nhiệm về các sự kiện đã xảy ra bằng nhiều kênh và tùy chọn khác nhau:
* Gửi Tin nhắn
* Để Zabbix tự động khắc phục sự cố
* Báo cáo sự cố theo các mức dịch vụ linh hoạt do người dùng xác định
* Tùy chỉnh tin nhắn dựa trên vai trò của người nhận
* Tùy chỉnh thông báo với thời gian chạy và các Thông tin Inventory

Giữ bạn khỏi hàng nghìn thông báo lặp đi lặp lại và tạp trung vào nguyên nhân gốc rễ của sự cố với cơ chế tương quan sự kiện Zabbix

![huydv](/images/Screenshot_20.png)

Zabbix cung cấp quy trình làm việc hoàn chỉnh: gửi thông báo, cho phép xác nhận thông tin đã nhận, chuyển thông cho người khác và khả năng thực hiện hành động.

## Gửi thông báo
Phương thức thông báo:
* Email
* SMS
* Sử dụng cảnh báo tùy chỉnh

Các thông báo có thể đươc viết theo kịch bản. Nội dung thông báo hoàn toàn có thể tùy chỉnh theo ngữ cảnh. Mỗi liên hệ có thể được thông báo cho các cấp độ cụ thể bàng các sử dụng phương tiện được chỉ định vào những ngày và thời gian cụ thể.
## Tùy chỉnh tin nhắn
Thời gian chạy hoặc thông tin Iventory, Thông tin cấu hình và dữ liệu mới nhất có thể được bao gồm trong một tin nhắn thông báo. Một tin nhắn có thể có các trường như:

Tùy chọn tùy chỉnh tin nhắn:
* Ngày và giờ
* Host name
* Giá trị của Item
* Giá trị của Trigger
* Hồ sơ máy chủ
* Lịch sử nâng cấp

## Tùy chỉnh phụ thuộc vào người nhận
Khi gửi thông báo đến người dùng hoặc nhóm người dùng cụ thể, thông báo về cùng một vấn đề có thể được tùy chỉnh để cung cấp một nhóm thông tin khác nhau tùy thuộc vào vai trò của người nhận trong tổ chức

## Thực thi lệnh từ xa
Các lệnh shell có thể được thực thi trên hệ thống từ xa để khác phục tình huống hệ thống có thể bị quá tải hoặc các dịch vụ ngừng hoạt động bình. Lệnh điển hình nhất để sử dụng là khởi động lại máy chủ hoặc các dịch vụ.

Lệnh có thể thực hiện:
* Trên Zabbix server 
* Trên Zabbix agent
* Sử dụng IPMI(Intelligent Platform Management Interface)
* Sử dụng Telnet và SSH

## Báo cáo leo thang- báo cáo phản hồi cho các vấn đề
Báo cáo có chứa một kịch bản đại diện cho một tiến trình để gửi thông báo, trước tiên là cho người nhận ban đầu, sau đó, nếu sự cố vẫn tiếp diễn hoặc không có xác nhận được thực hiện, cho những người nhận khác và thậm chí thực hiện các lệnh khi cần thiết.

Các tùy báo cáo leo thang được hỗ trợ:
* Thông báo ngay cho người dùng về vấn đề mới
* Chủ động thực thi các lệnh từ xa
* Lặp lại sự cố cho đến khi máy chủ được giải quyết
* Lộ trình leo thang khác nhau cho các vấn đề đã được thừa nhận và chưa xác nhận
* Thông báo khôi phục cho tất cả các bên quan tâm
* Không giới hạn bước leo thang

Zabbix cung cấp các quy tắc xây dụng leo thang hiệu quả và cực kỳ linh hoạt. Tùy thuộc vào thiết lập, Zabbix sẽ tự động báo cáo các ván đề chưa được giải quyết và thực hiện các hành động được chỉ định cho mỗi bước báo cáo.

Lịch sử nâng cấp có thể được đưa vào các tin nhắn thông báo, để người nhận biết những gì đang diễn ra và tại sao anh ta lại nhận được tin nhắn này.

## Sự kiện tương đồng
* Nhân bản
* Lọc sự kiện
* Phân tích nguyên nhân gốc

Chỉ nhận thông báo cho các vấn đề gốc

![huydv](/images/Screenshot_21.png)
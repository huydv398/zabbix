# Template
Sử dụng các Template là một cách tuyệt vời để làm việc cho việc bảo trì Zabbix dễ dàng hơn. Một tập hợp các thực thể(items, Triggers, graphs, appplications, screen, discovery rules và các tình huống web) có thể được gán cho 1 template, cho phép quản lý hiệu quả hàng nghìn thiết bị.

## Multiple templates for single host
Một mẫu có thể được liên kết với một số máy chủ. Tất cả items, trigger and graphs của Template sẽ được tự động thêm vào các máy chủ được liên kết. Thay đổi định nghĩa của thực thể mẫu(Item, trigger, graph,etc.) và thay đổi sẽ được áp dụng cho máy host.

![huydv](/images/Screenshot_23.png)

## Các Template lồng nhau

Là một Template bao gồm một hoặc nhiều template khác. Lợi ích của lồng ghép là sau đó bạn chỉ phải liên kết một mẫu với máy chủ lưu trữ và máy chủ lưu trữ sẽ tự động kế thừa các thực thể của các mãu được liên kết.

![huydv](/images/Screenshot_24.png)
## Nhập/ Xuất cấu hình 
Chức năng này của Zabbix cho phép trao đổi hiệu quả các thực thể  cấu hình giữa các hệ thống.

Dữ liệu được xuất ở định dạng XML, dễ đọc và sửa đổi. Các trường hợp sử dụng sẽ bao gồm:
* Chia sẻ các template hoặc bản đồ mạng giữa người dùng, hệ thống hoặc tổ chức
* Chia sẻ các thông số cấu hình.
* Tích hợp với các công cụ của bên thứ ba

Việc sử dụng định dạng XML cho phép tích hợp Zabbix với các công cụ và ứng dụng của bên thứ ba và nhập xuất dữ liệu.

Chức năng này áp dụng cho 3 loại cấu hình chính:
* Hosts and their associated data- Máy chủ lưu trữ và dữ liệu liên quan
* Network maps
* Screens

## Import/Export
### Host 
* Máy chủ lưu trữ và các liên kết của chúng với các Template
* Template
* Các ứng dụng
* Items
* Triggers
* Custom Graphs
* Discovery Rules
* User Macros
### Map
* Full map configuration 
* Tất cả các yếu tố map, bao gồm images, triggers, hosts, hosts groups and maps.
* Tất cả các trình kết nối có dữ liệu liên quan, bao gồm cả lables và chỉ số trạng thái
### Screens
Nhập xuất màn hình Zabbix hỗ trợ tất cả các thành phần màn hình
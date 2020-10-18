# Item
Là một phần dữ liệu cụ thể mà bạn muốn nhận từ máy chủ lưu trữ, một chỉ số dữ liệu.

Trong phần này, bạn sẽ học cách thiết lập 1 Item.

Các Item là cơ sở thu thập dữ liệu trong Zabbix. Không có Item, sẽ không có dữ liệu - bởi vì chỉ một Item xác định một chỉ số duy nhất hoặc dữ liệu nào cần lấy từ máy chủ.

## add Item
Tất cả Item được nhóm xung quanh các máy chủ. Đó là lý do tại sao để cấu cấu mục Item mẫu, Chúng ta vào **Configuration** -> **Host**

Click vào host cần thêm Item;

Create Item:

![](/images/Screenshot_64.png)

Điền thông tin:

![](/images/Screenshot_65.png)

Các trường bắt buộc điền được đánh dấu bằng dấu sao mầu đỏ.

## Các thông tin cần thiết

Name: Là tên mục được hiển thị trong danh sách và các nơi khác

**Key**: Nhập `system.cpu.load` làm giá trị. Đây là tên kỹ thuật của 1 Item xác định loại thông tin sẽ được thu thập. Key cụ thể chỉ là một trong những key được xác định trước đi kèm Zabbix Agent.

**Type of information**: Thuộc tính xác định định dạng của dữ liệu

Khi hoàn thành, click **Add**. Item mới sẽ xuất hiện.
## Xem dữ liệu
Dữ liệu đầu tiên có thể mất 60 để có thể thu thập được. Theo mặc định, đó là tần suất máy chủ đọc các thay đổi cấu hình và chọn các mục Item mới để thực thi.

Nếu bạn không thấy thông tin về Item hãy đảm bảo rằng:
* Bạn đã nhập chính xác các trường của Item như ảnh màn hình bên trên.
* Zabbix Agent và Zabbix server phải ở trạng thái running
* Trạng thái máy chủ Zabiix và biểu tưởng khả dụng phải được hiển thị màu xanh phải được hiển thị màu xanh
* Item phải ở trạng thái đang hoạt động

## Graph
Với mỗi mục đang hoạt động trong một khoảng thời gian, có thể dã đén lúc bạn cần nhìn thấy có gì đó trực quan. Đồ thị đơn giản có sẵn cho bất kỳ mục số được giám sát nào mà không cần bất kỳ cấu hình bổ sung nào. Các đồ thị này được tạo trong thời gian chạy

Chọn **Monitoring** -> **Latest** data và click vào **Graph**

![](/images/Screenshot_66.png)
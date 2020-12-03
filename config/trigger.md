# Tổng quan
Trigger là biểu thức logic "đánh giá" dữ liệu được thu thập bởi các Item cho trạng thái hệ thống hiện tại.

Các biểu thức của trigger cho phép xác định ngưỡng trạng thái của dữ liệu là "có thể chấp nhận được". Do đó, nếu dữ liệu vượt qua trạng thái có thể chấp nhận được, một trigger được kích hoạt- hoặc thay đổi trạng thái thành **Problem**.

Trigger có thể có hai trạng thái sau:

|Value|Miêu tả|
|-|-|
|OK|Đây là trạng thái trigger bình thường|
|PROBLEM|Thông thường thì đã có 1 vấn đề gì đó đã xảy ra. ví dụ, processor quá cao|

Trạng thái của trigger (the expression) được tính toán lại mỗi khi máy chủ Zabbix nhận được giá trị mới là một phần của biểu thức (the expression)

Trigger chỉ được đánh giá dựa trên dữ liệu lịch sử; dữ liệu xu hướng không được xem xét.

Bạn có thể xây dựng một biểu thức trigger với độ khó và phức tạp khác nhau

## Cấu hình Trigger

Để cấu hình trigger:

**Configuration** → **Hosts**

### Thông số cấu hình Trigger

>Chú ý: Tất cả các trường hợp bắt buộc được đánh dấu bằng hoa thị đỏ

![](/images/Screenshot_75.png)

|Tham số|Miêu tả|
|-|-|
|Name|Tên của Trigger. |
|Operational data|Cho phép xác định các chuỗi tùy ý cùng với các macro sẽ tự động giải quyết dữ liệu thời gian thực trong giám giát|
|Severity|Đặt mức độ nghiêm trọng cho trigger|
|Expression|Logical expression- biểu thưc logic: Được sử dụng để xác định các điều kiện của một vấn đề.</br> Problem được tạo ra khi tất cả các điều kiện có trong biểu thức được đáp ứng, TRUE. Sự cố sẽ được giải quyết ngay sau khi biểu thức đánh giá là FALSE, trừ các điều kiện khôi phục bổ sung được chỉ định trong  Recovery expression  |
|OK event generation|**Expression**- OK event được tạo ra biểu thức giống như các sự kiện vấn đề'</br>**Recovery expression**- Được tạo ra nếu biểu thức sự cố đánh giá là (expression evaluates) False và biểu thức khôi phục (expression evaluates) là True</br>**None**- Trigger sẽ không bao giờ trở về trạng thái OK|
|PROBLEM event generation mode|**Single**- một sự kiện duy nhất được tạo khi trigger kích hoạt chuyển xang trạng thái 'Problem' lần đầu tiên</br>**Multiple**- Một sự kiện được tạo dựa trên mọi đánh giá "Problem" của Trigger|

### test biểu thức 
Có thể kiểm tra biểu thức kích đã định cấu hình xem kết quả biểu thức sẽ như thế nào tùy thuộc vào giá trị nhận được.


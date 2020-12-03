# Event trong Zabbix
Một số sự kiện được tạo trong Zabbix
* trigger events- Bất cứ khi nào một trigger thay đổi trạng thái của nó.(OK→PROBLEM→OK)
* discovery events- Khi các máy chủ và dịch vụ được phát hiện
* autoregistration events- Khi các Agent hoạt động được máy chủ tự động đăng ký tự động
* internal events- Khi một Item/ low-level discovery rule chuyển trạng thái không được xác định

Các Event được đánh dấu thời gian và có thể là cơ sở của hành động như gửi EMail,v.v

**Monitoring** → **Problems**: Ở đây bạn có thể nhấp vào ngày và giờ sự kiện để xem chi tiết của một sự kiện.

## Thế hệ Trigger Event
Thay đổi trạng thái của trigger là nguồn sự kiện thường xuyên nhất và quan trọng nhất. Mỗi khi trình kích hoạt thay đổi trạng thái của nó, một sự kiện sẽ được tạo ra. Sự kiện chứa thông tin chi tiết về sự thay đổi của trạng thái trigger- khi nó xảy ra và trạng thái mới là gì.
### PROBLEM EVENTS
PROBLEM EVENTS được tạo ra:
* Khi biểu thức trigger đánh giá là True nếu trigger có trạng thái OK
* Biểu thức của Trigger đánh giá là True nếu quá trình tạo ra sự kiện nhiều vấn đề  được kích hoạt cho Trigger
### OK EVENTS
OK EVENTS đóng các sự kiện sự cố liên quan và có thể được tạo ra bởi 3 thành phần:
* Expression: khi biểu thức được đánh giá là False
* Recovery expression: khi biểu thức được đánh giá là False và Recovery expression Đánh giá là True
* None : events Không bao giờ được tạo. điều này có thể được sử dụng với việc tạo nhiều sự kiện sự cố để chỉ cần gửi thông báo khi có điều gì đó xảy ra.
### EVENT CORRELATION

Tương quan sự kiện là cách để thiết lập quy tắc đóng sự kiện tùy chỉnh

Các quy tắc xác định cách sự kiện sự cố mới được ghép nối với các sự kiện hiện có và cho phép đóng sự kiện mới hoặc các sự kiện dã khớp bằng cách tạo các sự kiện OK tương ứng 

Tương quan sự kiện phải được định cấu hình rất cẩn thận, vì nó có thể ảnh hưởng tiêu cực đến  hiệu suất sử lý sự kiện hoặc nếu bị định cấu hình sai, đóng nhiều sự kiện hơn dự định

1. Luôn giảm phạm vi tương ứng bằng cách đặt một thẻ duy nhất cho sự kiện kiểm soát và sử dụng điều kiện tương quan "thẻ sự kiện mới"
2. đừng quên thêm một điều kiện dựa trên sự kiện cũ khi sử dụng thao tác đóng sự kiện cũ, nếu không tất cả các vấn đề hiện có có thể được đóng
3. Tránh sử dụng các tên thẻ phổ biến được sử dụng bởi các cấu hình tương quan khác nhau.

### TASK MANAGER
Nếu cài đặt 'Allow manual close- cho phép đóng thủ công' được bật cho Trigger, sự bạn có thể đóng các sự kiện sự cố do trigger tạo theo các thủ công. Điều này được thực hiện trong giao diện người dùng khi cập nhật sự cố. EVENTS không được đóng trực tiếp- thay vào đó, một tác vụ 'close events' được tạo, sẽ được trình quản lý tác vụ sử lý ngay. Trình quản lý tác vụ sẽ tạo ra một sự kiện OK tương ứng và sự kiện sự cố sẽ được đóng lại.

## Các nguồn sự kiện khác
### Discovery EVENTS
Zabbix định kỳ quét các dải IP được xác định trong các quy tắc khám phá mạng. Tần xuất kiểm tra có thể định cấu hình cho từng quy tắc riêng lẻ. Khi một máy chủ hoặc 1 dịch vụ được phát hiện, Discovery events sẽ được tạo ra

Zabbix tạo ra các sự kiện sau:
|Event- Sự kiện|Khi được tạo ra|
|-|-|
|Service Up|Mỗi khi Zabbix phát hiện dịch vụ đang hoạt động|
|Service Down|Mỗi khi Zabbix không thể phát hiện dịch vụ|
|Host Up||
|Host Down|Nếu tất cả các dịch vụ không phản hồi|
|Service Discovered|Nếu dịch vụ hoạt động trở lại sau thời gian ngừng hoạt động hoặc được phát hiện lần đầu tiên|
|Service Lost|Nếu dịch vụ bị mất sau khi up|
|Host Discovered|Nếu máy chủ hoạt động trở lại sau thời gian ngừng hoạt động hoặc được phát hiện lần đầu tiên|
|Host Lost|Nếu máy chủ bị mất sau khi lên|
### ACTIVE AGENT AUTO-DISCOVERY EVENTS
Active agent đăng ký tự động tạo các sự kiện trong Zabbix

Nếu được định cấu hình, ACTIVE AGENT AUTO-DISCOVERY EVENTS sẽ được tạo khi Active agent không xác định trước đó yêu cầu kiểm tra  hoặc nếu siêu dữ liệu máy chủ đã thay đổi. Máy chủ thêm một host đăng ký tự động mới, sử dụng địa chỉ IP đã nhận và cổng của agent.

### INTERNAL EVENTS- Sự kiện nội bộ

Các sự kiện nội bộ khi xảy ra:
* Một Item thay đổi trạng thái từ 'normal' xang 'unsupported'
* Một Item thay đổi trạng thái từ 'unsupported' xang 'normal'
*  low-level discovery rule thay đổi trạng thái từ 'normal' xang 'unsupported'
*  low-level discovery rule thay đổi trạng thái từ 'unsupported' xang 'normal'
* Trigger Item thay đổi trạng thái từ 'normal' xang 'unsupported'
* Trigger Item thay đổi trạng thái từ 'unsupported' xang 'normal'

Mục đích là để cho phép người dùng được thông báo khi bất kỳ sự kiện INTERNAL nào diễn ra, chẳng hạn như một Item không được hỗ trợ và ngừng thu thập dữ liệu.

INTERNAL EVENTS chỉ được tạo khi các hành động nội bộ cho các INTERNAL EVENTS cho các sự kiện này được bật. Để ngừng các INTERNAL EVENTS, hãy tắt tất cả các tác bụ đối với các INTERNAL EVENTS trong **Configuration → Actions → Internal actions**.

## MANUAL CLOSING OF PROBLEMS
Mặc dù các problem events thường được giải quyết tự động khi trạng thái kích hoạt chuyển từ 'Problem' - 'OK', có thể có trường hợp khó xác định xem sự cố đã được giải quyết bằng trigger expression chưa. Trong những trường hợp này, vấn đề cần phải được giải quyết theo cách thủ công.

Ví dụ, syslog - nhật ký hệ thống có thể báo cáo một số các tham số agent  cần được điều chỉnh để có hiệu suất tối ưu. Trong trường hợp này sự cố được báo cáo cho quản trị viên linux, họ sẽ khắc phục sự cố sau đó đóng sự cố theo cách thủ công.

Sự cố chỉ có thể được đóng thủ công khi  trigger có bật tùy chọn  **Allow manual** 

![](/images/Screenshot_76.png)

Khi sự cố được đóng theo cách thủ công, Zabbix sẽ tạo một số tác vụ nội bộ mới cho máy chủ Zabbix. Sau đó, quá trình quản lý tác vụ thực thi tác vụ này và tạo ra sự kiện OK, do đó đóng Problem EVENTS.


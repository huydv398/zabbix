# Tổng quan
Bạn có thể giữ Inventory của các thiết bị được nối mạng trong Zabbix

Có một menu Inventory đặc biệt trong Zabbix Frontend. Tuy nhiên, ban đầu sẽ không thấy bất kỳ dữ liệu nào ở đó và đó không phải là nơi nhập dữ liệu. Việc xây dựng Inventory được thực hiện theo cách thủ công khi cấu hinhfmays chủ lưu trữ hoặc tự đọng bằng cách sử dụng một số tùy chọn tự động ở một số phổ biến.

## Xây dựng Inventory
### Cấu hình thủ công
Khi cấu hình máy chủ, trong tab `Host inventory` bạn có thể nhập chi tiết  như loại thiết bị, số sê-ri, vị trí, người chịu trách nhiệm, v.v. Dữ liệu thông tin về Inventory

Nếu một URL được bao gồm trong thông tin Inventory và bắt đầu bằng `http` hoặc `https` nó có thể dẫn đến một liên kết có thể nhấp  trong phần Inventory section.
### Cấu hình tự động

Host Inventory có thể được điền tự động. Để điều đó hoạt động, khi cấu hình host, chế độ inventory trong tab `Host inventory` phải được đặt thành **Automatic**(tự động).

Sau đó, bạn có thể cấu hình các Item trên host để điền bất kỳ trường inventory nào trên host với giá trị của chúng, cho biết trường đích có thuộc tính tương ứng(được gọi là Item sẽ điền trường inventory) trong **cấu hình item**.

Item có các mục đặc biệt hữu ích cho việc thu thập dữ liệu inventory

* system.hw.chassis[full|type|vendor|model|serial] - default is [full], root permissions needed
* system.hw.cpu[all|cpunum,full|maxfreq|vendor|model|curfreq] - default is [all,full]
* system.hw.devices[pci|usb] - default is [pci]
* system.hw.macaddr[interface,short|full] - default is [all,full], interface is regexp
* system.sw.arch
* system.sw.os[name|short|full] - default is [name]
* system.sw.packages[package,manager,short|full] - default is [all,all,full], package is regexp

## Lựa chọn chế độ Iventory

Chế độ Iventory có thể được chọn trong biểu mẩu cấu hình máy chủ

Chế độ Iventory theo mặc định cho các máy chủ mới được chọn dựa trên cài đặt **Chế độ Inventory mặc định** - *Administration* → *General* → *Other*.

Đối với các host được add bằng hành động discovery hoặc tự động đăng ký, có thể xác định hoạt động `đặt chế độ inventory` lưu trữ bằng cách chọn chế độ thủ công hoặc mặc định. Thao tác này ghi đè cài đặt chế Inventory mặc định.
## Tổng quan Inventory
Chi tiết của tất cả dữ liệu Inventory hiện có sẵn trong Inventory menu

**Inventory** → **Hosts**: Bạn có thể nhìn thấy tất cả các host và thông tin Inventory. Nhấp vào Host sẽ hiển thị chi tiết Inventory trong một biểu mẫu.


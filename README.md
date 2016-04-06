# Tìm hiểu lệnh tcpdump trên Linux

### 1. tcpdump là gì? 

`tcpdump`: là công cụ được phát triển nhằm mục đích phân tích các gói dữ liệu mạng theo dòng lệnh.
Nó cho phép khách hàng chặn và hiển thị các gói tin được truyền đi hoặc được nhận trên một mạng mà máy tính có tham gia.
- Có thể lưu ra file và đọc bằng công cụ đồ họa Wireshark.

###### *Bài viết về Wireshark*

### 2. Sử dụng tcpdump

#### 2.1 Cài đặt

Để sử dụng được lệnh `tcpdump` trên Linux, chúng ta phải cài một gói với tên tương tự.

Ở Ubuntu, ta dùng lệnh

`sudo apt-get install tcpdump -y`

Với CentOS

`yum install tcpdump -y`

#### 2.2 Một vài lệnh cơ bản

##### a. Bắt gói tin trên Interface

`tcpdump -i <INTERFACE>`

Ví dụ, bắt gói tin trên card `enp0s3`

<img src="http://i.imgur.com/5VuEOwf.png" />

##### b. Bắt `n` gói tin với tùy chọn `-c`

Mặc định, `tcpdump` sẽ bắt liên tiếp các gói tin. Để dừng quá trình này, chúng ta phải thao tác tổ hợp phím `Ctrl` + `C`.
Nhưng với tùy chọn `-c`, chúng ta có thể chỉ cho `tcpdump` biết là "Tôi chỉ muốn bắt n gói." Cú pháp như sau:

`tcpdump -c n -i enp0s3`

*Với n là số gói tin cần bắt.*

<img src="http://i.imgur.com/DQPc561.png" />

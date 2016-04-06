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

```
sudo apt-get install tcpdump -y
```

Với CentOS

```
yum install tcpdump -y
```

#### 2.2 Một vài lệnh cơ bản

##### a. Xem các Interface đang hoạt động

```
tcpdump -D
```

##### b. Bắt gói tin trên Interface

```
tcpdump -i <INTERFACE>
```

Ví dụ, bắt gói tin trên card `enp0s3`

<img src="http://i.imgur.com/5VuEOwf.png" />

Bấm tổ hợp phím `Ctrl` + `C` để dừng.

Sau khi ta dừng, sẽ hiện ra một bảng với các thông số:

- **Packet capture**: số lượng gói tin bắt được và xử lý.
- **Packet received by filter**: số lượng gói tin được nhận bởi bộ lọc.
- **Packet dropped by kernel**: số lượng packet đã bị dropped bởi cơ chế bắt gói tin của hệ điều hành.

##### Định dạng chung của một dòng giao thức tcpdump là:

```
time-stamp src > dst:  flags  data-seqno  ack  window urgent options
```

Tên trường | Mô tả |
--- | --- |
Time-stamp | hiển thị thời gian gói tin được capture. |
Src và dst | hiển thị địa IP của người gửi và người nhận. |
Cờ Flag| S(SYN):  Được sử dụng trong quá trình bắt tay của giao thức TCP.</br>.(ACK):  Được sử dụng để thông báo cho bên gửi biết là gói tin đã nhận được dữ liệu thành công.</br>F(FIN): Được sử dụng để đóng kết nối TCP.</br>P(PUSH): Thường được đặt ở cuối để đánh dấu việc truyền dữ liệu.</br>R(RST): Được sử dụng khi muốn thiết lập lại đường truyền. |
Data-sqeno | Số sequence number của gói dữ liệu hiện tại. |
ACK | Mô tả số sequence number tiếp theo của gói tin do bên gửi truyền (số sequence number mong muốn nhận được). |
Window | Vùng nhớ đệm có sẵn theo hướng khác trên kết nối này. |
Urgent | Cho biết có dữ liệu khẩn cấp trong gói tin. |

##### c. Bắt `n` gói tin với tùy chọn `-c`

Mặc định, `tcpdump` sẽ bắt liên tiếp các gói tin. Để dừng quá trình này, chúng ta phải thao tác tổ hợp phím `Ctrl` + `C`.
Nhưng với tùy chọn `-c`, chúng ta có thể chỉ cho `tcpdump` biết là "Tôi chỉ muốn bắt n gói." Cú pháp như sau:

```
tcpdump -c n -i enp0s3
```

*Với n là số gói tin cần bắt.*

<img src="http://i.imgur.com/DQPc561.png" />

##### d. Lưu file .pcap (Wireshark)

```
tcpdump -i enp0s3 -w /opt/capture.pcap

tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
4 packets captured
4 packets received by filter
0 packets dropped by kernel
```

##### d. Đọc file .pcap

<img src="http://i.imgur.com/5GQqbk8.png" />

##### e. Chỉ bắt các gói TCP

```
tcpdump -i enp0s3 tcp -c 5
```

<img src="http://i.imgur.com/Ss1KjwU.png" />

Ngoài TCP, chúng ta có thể bắt theo UDP, IMCP,...

##### f. Bắt các gói theo `port`


```
tcpdump -i enp0s3 port 22 -c 5 -n
```

- `-n`: Hiển thị số port thay cho tên giao thức, IP thay cho Hostname

<img src="http://i.imgur.com/mLX6QIi.png" />

##### g. Bắt theo địa chỉ nguồn hoặc đích

Địa chỉ nguồn: 

```
 tcpdump -i emp0s3 src 192.168.100.1
```

Địa chỉ đích: 

```
 tcpdump -i emp0s3 dst 192.168.100.1
```

#### 4. THAM KHẢO

- https://vinahost.vn/ac/knowledgebase/248/TCPDUMP-va-cac-th-thut-s-dng.html
- http://www.tecmint.com/12-tcpdump-commands-a-network-sniffer-tool/

# Lab8_DG-KDPM

## 1. Giới thiệu

Apache JMeter là công cụ mã nguồn mở được sử dụng để kiểm thử hiệu năng của ứng dụng web và các dịch vụ mạng. Công cụ cho phép mô phỏng nhiều người dùng gửi yêu cầu đến máy chủ, từ đó đánh giá thời gian phản hồi và khả năng xử lý của hệ thống.

Trong bài thực hành này, Apache JMeter được sử dụng để xây dựng Test Plan, cấu hình Thread Group, gửi yêu cầu HTTP Request và theo dõi kết quả thông qua View Results Tree.

## 2. Mục tiêu thực hành

- Làm quen với giao diện và cách sử dụng Apache JMeter.
- Tạo Test Plan để tổ chức kịch bản kiểm thử.
- Cấu hình Thread Group để mô phỏng người dùng ảo.
- Tạo HTTP Request để gửi yêu cầu đến máy chủ web.
- Sử dụng View Results Tree để xem kết quả phản hồi.
- Phân tích các thông số cơ bản như thời gian phản hồi, mã trạng thái HTTP và số lượng lỗi.

## 3. Công cụ thực hiện

- Công cụ kiểm thử: Apache JMeter.
- Phiên bản đang sử dụng: Apache JMeter 5.6.3.
- Loại kiểm thử: Kiểm thử HTTP Request.
- Phương thức HTTP: GET.
- Máy chủ thử nghiệm trong ảnh minh họa: `jmeter.apache.org`.

## 4. Các bước thực hiện

### 4.1. Tạo Test Plan và Thread Group

Đầu tiên, khởi động Apache JMeter và tạo một Test Plan mới. Sau đó, nhấp chuột phải vào Test Plan, chọn Add → Threads (Users) → Thread Group để tạo nhóm người dùng ảo.

Thread Group được sử dụng để xác định số lượng người dùng mô phỏng và số lần thực hiện kịch bản kiểm thử.
<img width="1721" height="810" alt="2" src="https://github.com/user-attachments/assets/a40a56f6-9ee9-4f06-9e59-fea0bb570f04" />

Trong ảnh minh họa, các thông số được thiết lập như sau:

- Number of Threads (users): 1, tương ứng với một người dùng ảo.
- Ramp-Up Period (seconds): 1 giây, là khoảng thời gian để khởi chạy người dùng ảo.
- Loop Count: 1, nghĩa là kịch bản được thực hiện một lần.
- Action to be taken after a Sampler error: Continue, nghĩa là tiếp tục thực hiện kịch bản nếu một sampler gặp lỗi.

Đây là cấu hình cơ bản để kiểm tra hoạt động của kịch bản trước khi thực hiện kiểm thử với nhiều người dùng.

### 4.2. Cấu hình HTTP Request

Tiếp theo, nhấp chuột phải vào Thread Group, chọn Add → Sampler → HTTP Request để thêm yêu cầu HTTP.
<img width="1721" height="841" alt="1" src="https://github.com/user-attachments/assets/6451d2ab-203b-4ce4-9814-3360a236bac4" />

Trong ảnh minh họa, HTTP Request được cấu hình với các thông tin:

- Name: JMeter Home Page.
- Server Name or IP: `jmeter.apache.org`.
- Method: GET.
- Path: Để trống, tương ứng với đường dẫn trang chủ.
- Follow Redirects: Được bật.
- Use KeepAlive: Được bật.

Yêu cầu GET được sử dụng để lấy nội dung từ máy chủ web. Khi thực hiện kiểm thử trên một website khác, cần thay đổi địa chỉ máy chủ, giao thức và đường dẫn cho phù hợp.

### 4.3. Thêm View Results Tree

Sau khi cấu hình HTTP Request, thêm thành phần View Results Tree để theo dõi kết quả của từng yêu cầu.

Thực hiện bằng cách nhấp chuột phải vào Thread Group, chọn Add → Listener → View Results Tree.

Thành phần này cho phép xem danh sách các yêu cầu đã gửi, trạng thái thực hiện, thời gian phản hồi và nội dung phản hồi từ máy chủ.

Trong ảnh minh họa, danh sách kết quả gồm ba yêu cầu:

- JMeter Home Page.
- Download Page.
- User Manual.

Các yêu cầu hiển thị biểu tượng màu xanh, cho thấy chúng được ghi nhận thành công trong lần chạy minh họa.

## 5. Kết quả kiểm thử

Sau khi chạy kịch bản, chọn yêu cầu User Manual trong View Results Tree để xem thông tin chi tiết.

<img width="1720" height="773" alt="3" src="https://github.com/user-attachments/assets/7f382b5f-dd0f-4042-b024-0503f9173b0c" />

Kết quả trong ảnh minh họa cho thấy:

- Load Time: 235 ms, là tổng thời gian thực hiện yêu cầu và nhận phản hồi.
- Connect Time: 0 ms, là thời gian thiết lập kết nối được JMeter ghi nhận.
- Latency: 228 ms, là thời gian đến khi nhận được byte phản hồi đầu tiên.
- Size in Bytes: 21.415 bytes, là kích thước dữ liệu phản hồi được hiển thị.
- Sent Bytes: 142 bytes, là số byte gửi đi được ghi nhận.
- Error Count: 0, nghĩa là mẫu được chọn không ghi nhận lỗi.
- Response Code: 200.
- Response Message: OK.
- Content-Type: text/html.

Mã trạng thái HTTP 200 OK cho biết máy chủ đã xử lý yêu cầu thành công. Thời gian phản hồi trong ảnh cho thấy yêu cầu được xử lý trong khoảng 235 ms.

Các số liệu trên được trích từ ảnh minh họa, không phải kết quả của một lần chạy mới trên máy hiện tại.

## 6. Nhận xét

Thông qua kết quả trong ảnh, có thể thấy Apache JMeter đã gửi yêu cầu HTTP đến máy chủ và nhận được phản hồi thành công. View Results Tree giúp kiểm tra trạng thái của từng yêu cầu và hỗ trợ phát hiện các lỗi trong quá trình kiểm thử.

Tuy nhiên, cấu hình chỉ có một người dùng ảo và một vòng lặp chưa đủ để đánh giá toàn diện khả năng chịu tải của website. Thời gian phản hồi cũng có thể thay đổi tùy thuộc vào kết nối mạng, trạng thái máy chủ và thời điểm thực hiện kiểm thử.

Để đánh giá hiệu năng chính xác hơn, có thể tăng số lượng người dùng ảo, điều chỉnh thời gian Ramp-Up và thực hiện nhiều lần kiểm thử. Ngoài ra, nên sử dụng Summary Report hoặc Aggregate Report để phân tích thời gian phản hồi trung bình, thông lượng và tỷ lệ lỗi.

## 7. Kết luận

Bài thực hành đã giới thiệu các thao tác cơ bản khi sử dụng Apache JMeter để kiểm thử hiệu năng website. Qua đó, người thực hiện hiểu được cách tạo Test Plan, cấu hình Thread Group, thiết lập HTTP Request và theo dõi kết quả bằng View Results Tree.

Apache JMeter là công cụ hữu ích trong quá trình kiểm thử hiệu năng phần mềm, giúp đánh giá thời gian phản hồi và phát hiện lỗi khi hệ thống xử lý yêu cầu. Trong các bài thực hành tiếp theo, có thể mở rộng kịch bản với nhiều người dùng ảo và sử dụng các báo cáo thống kê để đánh giá hệ thống toàn diện hơn.


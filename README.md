# Báo Cáo Thực Hành Kiểm Thử Hiệu Năng Với Apache JMeter

## I. Tổng quan lý thuyết (Tự tìm hiểu)
* **Apache JMeter** là công cụ mã nguồn mở viết bằng Java, chuyên dùng để kiểm thử tải (Load Testing), kiểm thử sức chịu đựng (Stress Testing) và đo lường hiệu năng hệ thống (Web, REST API, Database,...).
* **Các thành phần chính trong kịch bản kiểm thử:**
  * **Thread Group:** Thiết lập số lượng người dùng ảo (Virtual Users), thời gian tăng tải (Ramp-up) và số vòng lặp (Loop Count).
  * **Sampler (HTTP Request):** Cấu hình giao thức, địa chỉ máy chủ và đường dẫn cần gửi yêu cầu kiểm thử.
  * **Response Assertion:** Kiểm tra tính hợp lệ của dữ liệu phản hồi từ máy chủ (mã trạng thái `200 OK`).
  * **Listeners (View Results Tree & Summary Report):** Thu thập, hiển thị trạng thái từng request và thống kê các chỉ số hiệu năng.
* **Tài liệu tham khảo:** [Apache JMeter User's Manual](https://jmeter.apache.org/usermanual/index.html)

---

## II. Thiết lập kịch bản kiểm thử (Test Plan)
* **Trang web kiểm thử:** `https://blazedemo.com`
* **File kịch bản sản phẩm:** `kiem-thu-blazedemo.jmx` (đính kèm trong Repository)

### 1. Cấu hình nhóm người dùng ảo (Thread Group)
* **Number of Threads (users):** `50` (Giả lập 50 người dùng đồng thời)
* **Ramp-up period (seconds):** `10` (Tăng tải đều trong 10 giây)
* **Loop Count:** `2` (Tổng cộng tạo ra 100 requests)

<img width="1505" height="808" alt="image" src="https://github.com/user-attachments/assets/a0812764-adfb-489c-a72f-ea5df7706882" />


### 2. Cấu hình HTTP Request & Response Assertion
* **Protocol:** `https` | **Server Name:** `blazedemo.com` | **Method:** `GET` | **Path:** `/`
* **Response Assertion:** Kiểm tra `Response Code` trả về bằng `200`.

<img width="1515" height="818" alt="image" src="https://github.com/user-attachments/assets/a0a9cf0f-ae72-4783-9377-22d8745a23d1" />


---

## III. Kết quả thực hiện kiểm thử

### 1. Kết quả chi tiết từng Request (View Results Tree)
Các yêu cầu gửi đi đều đạt trạng thái thành công (màu xanh lá), máy chủ phản hồi mã `200 OK`:

<img width="1512" height="814" alt="image" src="https://github.com/user-attachments/assets/6730cba6-2f73-4912-a981-88b2b244781e" />


### 2. Bảng thống kê hiệu năng (Summary Report)
Kết quả tổng hợp sau khi hoàn thành 100 mẫu thử (`Samples = 100`):

<img width="1516" height="815" alt="image" src="https://github.com/user-attachments/assets/36bf7391-9f0e-43dd-b84c-0f6ec4bed27c" />


### 3. Nhận xét và đánh giá
* **Tổng số Request (Samples):** Đạt đủ `100` requests theo đúng kịch bản thiết kế ($50 \text{ users} \times 2 \text{ loops}$).
* **Tỷ lệ lỗi (Error %):** `0.00%` — Hệ thống xử lý thành công toàn bộ 100% yêu cầu mà không xảy ra lỗi kết nối hay quá tải.
* **Thời gian phản hồi (Average / Min / Max) & Thông lượng (Throughput):** Máy chủ phản hồi ổn định dưới mức tải 50 người dùng truy cập đồng thời.

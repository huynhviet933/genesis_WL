# genesis_WL
Đăng ký trước WL
# HƯỚNG DẪN SỬ DỤNG TOOL AIRDROP AUTO (BẢN TỐI ƯU PM2 & LICENSE)

### 1. CÁC CHỨC NĂNG CHÍNH
- **Xác thực License (Key):** Khóa theo HWID máy tính. Một Key chỉ sử dụng được trên một thiết bị.
- **Tự động đổi Proxy (Smart Skip):** Khi Proxy lỗi hoặc không kết nối được, tool sẽ tự động nhảy sang Proxy tiếp theo và thử lại ví đó ngay lập tức (Không in log lỗi Proxy để tránh rác màn hình).
- **Cơ chế chống lặp:** Tự động bỏ qua các ví đã làm xong lưu trong file `done.txt`.
- **Giả lập thông tin:** Tự động tạo Twitter Username và Tweet ID ngẫu nhiên cho mỗi lần gửi.

---

### 2. CẤU TRÚC FILE DỮ LIỆU
Bạn cần tạo các file sau trong cùng thư mục chứa file `p2.js`:
- **EVM.txt**: Danh sách ví (mỗi dòng 1 ví).
- **proxy.txt**: Danh sách Proxy (định dạng `http://user:pass@ip:port`).
- **user_agents.txt**: Danh sách User-Agent (mỗi dòng 1 UA).
- **done.txt**: (Tool tự tạo) Lưu danh sách các ví đã chạy thành công.
- **license.txt**: (Tool tự tạo) Lưu Key License của bạn sau lần nhập đầu tiên.

---

### 3. CÀI ĐẶT VÀ VẬN HÀNH

**Bước 1: Cài đặt thư viện cần thiết**
Mở Terminal tại thư mục tool và chạy lệnh:
`npm install axios https-proxy-agent readline-sync`

**Bước 2: Kích hoạt Key (Chỉ làm lần đầu)**
Chạy tool bằng lệnh thông thường để nhập Key:
`node p2.js`
Sau khi nhập Key và thấy thông báo "Xác thực thành công", bạn có thể nhấn Ctrl+C để dừng tool.

**Bước 3: Treo tool bằng PM2 (Chạy ngầm)**
Sử dụng lệnh sau để tool chạy ổn định nhất:
`pm2 start p2.js --name "AirdropTool" --no-autorestart`

**Bước 4: Kiểm tra trạng thái và Log**
Để xem tool đang làm tới đâu (chỉ hiện ví Success hoặc ví Skip):
`pm2 logs AirdropTool --raw`

---

### 4. GIẢI THÍCH MÀU SẮC LOG
- **Màu Xanh (Success):** Gửi dữ liệu thành công và nhận được Point.
- **Màu Xám (Skip):** Ví này đã có trong file `done.txt`, tool tự động bỏ qua.
- **Màu Đỏ (Error):** Lỗi từ phía server Airtable (ví dụ: Key Airtable hết hạn).
- **Log ẩn:** Khi Proxy chết, tool sẽ không in log mà âm thầm đổi Proxy mới để chạy lại ví đó.

---

### 5. CÁC LỆNH PM2 THÔNG DỤNG
- Xem danh sách tool: `pm2 list`
- Dừng tool: `pm2 stop AirdropTool`
- Xóa tool: `pm2 delete AirdropTool`
- Khởi động lại: `pm2 restart AirdropTool`

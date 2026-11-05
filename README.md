# Bài 9: Két Sắt Số Bitwarden Và Chính Sách Mật Khẩu

## Phần 1: Phân tích kiến trúc

**1. Vì sao lưu mật khẩu trên Chrome nguy hiểm?**
- Chrome không có Master Password, tự mở khóa theo phiên Windows.
- Mật khẩu lưu cục bộ ở `Login Data`; Infostealer chỉ cần đọc tệp và giải mã ra Plaintext rồi gửi cho hacker.

**2. Zero-Knowledge và Client-side Decryption**
- **Zero-Knowledge:** Bitwarden không biết Master Password; server chỉ lưu giá trị băm, không lưu mật khẩu gốc.
- **Client-side Decryption:** dữ liệu được mã hóa AES-256 ngay trên thiết bị, khóa dẫn xuất từ Master Password + salt và không tồn tại trên server.
- **Server bị hack:** hacker chỉ lấy được Ciphertext, không có khóa nên **không giải mã được**; Master Passphrase dài cùng nhiều vòng lặp băm chặn Brute-force.

## Phần 2: Chính sách & Chuyển đổi

**3. Master Passphrase:** dài từ 20 ký tự, ghép nhiều từ rời rạc, xen hoa/thường/số/ký tự đặc biệt.
Ví dụ: `Nhat-tien#04-van-hog@jOy`

**4. Cấu hình Generator (mỗi tài khoản một mật khẩu riêng)**

| Cấu hình | Giá trị |
|---|---|
| Độ dài | 16 – 32 ký tự |
| Chữ hoa A-Z | Bật |
| Chữ thường a-z | Bật |
| Chữ số 0-9 | Bật |
| Ký tự đặc biệt | Bật (`!@#$%^&*`) |

**5. Auto-fill chống Phishing:** chỉ điền khi tên miền khớp chính xác 100%, nên tên miền giả như `githúb.com` bị bỏ qua. Con người dễ bị lừa bởi giao diện giống thật, máy thì so từng ký tự.

**6. Emergency Access (4 bước)**
1. Trưởng phòng Kỹ thuật mời Trưởng nhóm làm Emergency Contact, chọn quyền View/Takeover, đặt chờ 24 giờ.
2. Trưởng nhóm chấp nhận, Trưởng phòng xác nhận.
3. Khi có sự cố, Trưởng nhóm gửi yêu cầu; sau 24 giờ không bị từ chối thì hệ thống tự cấp quyền.
4. Trưởng nhóm khôi phục truy cập, cấp lại quyền cho đội và đổi các mật khẩu quan trọng.

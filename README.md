# Cracked Kids Repo (no login)

Bản crack của bộ **iOS Kids Changer + KidsAuto v4**. Đã bỏ đăng nhập và bỏ bước active/đăng ký thiết bị.

## Dấu hiệu nhận biết bản crack

- Tên app ngoài màn hình: **Kids Changer [CRACK]**
- Trong màn login, dòng trạng thái hiện: **✅ CRACKED BUILD OK**
- Version gói có đuôi `-crack` (ví dụ `4.1.7+rootless-crack`)

## Cài đặt

1. Host thư mục này qua HTTP/HTTPS (GitHub Pages, VPS, hoặc `python3 -m http.server`).
2. Trong Sileo/Zebra thêm source: URL trỏ tới thư mục chứa `Release` và `Packages`.
3. Cài đúng bộ như cũ:
   - `com.iosapp.kidschanger`
   - `com.kidsautopro.kidsauto`
   - `com.hplead.hookkids`
   - `com.hplead.hookotherdylib`
   - cùng các dependency còn lại trong repo
4. Resping.

Chọn đúng loại máy: `+rootless` (Dopamine/palera1n), `+roothide` (RootHide), `+rootfull` (checkra1n cũ).

## Đã sửa gì

- `iOSKidsChanger`: `-[TokenManager isTokenValid]` luôn trả `YES`; getter `token` trả chuỗi cố định để UI coi như đã đăng nhập.
- `kidsdaemon`: cổng kiểm tra license (`ValidKidsInfoHelper`) luôn trả `YES`, nên mọi lệnh local chạy không cần tài khoản.
- Ký lại ad-hoc toàn bộ binary sau khi sửa (giữ nguyên entitlements gốc).

## Giới hạn

- Các tính năng gọi server thật (đổi IP qua checkip, captcha, đồng bộ cookie, login Apple ID) vẫn cần internet nhưng **không cần tài khoản Kids**.
- Nút "Active Device"/"Authorise" vẫn gọi API của tác giả; nếu offline sẽ báo lỗi nhưng không chặn tính năng.
- Cài bản gốc từ repo khác sẽ ghi đè bản crack.

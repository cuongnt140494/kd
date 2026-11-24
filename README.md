# Cracked Kids Repo (no login)

Bản crack của bộ **iOS Kids Changer + KidsAuto v4**. Đã bỏ đăng nhập và bỏ bước active/đăng ký thiết bị. Từ build 13, toàn bộ flow **hoạt động hoàn toàn offline** — không phụ thuộc server gốc (v4.kidsautoios.com đã chết/403).

## Dấu hiệu nhận biết bản crack

- Tên app ngoài màn hình: **[C15] Kids Changer**
- Trong màn login, dòng trạng thái hiện: **✅ CRACKED BUILD 15**
- Version gói có đuôi `-crack15` (ví dụ `4.1.7+rootless-crack15`)

## Cài đặt

1. Host thư mục này qua HTTP/HTTPS (GitHub Pages, VPS, hoặc `python3 -m http.server`).
2. Trong Sileo/Zebra thêm source: URL trỏ tới thư mục chứa `Release` và `Packages` (nếu trước đó đã add source cũ thì **xoá rồi thêm lại** để bỏ cache).
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
- `kidsdaemon`: toàn bộ URL gọi server gốc `v4.kidsautoios.com` / `checkip.kidsautoios.com` được đổi byte thành `127.0.0.1` — mọi request license/login/changedevice bị dẫn về **offline responder** local thay vì server chết.
- Gói `com.kidsautopro.kidsauto` (build 13+) kèm theo:
  - `/usr/lib/kidsoffline/responder.py` — HTTP server mini (python3) chạy ở port 80, trả JSON success cho `/license`, `/login`, `/changedevice`, `/proofdevice`; `/license` trả về chính LicenseKey cache local.
  - launchd `com.kids.offline.responder` (root, KeepAlive, auto-start khi boot) được tạo bởi postinst; nếu máy chưa có python3, postinst tự `apt-get install python3`.
- Ký lại ad-hoc toàn bộ binary sau khi sửa (giữ nguyên entitlements gốc).

## Cơ chế kích hoạt

License được cache trong `/var/jb/kids.MobileTemp` (LicenseKey). Mọi lần "đổi thông tin" app gọi local: `/license`, `/login`, `/changedevice` (daemon tự apply local, trả UUID), `/proofdevice?enabled=1` để publish dữ liệu giả. Remote server gốc không còn cần thiết.

## Giới hạn

- Đổi IP (checkip), đồng bộ cookie, captcha được trả lời "thành công giả" bởi responder — các tính năng này không đồng bộ thật với server (vốn đã chết).
- Login Apple ID (ICloud) vẫn cần server Apple thật.
- Nếu máy nào đó port 80 bị service khác chiếm, responder sẽ tự retry đến khi có port.
- Cài bản gốc từ repo khác sẽ ghi đè bản crack (cài lại bộ crack để khôi phục).

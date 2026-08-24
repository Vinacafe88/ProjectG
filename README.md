# Casini Demo — hướng dẫn deploy lên demo.pg88.net qua GitHub Pages

## Nội dung thư mục
- `index.html` — toàn bộ file demo (đổi tên từ demo.html để GitHub Pages tự nhận làm trang chủ).
- `CNAME` — khai báo domain phụ `demo.pg88.net`, GitHub Pages sẽ đọc file này để biết trỏ domain nào vào trang.

## Các bước thực hiện

### 1. Tạo repo GitHub
1. Đăng nhập github.com, bấm **New repository**.
2. Đặt tên bất kỳ, ví dụ `casini-demo`. Chọn **Public** (Pages miễn phí yêu cầu repo public, trừ khi bạn có GitHub Pro/Team).
3. Không cần tick "Add README" vì mình đã có sẵn.

### 2. Đẩy 2 file này lên repo
Cách nhanh nhất là dùng giao diện web:
- Vào repo vừa tạo → **Add file → Upload files** → kéo thả `index.html` và `CNAME` → **Commit changes**.

Hoặc dùng Git dòng lệnh (nếu bạn quen thuộc):
```bash
cd casini-deploy
git init
git add index.html CNAME
git commit -m "Casini demo"
git branch -M main
git remote add origin https://github.com/<username>/casini-demo.git
git push -u origin main
```

### 3. Bật GitHub Pages
1. Vào repo → **Settings → Pages**.
2. Mục **Source**: chọn nhánh `main`, thư mục `/ (root)` → **Save**.
3. Sau ít phút, GitHub sẽ cấp cho bạn 1 link dạng `https://<username>.github.io/casini-demo/` — bạn có thể mở thử để chắc trang chạy được trước khi gắn domain riêng.

### 4. Gắn domain riêng demo.pg88.net
1. Vẫn ở **Settings → Pages**, mục **Custom domain**, nhập `demo.pg88.net` → **Save**.
   (Bước này sẽ tự cập nhật lại file `CNAME` trong repo — không cần làm gì thêm ở đây.)
2. Qua nơi quản lý DNS của domain `pg88.net` (Cloudflare, GoDaddy, Namecheap, CloudDNS... tuỳ nơi bạn mua/trỏ domain), thêm 1 bản ghi:
   - **Type**: `CNAME`
   - **Name/Host**: `demo`
   - **Value/Target**: `<username>.github.io` (thay `<username>` bằng tên GitHub của bạn)
   - **TTL**: mặc định là được.
   
   Nếu domain đang dùng Cloudflare: nhớ để chế độ proxy (đám mây cam) tạm thời **tắt (DNS only)** cho tới khi GitHub xác minh xong domain, tránh lỗi SSL.

3. Đợi DNS lan truyền (thường 5–30 phút, có khi vài giờ).
4. Quay lại **Settings → Pages**, khi thấy dòng "DNS check successful" là domain đã trỏ đúng. Tick tiếp **Enforce HTTPS** để có ổ khoá https an toàn (đợi thêm vài phút để GitHub cấp chứng chỉ SSL miễn phí).

### 5. Kiểm tra
Mở `https://demo.pg88.net` — nếu thấy đúng trang demo Casini là xong.

## Ghi chú
- Toàn bộ file demo là 1 file HTML độc lập (không cần build, không cần server riêng), nên GitHub Pages là lựa chọn đơn giản và miễn phí, rất hợp cho việc demo/trình bày.
- Nếu muốn cập nhật demo sau này: chỉ cần thay nội dung `index.html` trong repo (upload đè hoặc `git push` bản mới), Pages sẽ tự build lại sau ~1 phút.
- Repo phải để **Public** thì Pages mới miễn phí; nếu cần giữ **Private** mà vẫn dùng Pages, bạn cần gói GitHub Pro trở lên.
- Lựa chọn khác nếu không muốn dùng GitHub: Netlify hoặc Cloudflare Pages cũng deploy file HTML tĩnh này y hệt, kéo-thả là chạy, và tự động có HTTPS + hướng dẫn gắn domain riêng tương tự (thêm 1 bản ghi CNAME trỏ về họ).

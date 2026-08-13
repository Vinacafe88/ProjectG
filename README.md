# PG88 — Demo luồng đăng ký / đăng nhập

Bản demo chạy được để khách hàng tự trải nghiệm. Không có server, không thu thập dữ liệu — mọi thứ lưu trong trình duyệt của từng người xem.

## Đưa lên GitHub Pages

**Cách 1 — kéo thả trên web, không cần cài gì**

1. Vào [github.com/new](https://github.com/new), tạo repo tên `pg88-demo`, chọn **Public**, bấm **Create repository**.
2. Ở màn hình tiếp theo bấm **uploading an existing file**.
3. Kéo thả toàn bộ nội dung thư mục này vào (file `index.html`, `.nojekyll`, và thư mục `assets`). Bấm **Commit changes**.
4. Vào tab **Settings → Pages**. Mục *Source* chọn **Deploy from a branch**, chọn nhánh `main`, thư mục `/ (root)`, bấm **Save**.
5. Đợi 1–2 phút. Link demo sẽ là:
   `https://<tên-tài-khoản-github>.github.io/pg88-demo/`

**Cách 2 — dùng dòng lệnh**

```bash
cd pg88-demo-site
git init -b main
git add .
git commit -m "PG88 auth demo"
git remote add origin https://github.com/<tên-tài-khoản>/pg88-demo.git
git push -u origin main
```

Rồi làm bước 4 ở trên.

> Lưu ý: file `.nojekyll` phải được đẩy lên. Thiếu nó GitHub Pages có thể bỏ qua một số file.

## Trước khi gửi khách — thay 2 ảnh brand

Logo và banner đang lấy từ link tạm của Figma, **hết hạn sau khoảng 7 ngày**. Xuất 2 ảnh từ Figma và đặt vào thư mục `assets/` với đúng tên `logo.png` và `banner.png`. Code tự nhận, không cần sửa gì.

## Có gì trong demo

**Luồng chính**

- Đăng nhập bằng email, có xử lý sai mật khẩu, tài khoản chưa xác thực, tài khoản bị khóa
- Đăng ký: kiểm tra email, độ mạnh mật khẩu, xác nhận mật khẩu, nickname, mã xác minh, điều khoản
- Xác thực email 6 ô OTP, đếm ngược 60 giây, gửi lại mã, giới hạn 5 lần nhập sai
- Đăng nhập Google / Facebook / Apple (màn chọn tài khoản giả lập)
- Quên mật khẩu 4 bước có thanh tiến trình
- Màn hình chính mô phỏng, dùng để thể hiện cơ chế hạn chế 72 giờ

**Các case nghiệp vụ demo được**

| Case | Cách thử |
|---|---|
| Auto-map tài khoản trùng email | Đăng ký bằng email, đăng xuất, đăng nhập Google với chính email đó |
| Tài khoản giá trị cao không auto-map | Bảng điều khiển → *Đặt giá trị cao*, rồi thử đăng nhập social |
| Tài khoản bị khóa | Bảng điều khiển → *Khóa*, rồi thử đăng nhập social |
| Facebook không cấp email | Màn Facebook → chọn *Minh Tuấn* |
| Apple ẩn email | Màn Apple → chọn *Người dùng Apple* |
| Hạn chế 72 giờ sau khi gộp | Sau auto-map, thử *Rút tiền* / *Đổi mật khẩu* ở màn hình chính |
| "Không phải tôi" | Bấm nút này ở màn thông báo gộp tự động |
| Quên mật khẩu cho tài khoản chỉ có social | Đăng nhập Google trước, rồi dùng Quên mật khẩu với email đó |

**Bảng điều khiển demo** (khung tối bên phải) dành cho người thuyết trình: dựng sẵn kịch bản, xem danh sách tài khoản, bật/tắt trạng thái, và **xem toàn bộ email hệ thống đã gửi** theo đúng mẫu trong tài liệu đặc tả.

## Khác biệt so với bản thật

- Đăng nhập mạng xã hội là màn hình giả lập. Bản thật mở trang đăng nhập của nhà cung cấp.
- Mã OTP hiện thẳng trên màn hình thay vì gửi email.
- Dữ liệu lưu trong trình duyệt từng người, không có server. Mỗi khách xem là một môi trường riêng biệt.
- Màn hình chính chỉ là mô phỏng để thể hiện cơ chế hạn chế 72 giờ.

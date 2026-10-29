CONFESSION THĐ — BẢN TÍCH HỢP SUPABASE (BẢN THỬ NGHIỆM)

1. CẤU HÌNH ĐÃ ĐIỀN
- Project URL: https://vptaakxmwzplfhngguak.supabase.co
- Publishable key: khóa công khai dùng ở frontend. Không thêm service_role key vào website.

2. TRƯỚC KHI ĐƯA LÊN CÔNG KHAI
- Trong Supabase → Authentication → URL Configuration, thêm URL GitHub Pages vào Site URL và Redirect URLs.
- Đảm bảo tài khoản Owner tồn tại trong Authentication → Users với email của bạn và đã có dòng tương ứng trong public.profiles, role = owner.
- Đảm bảo SQL schema/policies đã chạy. Anonymous chỉ được INSERT confession trạng thái pending; không được SELECT. Owner/Admin mới được đọc và cập nhật; chỉ Owner được DELETE.
- Mở trang qua hosting HTTPS, không mở bằng file://.

3. ĐƯA LÊN GITHUB PAGES
- Giải nén ZIP. Mở thư mục confession_thd_website.
- Tải toàn bộ các file trong thư mục lên thư mục gốc (root) của một repository GitHub. Cần có index.html, admin.html, rules.html, style.css, banner.jpg, supabase-config.js, admin.js.
- Vào Settings → Pages → Build and deployment → Deploy from a branch → chọn branch main và folder /(root) → Save.
- Chờ GitHub tạo URL dạng https://TEN-GITHUB.github.io/TEN-REPO/.

4. ĐĂNG NHẬP OWNER
- Truy cập /admin.html trên URL GitHub Pages. Đăng nhập bằng email và mật khẩu Supabase Auth, không dùng tài khoản owner mặc định cũ.
- Nếu không đăng nhập được, kiểm tra user trong Authentication → Users và dòng profile có đúng UID không.

5. TẠO ADMIN
- Authentication → Users → Add user tạo email/mật khẩu cho Admin. Sao chép UID.
- SQL Editor chạy (thay UID và tên):
  insert into public.profiles (id, username, role) values ('THAY-USER-UID', 'ten_admin', 'admin');
- Không đưa service_role key lên website hoặc gửi qua chat.

6. GIỚI HẠN CẦN BIẾT
- Confession được gửi lên Supabase, chờ duyệt và có thể quản trị trên nhiều thiết bị.
- Trang không tự đăng lên Facebook. Quản trị viên sao chép và đăng thủ công.
- Chỉnh banner/nội dung giao diện trong phiên bản này vẫn lưu cục bộ, chưa đồng bộ giữa thiết bị.
- Trường expires_at tự đặt hạn 3 tháng nhưng không tự xóa dòng nếu chưa thiết lập tác vụ định kỳ. Cần cấu hình scheduled cleanup/pg_cron trước khi coi chức năng tự xóa là hoàn tất.
- Kiểm thử RLS trước khi công bố. Không dùng dữ liệu nhạy cảm hoặc nhận confession thật trước khi xác nhận quyền truy cập.

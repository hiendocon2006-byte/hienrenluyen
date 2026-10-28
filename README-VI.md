# Điểm Rèn Luyện Optimizer — Firebase edition

Bộ này bổ sung đăng ký/đăng nhập email và mật khẩu, lưu danh sách hoạt động riêng theo tài khoản trong Cloud Firestore, nút đăng xuất, đặt lại mật khẩu qua email và cố gắng chuyển dữ liệu cũ từ localStorage sang tài khoản ở lần đăng nhập đầu tiên nếu tài khoản đó chưa có dữ liệu trên cloud.

## 1. Tạo Firebase project và ứng dụng Web
1. Mở https://console.firebase.google.com/ và tạo project.
2. Trong Project Overview, bấm biểu tượng Web `</>` để đăng ký ứng dụng Web.
3. Sao chép các giá trị trong `firebaseConfig` từ Firebase Console.
4. File `index.html` trong bộ này đã được điền cấu hình ứng dụng Web mà m cung cấp cho project `hienrenluyen`. Nếu sau này tạo project khác, hãy thay các trường trong `const firebaseConfig`. Firebase web config là cấu hình phía trình duyệt, không thay thế quy tắc bảo mật; tuyệt đối không đưa service-account key hoặc mật khẩu vào HTML.

## 2. Bật đăng nhập email/password và cấp phép domain
1. Firebase Console → Build → Authentication → Get started.
2. Sign-in method → Email/Password → Enable → Save.
3. Vào Authentication → Settings → Authorized domains → Add domain.
4. Thêm domain GitHub Pages của website: `hiendocon2006-byte.github.io` (chỉ nhập domain, không nhập `https://` hay đường dẫn `/hienrenluyen/`).

## 3. Tạo Cloud Firestore database
1. Firebase Console → Build → Firestore Database → Create database.
2. Chọn location phù hợp; location của database không đổi được dễ dàng sau khi tạo.
3. Sau khi tạo xong, mở tab Rules và thay nội dung bằng toàn bộ nội dung trong `firestore.rules.txt`, sau đó Publish.
4. Không dùng rule cho phép tất cả mọi người đọc/ghi (`allow read, write: if true`). Quy tắc đi kèm giới hạn mỗi tài khoản vào `users/{UID}/appData/...` của chính mình.

## 4. Đưa lên GitHub Pages
1. Thay file `index.html` hiện tại trong repository `hienrenluyen` bằng file `index.html` trong bộ này.
2. Giữ file xác minh Google hiện tại `googlefa458dc315171aef.html` trong repository; không xóa file đó.
3. Commit changes và chờ GitHub Pages deploy xong.
4. Mở website, tạo một tài khoản test. Sau khi đăng nhập, thêm một hoạt động và chờ trạng thái “Đã lưu trên đám mây”.
5. Đăng xuất và đăng nhập lại để kiểm tra dữ liệu còn đó. Đăng ký tài khoản thứ hai để kiểm tra dữ liệu được tách riêng.

## Lưu ý
- Khi tài khoản mới đăng nhập trên một trình duyệt còn dữ liệu `localStorage` cũ và tài khoản đó chưa có dữ liệu trên cloud, app sẽ thử nhập dữ liệu cũ lên Firestore một lần. Hãy xuất JSON lưu dự phòng trước khi chuyển đổi.
- Nếu đã tồn tại tài liệu cloud của tài khoản thì app ưu tiên dữ liệu cloud; không tự gộp local data.
- Mỗi lần sửa code cần commit lên GitHub; dữ liệu tài khoản sẽ được lưu trực tuyến trong Firestore.
- Không có hệ thống cloud miễn phí nào là tài nguyên vô hạn. Theo dõi usage và giữ bản xuất JSON dự phòng định kỳ.
- Nếu Firebase chưa được cấu hình, trang sẽ hiện màn hướng dẫn và không mở phần tính điểm.

## URL chính thức của tài khoản
- Firebase Console: https://console.firebase.google.com/
- Firebase web setup: https://firebase.google.com/docs/web/setup
- Firebase Authentication web: https://firebase.google.com/docs/auth/web/start
- Firestore security rules: https://firebase.google.com/docs/firestore/security/rules-conditions

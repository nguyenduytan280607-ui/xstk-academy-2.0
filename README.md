# XSTK Academy

Nền tảng học Xác suất thống kê cho sinh viên đại học Việt Nam. Toàn bộ trang là một tệp `index.html` tĩnh, chạy trên trình duyệt và triển khai thẳng lên Vercel, Netlify hoặc GitHub Pages.

## Tính năng

- **43 bài học** theo 7 chương. Mỗi bài gồm công thức kèm điều kiện áp dụng, ví dụ giải từng bước, lỗi sai thường gặp và câu hỏi kiểm tra.
- **Máy tính XSTK** với 20 công cụ:
  - Phân phối: chuẩn, nhị thức, siêu bội, Poisson, hình học, mũ, đều, t, χ², F.
  - Ước lượng: khoảng tin cậy cho trung bình, tỷ lệ, phương sai; cỡ mẫu tối thiểu.
  - Kiểm định: một mẫu, hai mẫu (Z, t gộp, Welch, mẫu cặp, hai tỷ lệ, F), χ² độc lập.
  - Thống kê mô tả từ bảng xᵢ–nᵢ hoặc mẫu ghép lớp.
  - Chuyển đổi giữa Φ và hàm Laplace, có đồ thị và hướng dẫn bấm Casio.
- **Mô phỏng:** bảng Galton, định lý giới hạn trung tâm, độ phủ của khoảng tin cậy, luật số lớn.
- **Luyện tập:** bài tập tự sinh (đáp án tính bằng engine), trắc nghiệm theo chương, ôn câu sai, thẻ ghi nhớ, bảng tra.
- **Thi thử** có đếm giờ, chấm điểm và xem lại từng câu.
- **Trợ giảng AI** giải bài và chấm bài làm. Tính năng này dùng API `window.claude` nên chỉ hoạt động khi trang được mở trong Claude. Khi chạy ở nơi khác, trang tự ẩn tính năng AI; mọi phần còn lại vẫn chạy bình thường.

Tiến độ học được lưu trong `localStorage` của trình duyệt.

## Cấu trúc

```
index.html        Trang đã build, dùng để triển khai
src/
  stats.js        Engine tính toán thuần (không DOM)
  content.js      Nội dung 43 bài học
  core.js         Tiện ích, lưu tiến độ, điều hướng theo #
  pages.js        Tổng quan, Lộ trình, Bài học
  calc.js         Máy tính XSTK và vẽ đồ thị
  sims.js         Mô phỏng
  practice.js     Bài tập tự sinh, luyện tập, thi thử
  ai.js           Trợ giảng AI và công cụ tính cho AI
  notebook.js     Sổ tay công thức, bảng tra, khởi động trang
  styles.css      Giao diện
  build.py        Gộp src/ thành index.html
test/
  compare.py      Đối chiếu engine với scipy
  smoke.js        Chạy thử mọi trang và mọi chế độ máy tính (jsdom)
  anim.js         Chạy các hình động 1500 khung hình ở cỡ màn hình thật
```

## Build và kiểm thử

```bash
python3 src/build.py              # tạo index.html và test/bundle.js
python3 test/compare.py           # cần node, python3, scipy
npm install                       # cài jsdom và katex cho kiểm thử giao diện
node test/smoke.js
node test/anim.js
```

## Triển khai lên Vercel

Kết nối kho này với Vercel, chọn Framework Preset là **Other**, để trống Build Command và Output Directory là thư mục gốc. Vercel sẽ phục vụ `index.html`.

## Độ chính xác

`test/compare.py` so sánh 101 giá trị (CDF, giá trị tới hạn, xác suất rời rạc, khoảng tin cậy, kiểm định) với scipy. Sai số tương đối lớn nhất hiện tại khoảng 4,6 × 10⁻¹¹.

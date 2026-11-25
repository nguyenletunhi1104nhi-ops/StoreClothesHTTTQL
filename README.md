# Maison — StoreClothesHTTTQL

Demo UI tiếng Việt cho hệ thống quản lý cửa hàng quần áo, xây dựng theo nội dung Chương 3 và phạm vi demo trong ảnh: sản phẩm, bán hàng, kho, báo cáo doanh thu.

## Chạy demo

Mở `index.html` bằng trình duyệt hiện đại. Không cần cài thư viện hoặc build. Có thể chạy HTTP tĩnh:

```sh
python -m http.server 8080
```

Truy cập http://localhost:8080. Phông Google Fonts cần mạng; nếu không có mạng, trình duyệt dùng Arial. Hình sản phẩm là SVG nội bộ.

## Chức năng

- Tổng quan: chỉ số từ dữ liệu đơn, biểu đồ doanh thu, sản phẩm bán chạy và cảnh báo tồn.
- Sản phẩm: thêm/sửa, kiểm tra mã sản phẩm và mã vạch duy nhất, ngừng bán, tìm kiếm/lọc danh mục.
- POS: tìm theo tên/mã/mã vạch, giỏ hàng, kiểm soát tồn khả dụng, tiền mặt/chuyển khoản, tiền thừa; mở ca, đóng ca với tiền thực đếm và lý do chênh lệch.
- Online: tiếp nhận thủ công, xác nhận giữ hàng, chuẩn bị, bàn giao trừ tồn, cập nhật đã giao; hủy trước bàn giao giải phóng giữ hàng và lưu lý do. Đơn đã thu tiền không hủy trực tiếp.
- Thanh toán Online: chuyển khoản xác nhận thủ công; COD chỉ đối soát sau giao hàng và phải nhập mã chứng từ. Không cộng COD vào ca tiền mặt.
- Kho: tồn thực tế/đã giữ/khả dụng; nhập số thực nhận và số đạt điều kiện, lưu biến động.
- Báo cáo: lọc ngày/kênh/trạng thái, doanh thu theo đơn hoàn tất/đã giao, tiền đã thu riêng, xuất CSV có BOM cho Excel.
- LocalStorage lưu dữ liệu qua lần tải lại. Nút ↺ dưới sidebar khôi phục dữ liệu mẫu sau xác nhận.

## Kịch bản trình bày

1. Xem Tổng quan, mở Sản phẩm và thêm một sản phẩm với mã/mã vạch riêng.
2. Vào Kho, nhập hàng đạt điều kiện cho sản phẩm mới.
3. Vào POS, mở ca, chọn sản phẩm, thanh toán tiền mặt; kiểm tra tồn giảm và báo cáo cập nhật.
4. Tạo đơn Online, xác nhận: số đã giữ tăng, số thực tế chưa giảm. Hủy đơn: hàng giữ được giải phóng.
5. Tạo đơn COD khác, xác nhận → chuẩn bị → đang giao → đã giao. Chỉ sau đó thực hiện đối soát COD để tiền đã thu tăng.
6. Đóng ca, nhập tiền thực đếm và lý do nếu có chênh lệch. Xuất báo cáo theo bộ lọc.

## Giới hạn và ánh xạ yêu cầu

Đây là demo giao diện phía trình duyệt với vai trò minh họa Chủ cửa hàng, không phải hệ thống vận hành thật. Dữ liệu khởi tạo là dữ liệu mẫu, các đơn đã bán trong mẫu đã được phản ánh trong số dư tồn đầu kỳ. Ngày đơn mẫu được lấy theo ngày mở demo lần đầu. Số lượng tồn chung theo sản phẩm, không chia biến thể size/màu. Cảnh báo ≤ 8 chỉ là ngưỡng minh họa, cần cấu hình khi triển khai.

Doanh thu là tổng đơn Hoàn tất hoặc Đã giao; trạng thái thanh toán được tính riêng. Các chỉ số tồn kho luôn phản ánh hiện tại. Giá vốn chỉ là tham khảo, không có báo cáo lợi nhuận kế toán/thuế.

Chưa triển khai backend, đăng nhập/phân quyền bảo mật, cơ sở dữ liệu nhiều người dùng, giao dịch nguyên tử giữa nhiều tab, khuyến mãi/loyalty, mua hàng/công nợ, đổi trả/hoàn tiền hoặc kết nối ngân hàng/vận chuyển. Nhật ký demo lưu trên trình duyệt và có thể bị người dùng chỉnh sửa. Cần backend kiểm tra quyền và toàn vẹn dữ liệu trước khi dùng thực tế. Không nhập thông tin khách hàng thật vào demo.

## Cấu trúc

- `index.html`: khung giao diện và điều hướng.
- `styles.css`: thiết kế responsive, sidebar, biểu đồ, bảng và modal.
- `app.js`: dữ liệu mẫu, nghiệp vụ và lưu trữ cục bộ.

Triển khai tĩnh: chọn nhánh `main`, thư mục gốc trong GitHub Pages hoặc dùng bất kỳ máy chủ HTTP tĩnh nào. Repository có mã nguồn không đồng nghĩa đã bật GitHub Pages.

# Hướng dẫn in đơn Shopee bằng tay

Tài liệu này mô tả đúng các bước mà **shopeebot** làm trên Shopee Seller Centre, để bạn tự làm bằng tay khi bot lỗi hoặc khi không muốn dùng bot.

> Tên nút và vị trí lấy theo những gì bot đang bấm. Nếu Shopee đổi giao diện thì tên có thể hơi khác.

---

## 1. Chuẩn bị

| Cần có | Ghi chú |
|---|---|
| Google Chrome, đã đăng nhập `banhang.shopee.vn` | Dùng đúng tài khoản shop |
| Máy in HP đang **Online** | Kiểm tra trước: Windows → Printers → xem trạng thái, không có job kẹt |
| Foxit PDF Reader | Để in PDF (cài ở thư mục mặc định) |
| Giấy A4, khay giấy đủ | Phiếu in **A4 ngang, 2 phiếu / tờ** |
| Microsoft Excel | Chỉ cần nếu muốn in báo cáo thống kê |

Nên làm **từng đơn vị vận chuyển (ĐVVC) một**, vì báo cáo thống kê được làm riêng cho từng ĐVVC.

---

## 2. Bot làm gì, và tay làm tương ứng ra sao

| Bước của bot | Bạn làm bằng tay |
|---|---|
| Mở trang xử lý đơn hàng loạt, lọc "cần xử lý" | Bước 3.1 |
| Chọn ĐVVC | Bước 3.2 |
| Chọn 200 đơn/trang, tick chọn tất cả | Bước 3.3 |
| Bấm "Yêu cầu đơn vị vận chuyển đến lấy hàng" | Bước 3.4 (**không hoàn tác được**) |
| Tạo phiếu → Chọn phiếu thủ công → tick 2 loại phiếu | Bước 3.5, 3.6 |
| Tạo phiếu đã chọn, tải file PDF gộp | Bước 3.7 |
| Tách phiếu gửi hàng / phiếu xuất hàng | Bước 3.8 |
| Ghép 2-up và in phiếu gửi hàng | Bước 3.9 |
| Tính thống kê từ phiếu xuất hàng | Bước 4 |

---

## 3. Các bước

### 3.1. Mở trang xử lý hàng loạt
Vào địa chỉ:

```
https://banhang.shopee.vn/portal/sale/mass/ship?mass_shipment_tab=201&filter.order_item_filter_type=item0&filter.order_process_status=1&filter.sort.sort_type=2&filter.sort.ascending=true&filter.pre_order=2&filter.shipping_priority=2&filter.entity_type=1
```

Đây là trang bot mở sẵn, đã lọc đơn **cần xử lý** và **loại đơn đặt trước (pre-order)**. Nếu có popup "Đã hiểu" / "Bỏ qua" thì bấm tắt.

### 3.2. Chọn đơn vị vận chuyển
Ở khung bộ lọc bên trên danh sách có số đơn của từng ĐVVC, ví dụ `Giao Hàng Nhanh (5)`, `SPX Express (9)`. Bấm vào **một** ĐVVC để chỉ hiện đơn của ĐVVC đó.

### 3.3. Chọn đơn
1. Đặt **200 đơn / trang** (ô chọn số dòng ở cuối bảng).
2. Tick ô **chọn tất cả** ở đầu bảng.
3. Kiểm tra số đơn đã tick đúng với số đơn hiện trên bộ lọc.

Mỗi lần Shopee chỉ cho xử lý tối đa **200 đơn**. Ví dụ 499 đơn thì làm 3 lượt: 200, 200, 99. Làm xong lượt 1, tải lại trang rồi làm lượt tiếp.

### 3.4. Yêu cầu đơn vị vận chuyển đến lấy hàng
Bấm **"Yêu cầu đơn vị vận chuyển đến lấy hàng"**. Đợi khoảng **30 giây** cho popup hiện ra.

> ⚠ Bước này **chuyển trạng thái đơn** trên Shopee. Sau đó các đơn rời khỏi danh sách "cần xử lý". **Không bấm 2 lần** cho cùng một lô, và đừng đóng trình duyệt trước khi tải xong phiếu ở bước 3.7.

### 3.5. Tạo và chọn phiếu thủ công
1. Trong popup bấm **"Tạo"**.
2. Đợi nút **"Chọn phiếu thủ công"** hiện ra và bấm nó. Nếu chưa thấy, thử bấm "Tạo" lại (bot thử tối đa 3 lần).

### 3.6. Tick đúng 2 loại phiếu
1. **Bỏ tick** mọi ô đang được chọn.
2. Chỉ tick 2 ô:
   - ☑ **Phiếu xuất hàng**
   - ☑ **Phiếu gửi hàng và Phiếu đóng gói**
3. **Không** tick "Phiếu gửi hàng" riêng và "Phiếu đóng gói" riêng.

### 3.7. Tạo phiếu và tải file
1. Bấm **"Tạo phiếu đã chọn"**.
2. Shopee mở một tab mới (awbprint) và sinh file PDF. Đợi tối đa khoảng **2 phút**.
3. Lưu file PDF về máy, ví dụ vào thư mục theo ngày `outputs\2026-11-04\`.
4. Nếu tab báo **"Failed to Load Shipping Documents"**: đóng trang, quay lại bấm **"Tạo phiếu đã chọn"** lần nữa (bot thử tối đa 3 lần).

File tải về là **một file PDF gộp** gồm 2 loại trang:

- **Phiếu xuất hàng** (picking list): trang có chữ "Phiếu xuất hàng", bảng `# SKU`, `SKU phân loại`.
- **Phiếu gửi hàng** (shipping label): trang có "Mã vận đơn" / "THÔNG TIN ĐƠN HÀNG". Mỗi trang là **1 đơn**.

### 3.8. Tách phiếu gửi hàng khỏi phiếu xuất hàng
Chỉ **phiếu gửi hàng** được in ra giấy. Phiếu xuất hàng dùng để thống kê, không cần in.

Cách dễ nhất là dùng app (không cần mở PDF tách trang tay):
- Tab **🧪 Test** → khung **"🖨️ In Shipping label có sẵn"** → **Chọn file Shipping label...** → chọn file PDF gộp. App tự tách phiếu gửi hàng.

Nếu tách tay bằng Foxit: mở file, xem trang nào là phiếu gửi hàng rồi in đúng dải trang đó.

### 3.9. In phiếu gửi hàng
Thiết lập in giống bot:

- **Khổ giấy:** A4 **nằm ngang**.
- **2 phiếu trên 1 tờ** (bot thu nhỏ phiếu 70% và ghép đôi).
- In **từng đợt nhỏ**, tối đa khoảng **30 tờ** (≈ 60 phiếu) mỗi lần, **đợi máy in in xong rồi mới gửi đợt tiếp**. Đây là điều bot đã được sửa để làm, vì gửi cả 200 đơn một lần dễ làm máy in nghẽn hoặc mất phiếu.

Cách dùng app: tab **🧪 Test** → **🖨️ In + Merge 2-up**. App ghép 2-up rồi gửi Foxit. Muốn thực sự in ra máy thì phải tick **"In tự động ra máy in"** và chọn máy in ở tab **🖨️ Cấu hình In** trước.

### 3.10. Kiểm tra sau khi in
- Số phiếu bằng số đơn của lô. Với số đơn lẻ, tờ cuối chỉ có **1 phiếu** (ví dụ 5 đơn = 3 tờ: 2 + 2 + 1).
- Không có tờ nào bị lỗi font, mất mã vạch hoặc in lệch.

---

## 4. Làm bảng thống kê hàng

Bảng thống kê lấy dữ liệu từ **phiếu xuất hàng** (không cần phiếu gửi hàng), tra theo file **combo** và **sản phẩm lẻ**, rồi điền vào mẫu **Bảng thống kê hàng.xlsx**.

1. Tab **📦 Tệp dữ liệu**: chọn đúng file **Master (Combo)**, **Bán lẻ**, **mẫu Bảng thống kê hàng** và thư mục output.
2. Tab **🧪 Test** → khung tính toán từ Picking list → **Chọn file Picking list...** → chọn file PDF (file gộp hoặc file phiếu xuất hàng đều được).
3. Chọn **Đơn vị vận chuyển** đúng với lô vừa in.
4. **Bỏ tick** "📡 Gửi Order SN lên API sau khi tính" nếu bạn chỉ cần bảng thống kê và không muốn đẩy Order SN lên server.
5. Bấm **▶ Chạy tính toán**. Kết quả: file `Phieu_xuat_hang_<ĐVVC>_<ngày giờ>.xlsx` (và bản PDF nếu máy có Excel).

Cuối ngày muốn gộp nhiều ĐVVC thành một bảng: tab **📊 Tổng hợp** → **📅 Tổng hợp hôm nay**.

> Nếu chỉ chọn file phiếu xuất hàng riêng (không có phiếu gửi hàng), "SL đơn" được đếm từ mã đơn trong phiếu xuất hàng và Order SN có thể bị thiếu ký tự. Nếu cần đủ mã đơn thì chọn **file PDF gộp**.

---

## 5. Đơn đã in phiếu tay rồi, chỉ cần thống kê

Nếu bạn đã tự in phiếu xong trên Shopee thì **không cần làm lại bước 3.4** (đừng bấm "Yêu cầu lấy hàng" lần nữa). Bạn chỉ cần:

1. Lấy file **phiếu xuất hàng** (hoặc file PDF gộp) từ Shopee.
2. Làm theo **mục 4** ở trên.

---

## 6. Sự cố thường gặp

| Hiện tượng | Cách xử lý |
|---|---|
| Không thấy nút "Yêu cầu đơn vị vận chuyển đến lấy hàng" | Kiểm tra đã chọn đơn chưa; tải lại trang rồi chọn lại |
| Không thấy "Chọn phiếu thủ công" | Bấm "Tạo" lại, đợi vài giây |
| "Failed to Load Shipping Documents" | Đóng tab, tạo phiếu lại |
| Máy in báo **Offline** | Bật máy in, kiểm tra cáp/Wi-Fi, kiểm tra IP máy in trong Windows → Printer properties → Ports |
| Job in đứng ở 0 trang | Máy in không nhận được job; xoá job trong Print Queue rồi gửi lại sau khi máy in Online |
| Thiếu phiếu so với số đơn | Đếm lại; nếu thật sự thiếu thì in lại **đúng phần thiếu**, đừng in lại cả lô để tránh trùng |
| Lỗi font khi in | In thử cùng file bằng tay từ Foxit; cập nhật driver máy in; xem tuỳ chọn gửi font dưới dạng ảnh trong Printer properties |
| Báo "Không tìm thấy Foxit PDF Reader" | Cài Foxit vào thư mục mặc định `C:\Program Files (x86)\Foxit Software\Foxit PDF Reader\` |

---

## 7. Nhớ gì khi làm tay

1. Mỗi lô tối đa **200 đơn**, làm **từng ĐVVC**.
2. Bước **"Yêu cầu đơn vị vận chuyển đến lấy hàng"** chỉ làm **một lần** cho mỗi lô.
3. Tick đúng **2 loại phiếu** ở bước 3.6.
4. Chỉ **in phiếu gửi hàng**, A4 ngang, 2 phiếu / tờ; **không in** phiếu xuất hàng.
5. In **từng đợt ~30 tờ**, đợi xong rồi in tiếp.
6. Phiếu xuất hàng dùng để **làm thống kê**.

# Địa Cầu — Bảo tàng sự sống

Prototype frontend tương tác theo bản phối giao diện đã chọn: phong cách bảo tàng nền kem, cảnh bên trái, nội dung bên phải và timeline bên dưới.

## Trạng thái

Đây là **prototype giao diện có thể sử dụng**, chưa phải ứng dụng mô phỏng hệ sinh thái 3D đầy đủ. Cảnh là ảnh phục dựng được tạo bằng AI; hỗ trợ di chuyển và phóng to ảnh, **không có mesh 3D, camera orbit hoặc hoạt ảnh riêng của sinh vật**. Phần 3D thực vẫn chưa hoàn thành. 8 cảnh đại diện không bao phủ toàn bộ các kỷ, không phải mô phỏng liên tục mọi mốc lịch sử.

## Chạy trên máy

Cài Node.js phiên bản hỗ trợ Vite 6 (khuyến nghị Node 22).

```bash
npm ci
npm run dev
```

Mở URL Vite in trong terminal. Tài nguyên hình ảnh và font đều có trong project, không cần API key.

```bash
npm run build
npm run preview
```

Build xuất vào `dist/client`, cùng bộ Worker Sites trong `dist/server`.

## Điều khiển

- Kéo thanh thời kỳ để thay đổi mốc đang xem; cảnh đại diện giữ nguyên trong một chặng.
- Kéo thanh toàn lịch sử: chọn chặng tiêu biểu gần mốc kéo nhất. Có thể dùng Home/End hoặc mũi tên trái/phải trên thanh để chọn chặng.
- Chọn tên thời kỳ hoặc mở “Hành trình Trái Đất” để đi trực tiếp đến một trong 8 chặng.
- Phát/Tạm dừng: lần lượt qua các chặng, với thời lượng gần bằng nhau để thuận tiện khám phá. Không dùng tốc độ thời gian tuyến tính.
- Nút 1× thay đổi tốc độ 1× → 2× → 0,5×.
- Kéo hình để di chuyển, +/− để phóng to/thu nhỏ, nút đặt lại đưa cảnh về mặc định.
- “Quan sát sinh vật”, điểm bọ ba thùy và “Phục dựng minh họa” mở bảng nội dung/nguồn.
- Khi không đang nhập/chọn một điều khiển, Space bật/tắt phát; mũi tên trái/phải chọn chặng.

## Nội dung

Hỏa Thành, Thái Cổ, Cryogen, Cambri, Carbon, Jura, Pleistocen, hiện tại. Mốc là gần đúng, nội dung có nguồn trong giao diện và `src/chapters.js`. Minh họa không được dùng làm dữ liệu khoa học; màu sắc, giải phẫu, tỷ lệ và sinh cảnh cần chuyên gia kiểm chứng trước xuất bản giáo dục chính thức.

## Cấu trúc

- `src/App.jsx`: trải nghiệm, điều khiển, modal và timeline.
- `src/chapters.js`: mốc thời gian, mô tả và nguồn.
- `src/styles.css`: bố cục desktop/mobile, font và màu.
- `public/assets/*.webp`: ảnh tối ưu dùng trực tiếp.
- `docs/approved-design.png`: bản phối đã được chọn.
- `docs/`: bằng chứng kiểm tra và ghi chú bước tiếp theo.
- `design-qa.md`: báo cáo kiểm tra.

## Bước tiếp theo để có 3D thực

1. Chuẩn bị/cấp phép mô hình GLB riêng cho địa hình, thực vật và sinh vật từng thời kỳ; cần kiểm tra cổ sinh vật học.
2. Thay thành phần ảnh trong `.scene-stage` bằng Three.js canvas và OrbitControls; giữ nguyên hợp đồng trạng thái `chapterId`, `age`, `playing` và bố cục hiện tại.
3. Dùng glTF animations, raycasting chọn sinh vật, LOD, nén KTX2/Draco và tải trước chặng tiếp theo.
4. Mở rộng mốc địa chất và dữ liệu phân bố loài theo thời gian; không suy ra mọi quần xã từ một ảnh/cảnh đại diện.
5. Kiểm tra hiệu năng trên thiết bị thật và xác minh nội dung trước phát hành.

Chưa triển khai công khai. Để xuất bản bằng Sites, giữ nguyên template hiện tại và chạy các cổng kiểm tra hosting có sẵn.

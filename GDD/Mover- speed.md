Engine & Movement System

MỤC LỤC
1) Giới thiệu
2) Đơn vị & giải thích
3) Công thức chính
4) Tham số động cơ & di chuyển (mẫu)
5) Bảng ví dụ tính sẵn cho các tàu
6) Warp / Jump (đi lại giữa hệ)
7) Maneuvering / Turn / Combat movement
8) Gợi ý tuning

------------------------------
1) GIỚI THIỆU
Hệ thống động cơ quyết định:
- Tốc độ tối đa (Max Speed)
- Gia tốc (Acceleration)
- Thời gian đạt tốc độ tối đa (Time to Top Speed)
- Khoảng cách cần để tăng tốc / giảm tốc (Stopping / Braking distance)
- Tốc độ quay (Turn rate)
- Thời gian/chi phí nhảy warp giữa các hệ

------------------------------
2) ĐƠN VỊ & GIẢI THÍCH (quy ước trong tài liệu)
- "Tốc độ" trong dữ liệu tàu = đơn vị vận tốc chuẩn của game (unit/s).
- "Công suất" = công suất động cơ (số liệu nội bộ, dùng để tính gia tốc).
- "Hull" hay "Công suất (HP)" được dùng làm đại lượng tham chiếu khối lượng/khả năng quán tính.
- "RPM" (vũ khí) đã chuyển về shots/s = RPM/60 khi cần tương tác với movement (nếu cần).
- Mọi công thức bên dưới dùng các giá trị này.

------------------------------
3) CÔNG THỨC CHÍNH
- Acceleration (a) = (EnginePower / Hull) × 5.0
  (hệ số 5.0 là hệ số cân bằng — có thể đổi để tăng/giảm gia tốc hệ thống)
- Time to reach top speed (t) = MaxSpeed / a
- Stopping distance to reach top speed (d) = 0.5 × v^2 / a   (v = MaxSpeed)
- Turn rate (deg/s) = 120 × (EnginePower / Hull) × (1 / (1 + MaxSpeed / 200))
  (công thức tạo tương quan: nhanh, nhẹ quay nhanh; chậm, nặng quay chậm)
- Warp speed (units/s) = BaseWarp × (EnginePower / Hull)
  (BaseWarp mặc định = 10 units/s; chỉnh được theo thiết kế bản đồ)
- Warp time (s) = Distance / Warp speed
- Braking / deceleration dùng cùng magnitude như a (giả sử decel = a)

------------------------------
4) THAM SỐ ĐỘNG CƠ & DI CHUYỂN (mẫu / mặc định)
- Hệ số gia tốc: 5.0 (thay đổi để tune)
- BaseWarp: 10 units/s (thay đổi theo scale bản đồ)
- Turn base: 120 deg/s (hệ số cơ sở trong công thức turn rate)
- Lưu ý: nếu EnginePower/Hull = 1 → gia tốc = 5.0; nếu >1 → gia tốc >5

------------------------------
5) BẢNG VÍ DỤ TÍNH SẴN (dựa trên dữ liệu tàu bạn cung cấp)
Giả sử: a = (Power/Hull) × 5.0 ; turn = 120 × (P/H) × 1/(1+v/200) ; warp_base = 10

Các tàu (Power / Hull / MaxSpeed):
- Scout: Power=500 / Hull=500 / MaxSpeed=300
- Interceptor (máy bay đánh chặn): Power=1200 / Hull=1200 / MaxSpeed=300
- Tàu khu trục: Power=1000 / Hull=1000 / MaxSpeed=270
- Kẻ hủy diệt: Power=2000 / Hull=2000 / MaxSpeed=250
- Cruiser (tuần dương): Power=4500 / Hull=4500 / MaxSpeed=230
- Battle (tàu chiến): Power=9000 / Hull=9000 / MaxSpeed=200
- Dreadnought (thiết giáp hạm): Power=15000 / Hull=15000 / MaxSpeed=160
- Prototype (nguyên mẫu): Power=20000 / Hull

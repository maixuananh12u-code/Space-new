===============================
= MISSING GAME SYSTEMS – PACK =
=      Version 1.0            =
===============================

================================
1. AI NON-COMBAT SYSTEM
================================

1.1 AI Exploration (Khám phá)
- AI quét các ô xung quanh theo hình vuông.
- Ưu tiên mở rộng đến:
  + Ô chưa khám phá
  + Ô có tài nguyên
  + Ô có cổng dịch chuyển
- Tránh ô có hải tặc mạnh (Threat > 3).

1.2 AI Expand Territory (Mở rộng lãnh thổ)
- AI chiếm ô khi:
  + Tài nguyên > 50%
  + Không có kẻ thù gần
  + Đang thiếu tài nguyên quan trọng
- Không mở rộng khi giáp đội yếu.

1.3 AI Resource Management (Thu thập tài nguyên)
- Tự chọn mỏ tốt nhất trong phạm vi 5 ô.
- Chọn ưu tiên theo:
  1) Kim loại
  2) Pha lê
  3) Plasma
  4) Tài nguyên hiếm
- Tránh mỏ trong vùng nguy hiểm.

1.4 AI Building Logic (Xây dựng)
- Xây mỏ khi tài nguyên < 60%.
- Xây nhà máy khi đang thiếu tàu.
- Xây trung tâm nghiên cứu khi tồn kho tài nguyên cao.

1.5 AI Diplomacy (Ngoại giao)
- Thân thiện nếu:
  + Khoảng cách xa
  + Không cạnh tranh lãnh thổ
- Thù địch nếu:
  + Tranh cùng mỏ
  + Tấn công trước
  + Tàu bị phá nhiều lần

1.6 AI Patrol (Tuần tra)
- Tuần tra 2–4 ô giữa căn cứ và biên giới.
- Tăng gấp đôi tuần tra nếu:
  + Có hải tặc ở trong phạm vi 3 ô.

1.7 AI Trade (Thương mại)
- Gửi tàu vận tải giữa 2 hệ sao nếu lợi nhuận > 25%.
- Tránh đường đi nguy hiểm.

================================
2. STAR & PLANET SYSTEM (HỆ SAO – HÀNH TINH)
================================

2.1 Loại sao
- Sao Vàng (Chuẩn): Tài nguyên ổn định.
- Sao Xanh: Tăng tốc độ nghiên cứu 20%.
- Sao Đỏ: Tài nguyên nhiều hơn 30% nhưng nguy hiểm hơn.
- Sao Trắng: Cho phép công nghệ nâng cấp đặc biệt.
- Sao Neutron: Hiếm → chứa vật phẩm đặc biệt.

2.2 Loại hành tinh
- Rocky Planet: Kim loại nhiều.
- Ice Planet: Pha lê nhiều.
- Gas Planet: Plasma nhiều.
- Bio Planet: Dùng cho công trình đặc biệt.
- Dead Planet: Ít tài nguyên nhưng rẻ để chiếm.

2.3 Chỉ số hành tinh
- Resource_Rate: tốc độ khai thác.
- Defense_Level: giáp tự nhiên.
- Hazard_Level: nguy hiểm tự nhiên.

2.4 Kết nối thiên hà
- Mỗi ô có thể chứa:
  + 1 hệ sao
  + 0–5 hành tinh
  + Mỏ tài nguyên
  + Dị thường (anomaly)
  + Hạm đội

================================
3. BUILDING SYSTEM (CÔNG TRÌNH)
================================

3.1 Mỏ tài nguyên (Mining Station)
- Tăng tài nguyên theo:
  Output = Base × Planet Resource_Rate

3.2 Nhà máy tàu (Shipyard)
- Tạo tàu mới.
- 3 cấp độ: Light / Medium / Heavy.

3.3 Trung tâm nghiên cứu (Research Lab)
- +15% tốc độ nghiên cứu.
- Yêu cầu năng lượng cao.

3.4 Trạm phòng thủ (Defense Station)
- Bắn tự động vào kẻ thù.
- Có thể nâng cấp theo cấp độ sao.

3.5 Kho năng lượng (Energy Core)
- Tăng dung lượng tối đa +20%.

================================
4. TECH TREE (CÂY CÔNG NGHỆ)
================================

4.1 Ngành: Quân sự
- Tăng sát thương
- Mở vũ khí mới
- Giáp từ thấp đến cao

4.2 Ngành: Kinh tế
- Tăng tài nguyên
- Giảm phí xây dựng
- Tăng tốc độ vận chuyển

4.3 Ngành: Khoa học
- Radar
- Tàng hình
- Drone hỗ trợ

4.4 Ngành: Sinh thái
- Hành tinh đặc biệt
- Mỏ năng lượng sinh học

================================
5. ECONOMY SYSTEM (KINH TẾ)
================================

5.1 Các loại tài nguyên chính
- Metal (Kim loại)
- Crystal (Pha lê)
- Plasma (Năng lượng)
- Rare-Ore (Khoáng hiếm)

5.2 Thuế vùng
- Hệ sao trung tâm thu thuế 5–10%.
- Vùng biên giới không thu thuế.

5.3 Thương mại
TradeProfit = (Giá bán – Giá mua) × Số lượng

5.4 Hạm đội vận tải
- Tự động vận chuyển giữa 2 trạm giao dịch.
- Bị cướp nếu đi qua vùng nguy hiểm.

================================
6. EXPLORATION (THĂM DÒ)
================================

6.1 Fog of War
- Không thể thấy tàu địch ngoài tầm radar.
- Hành tinh mới không hiện chi tiết nếu chưa khảo sát.

6.2 Anomaly (dị thường)
- Cho phần thưởng ngẫu nhiên:
  + Tài nguyên hiếm
  + Công nghệ
  + Tàu đặc biệt

6.3 Radar System
- Radar_Tier1: 2 ô
- Radar_Tier2: 4 ô
- Radar_Tier3: 6 ô

================================
7. PLAYER PROGRESSION (TIẾN TRÌNH NGƯỜI CHƠI)
================================

7.1 Level
- Cấp càng cao mở tàu mới.

7.2 Unlock
- Unlock vũ khí cấp cao.
- Unlock công nghệ.

7.3 Reputation (Uy tín)
- Uy tín cao = nhiều liên minh.
- Uy tín thấp = bị săn đuổi.

================================
8. UI / HUD LOGIC
================================

8.1 Minimap
- Hiển thị ô đã khám phá.
- Hiện kẻ địch trong radar.

8.2 Combat Log
- Ghi sát thương, phá giáp, kích nổ.

8.3 Indicators
- Mũi tên hướng kẻ địch
- Cảnh báo giáp thấp
- Cảnh báo năng lượng thấp

===============================
= END OF MISSING SYSTEM PACK =
===============================

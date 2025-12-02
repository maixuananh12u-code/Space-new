========================================
= GALAXY GAME – SYSTEM PACK (NO EVENTS)
= Version 1.0
========================================

=========================
1. AI NON-COMBAT SYSTEM
=========================

1.1 AI Exploration (Khám phá)
- AI mở rộng tầm nhìn theo ô vuông.
- Ưu tiên khám phá ô có:
  + Tài nguyên
  + Hành tinh
  + Dị thường
  + Cổng dịch chuyển
- Tránh vùng có kẻ địch mạnh.

1.2 AI Expand Territory (Mở rộng lãnh thổ)
- Chiếm ô khi:
  + Không có địch gần
  + Cần tài nguyên
  + Khu vực an toàn
- Không mở rộng khi lực lượng yếu.

1.3 AI Resource Management (Thu tài nguyên)
- Chọn mỏ chất lượng cao nhất trong 5 ô.
- Ưu tiên:
  1) Kim loại
  2) Pha lê
  3) Plasma
  4) Hiếm
- Tránh mỏ trong vùng nguy hiểm.

1.4 AI Building Logic (Xây dựng)
- Xây mỏ khi tài nguyên thấp.
- Xây nhà máy khi thiếu tàu.
- Xây phòng thủ khi biên giới yếu.
- Xây nghiên cứu khi dư tài nguyên.

1.5 AI Diplomacy (Ngoại giao)
- Thân thiện nếu không tranh lãnh thổ.
- Thù địch nếu:
  + Tranh mỏ
  + Tấn công trước
  + Đụng độ nhiều lần.

1.6 AI Patrol (Tuần tra)
- Tuần tra giữa căn cứ và biên giới.
- Tăng tuần tra khi có hải tặc gần.

1.7 AI Trade (Thương mại)
- Vận chuyển giữa hệ sao có lợi nhuận > 20%.
- Tránh đường nguy hiểm.


=========================
2. STAR & PLANET SYSTEM
=========================

2.1 Loại sao
- Sao Vàng: Cân bằng.
- Sao Đỏ: +30% tài nguyên, nguy hiểm.
- Sao Xanh: +20% nghiên cứu.
- Sao Trắng: Công nghệ đặc biệt.
- Sao Neutron: Hiếm, có kho báu.

2.2 Loại hành tinh
- Rocky: Kim loại cao.
- Ice: Pha lê cao.
- Gas: Plasma cao.
- Bio: Vật liệu sinh học.
- Dead: Tài nguyên thấp, rẻ để chiếm.

2.3 Chỉ số hành tinh
- Resource_Rate  
- Defense_Level  
- Hazard_Level

2.4 Cấu trúc hệ sao
- Số hành tinh: 0–5
- Mỏ tài nguyên
- Vật thể lạ (anomaly)
- Tàu NPC hoặc hải tặc


=========================
3. BUILDING SYSTEM
=========================

3.1 Mining Station (Mỏ)
Output = Base × Planet Resource_Rate

3.2 Shipyard (Nhà máy tàu)
- Tạo tàu
- 3 cấp độ: Light / Medium / Heavy

3.3 Research Lab (Nghiên cứu)
- +15% tốc độ nghiên cứu

3.4 Defense Station (Phòng thủ)
- Tự động bắn địch
- Nâng cấp theo cấp sao

3.5 Energy Core (Kho năng lượng)
- +20% dung lượng năng lượng


=========================
4. TECH TREE SYSTEM
=========================

4.1 Nhánh Quân Sự
- Tăng sát thương
- Mở giáp mới
- Unlock vũ khí cấp cao

4.2 Nhánh Kinh Tế
- Tăng tài nguyên
- Giảm chi phí xây dựng
- Tăng vận chuyển

4.3 Nhánh Khoa Học
- Radar
- Tàng hình
- Drone hỗ trợ

4.4 Nhánh Sinh học
- Mỏ bio
- Công trình đặc biệt

=========================
5. ECONOMY SYSTEM
=========================

5.1 Tài nguyên
- Metal (Kim loại)
- Crystal (Pha lê)
- Plasma (Năng lượng)
- Rare-Ore (Hiếm)

5.2 Thuế hệ sao
- Trung tâm: thuế 10%
- Biên giới: không thuế

5.3 Công thức lợi nhuận
TradeProfit = (Sell – Buy) × Amount

5.4 Hạm đội vận tải
- Vận chuyển giữa vùng thương mại
- Bị tấn công trong vùng nguy hiểm


=========================
6. EXPLORATION SYSTEM
=========================

6.1 Fog of War
- Không thấy địch ngoài tầm radar
- Hành tinh chưa khảo sát → ẩn thông tin

6.2 Anomaly (Dị thường)
- Ngẫu nhiên:
  + Tài nguyên hiếm
  + Buff hành tinh
  + Drone cổ đại

6.3 Radar Tiers
- Tier 1 → 2 ô
- Tier 2 → 4 ô
- Tier 3 → 6 ô


=========================
7. PLAYER PROGRESSION
=========================

7.1 Level System
- Level cao = tàu mới + vũ khí mới

7.2 Reputation (Uy tín)
- Cao → liên minh dễ hơn
- Thấp → bị săn đuổi

7.3 Unlock Tree
- Tàu mới mở theo level
- Module mở theo nghiên cứu


=========================
8. UI / HUD SYSTEM
=========================

8.1 Minimap
- Hiện ô đã khám phá
- Hiện địch trong tầm radar

8.2 Combat Log
- Hiện sát thương
- Giáp bị phá
- Khiên sập

8.3 Indicators
- Cảnh báo giáp thấp
- Cảnh báo năng lượng thấp
- Mũi tên hướng kẻ địch

==================================
= END OF FULL SYSTEM PACK v1.0   =
==================================

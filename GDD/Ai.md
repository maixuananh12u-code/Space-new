AI SYSTEM – FULL VERSION

1. OVERVIEW
Hệ thống AI điều khiển tàu NPC gồm 4 phần:
- Combat AI (chiến đấu)
- Pathfinding AI (di chuyển & né tránh)
- Formation AI (đội hình)
- Tactical AI (chiến thuật nâng cao)

---

2. COMBAT AI – AI CHIẾN ĐẤU
2.1. Tấn công
- Bắn theo cooldown
- Ưu tiên phá giáp trước thân
- Chọn vũ khí theo tầm bắn
- Dùng kỹ năng khi tỷ lệ trúng ≥ 60%
- Tập trung bắn vào tàu yếu hoặc nguy hiểm

2.2. Phòng thủ
- Bật khiên khi bị focus
- Né boost khi đạn sắp trúng
- Xoay tàu giảm sát thương
- Tắt vũ khí để hồi năng lượng
- Dùng kỹ năng tránh né (EMP, Jammer)

2.3. Rút lui
Điều kiện rút lui:
- HP < 20%
- Armor = 0
- Energy < 10%
- Bị >2 tàu khóa mục tiêu

Hành vi rút lui:
- Boost tối đa
- Đổi hướng 90°
- Dùng skill làm chậm địch

---

3. TARGETING AI – CHỌN MỤC TIÊU

Ưu tiên mục tiêu:
1. Tàu có giáp yếu nhất
2. Tàu đang dùng vũ khí mạnh
3. Tàu gần nhất
4. Tàu đang khóa mục tiêu vào AI
5. Tàu trong tầm bắn tối ưu

Đổi mục tiêu khi:
- Mục tiêu sắp nổ
- Vượt ra khỏi tầm
- Xuất hiện mục tiêu nguy hiểm hơn

---

4. TACTICAL AI – CHIẾN THUẬT NÂNG CAO

4.1. Basic AI
- Tấn công đơn giản
- Ít né
- Không phối hợp đồng đội

4.2. Advanced AI
- Né boost
- Chọn mục tiêu hợp lý
- Dùng skill theo tình huống

4.3. Elite AI
- Dành cho boss và kẻ địch mạnh
- Combo skill
- Bao vây, chia cắt đội hình
- Gọi hỗ trợ

---

5. PATHFINDING AI – DI CHUYỂN & NÉ TRÁNH

- Tránh thiên thạch, mảnh vỡ
- Tránh vùng AOE
- Di chuyển theo vector 3D
- Boost sang trái/phải khi né
- Lật tàu 45° để giảm sát thương

Công thức né:
EvasionChance = Evasion / (Evasion + Aim)

AI né nếu:
- Đạn bay thẳng hướng
- Impact < 0.6s

---

6. FORMATION AI – ĐỘI HÌNH

6.1. Wedge (mũi tên)
- Tàu mạnh đứng đầu
- Tàu hỗ trợ ở sau

6.2. Circle (bao vây)
- Tấn công từ nhiều góc

6.3. Line (hàng dọc)
- Tank trước, DPS sau

6.4. Scatter (tản ra)
- Dùng khi bị AOE

---

7. AI BOSS – HÀNH VI BOSS

Boss có 3–5 pha:

Pha 1:
- Bắn cơ bản
- Gọi drone

Pha 2:
- Tăng tốc
- Dùng skill mạnh
- AOE

Pha 3:
- Sát thương ×1.5
- Tốc độ ×2
- Tấn công dồn dập

Boss không rút lui.

---

8. AI STATS – CHỈ SỐ

ReactionTime: 0.1–0.4s
Aggression: 30–90
RetreatThreshold: 15–25%
Aim: 30–70
Evasion: 20–60
Teamwork: 20–100

---

9. CÔNG THỨC

Đổi mục tiêu:
SwitchScore = Threat + (DPS / HP) × 2 + DistancePenalty

Tấn công:
Attack = (HitChance > 45%) AND (Energy > 20%)

Né:
Evade = (IncomingProjectile) AND (ImpactTime < 0.6)

---

KẾT THÚC FILE

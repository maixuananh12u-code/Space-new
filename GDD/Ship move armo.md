# SHIPS — Full Specs (Ship / Armor / Shields / Engine / Cargo)

## Ghi chú chung
- Power (Công suất) = dùng để tính gia tốc.
- Hull = HP vật lý.
- Shield = điểm lá chắn.
- ShieldRegen/s = hồi khiên mỗi giây.
- Armor = giảm sát thương (%).
- MaxSpeed = tốc độ tối đa (unit/s).
- WeaponSlots = số ô vũ khí.
- Cargo = sức chứa tài nguyên.
- TurnRate, Accel, WarpSpeed tính theo công thức chung (EnginePower / Hull).

-----------------------------------------------------------------------
## 1) Scout (Tàu trinh sát)
- Power: 500
- Hull: 500
- Shield: 200
- ShieldRegen/s: 10
- Armor: 5% 
- MaxSpeed: 300
- WeaponSlots: 3
- Cargo: 150
- Notes: nhẹ, cơ động, ít giáp

## 2) Interceptor (Máy bay đánh chặn)
- Power: 1200
- Hull: 1200
- Shield: 700
- ShieldRegen/s: 35
- Armor: 8%
- MaxSpeed: 300
- WeaponSlots: 3
- Cargo: 150
- Notes: tốc độ cao, phù hợp tàu nhỏ/tấn công nhanh

## 3) Destroyer (Tàu khu trục)
- Power: 1000
- Hull: 1000
- Shield: 600
- ShieldRegen/s: 18
- Armor: 10%
- MaxSpeed: 270
- WeaponSlots: 4
- Cargo: 500
- Notes: cân bằng tấn công/phòng thủ

## 4) Cruiser (Tuần dương)
- Power: 4500
- Hull: 4500
- Shield: 1000
- ShieldRegen/s: 20
- Armor: 18%
- MaxSpeed: 230
- WeaponSlots: 7
- Cargo: 1400
- Notes: tàu chiến chủ lực, nhiều ô vũ khí

## 5) Battle (Tàu chiến)
- Power: 9000
- Hull: 9000
- Shield: 1200
- ShieldRegen/s: 24
- Armor: 20%
- MaxSpeed: 200
- WeaponSlots: 9
- Cargo: 3500
- Notes: hạng nặng, chịu đòn tốt

## 6) Dreadnought / Thiết giáp hạm
- Power: 15000
- Hull: 15000
- Shield: 2000
- ShieldRegen/s: 40
- Armor: 25%
- MaxSpeed: 160
- WeaponSlots: 12
- Cargo: 3500+
- Notes: cực bền, chậm, tiêu hao năng lượng lớn

## 7) Prototype (Tàu nguyên mẫu)
- Power: 20000
- Hull: 20000
- Shield: 4000
- ShieldRegen/s: 40
- Armor: 30% (giảm 30% sát thương)
- MaxSpeed: 100
- WeaponSlots: 15
- Cargo: 6000
- Special: giảm 30% sát thương, công nghệ độc nhất

-----------------------------------------------------------------------
# Engine / Movement formulas (áp dụng cho mọi tàu)
- Acceleration a = (Power / Hull) × 5.0 (units/s²)
- Time to TopSpeed t = MaxSpeed / a
- Stopping distance d = 0.5 × MaxSpeed² / a
- TurnRate (deg/s) = 120 × (Power/Hull) × (1 / (1 + MaxSpeed/200))
- WarpSpeed = BaseWarp × (Power/Hull) ; BaseWarp = 10 units/s

# Shield / Armor interaction (tóm tắt)
- Damage to shield: apply shield multipliers (ví dụ Plasma II ×3 lên khiên)
- NetShieldDPS = WeaponDPS × ShieldMultiplier − ShieldRegen/s
- Damage to hull after shield broken: Damage × (1 − Armor%)

-----------------------------------------------------------------------
# Ví dụ nhanh (các chỉ số để dùng tính TTK / DPS)
- Scout: Accel=5.00, TurnRate=48 deg/s, WarpSpeed=10 u/s
- Cruiser: Accel=5.00, TurnRate≈55.81 deg/s, WarpSpeed=10 u/s
- Prototype: Accel=5.00, TurnRate=80 deg/s, WarpSpeed=10 u/s

-----------------------------------------------------------------------
# Hướng dẫn gắn file
- Đặt file này là `ships_full.md` trong thư mục GDD.  
- Nếu muốn tách ra: chia theo phần “Ship Specs”, “Engine formulas”, “Shield & Armor rules”.  
- Mình có thể xuất cùng file dưới dạng JSON nếu muốn load trực tiếp vào engine.

# COMBAT_FORMULA
HIT_CHANCE_BASE = 80                  # % chính xác cơ bản
EVADE_BASE = 5                        # % né cơ bản
CRITICAL_CHANCE = 0.08                # % crit
CRITICAL_DAMAGE = 1.5                 # Sát thương crit x1.5
DAMAGE_VARIANCE = 0.10                # ±10% sát thương
ARMOR_REDUCTION_FACTOR = 0.65         # Hệ số giảm sát thương theo giáp
SHIELD_REGEN_RATE = 0.02              # Hồi khi thoát combat (%)
FOCUS_FIRE_BONUS = 1.25               # Tập trung hỏa lực tăng sát thương
MAX_COMBAT_RANGE = 900                # Tầm combat tối đa
COMBAT_TIME_SCALE = 1.0               # Tốc độ chiến đấu

# Công thức tính sát thương cuối:
# FinalDamage = (BaseDamage ± Variance) * (1 - Armor * ARMOR_REDUCTION_FACTOR)
# Nếu crit: FinalDamage *= CRITICAL_DAMAGE

# Công thức tính hit:
# HitChance = HIT_CHANCE_BASE + WeaponAccuracy - TargetEvasion
# Nếu HitChance < 5% → nâng lên 5%

# Công thức né:
# Evasion = EVADE_BASE + ShipSpeed / 10

------------------------------------------------------------

# FLEET_MANAGEMENT
MAX_FLEET_SIZE = 40                   # Số lượng tàu tối đa trong 1 hạm đội
COMMAND_POINT_BASE = 10               # Điểm điều khiển cơ bản
COMMAND_POINT_PER_SHIP = 1            # Mỗi tàu tiêu tốn CP
FLEET_SPEED_FACTOR = 0.85             # Ảnh hưởng khi hạm đội quá nặng
FORMATION_BONUS = 1.10                # Đội hình chuẩn tăng 10% phòng thủ
MORALE_SYSTEM = true                  # Dùng hệ thống sĩ khí
MORALE_MAX = 100                      # Sĩ khí tối đa
MORALE_LOSS_PER_DEATH = 8             # Mỗi tàu bị phá hủy giảm sĩ khí
MORALE_BUFF_AT_HIGH = 0.1             # >75 morale tăng 10% sát thương
MORALE_DEBUFF_AT_LOW = -0.15          # <25 morale giảm 15% sát thương
REPAIR_RATE = 0.015                   # % hồi hull ngoài combat
AUTO_REINFORCE = true                 # Hạm đội tự bổ sung tàu nếu có sẵn

------------------------------------------------------------

# NPC_SYSTEM
NPC_SPAWN_RATE = 0.12                 # Tỷ lệ sinh NPC mỗi vùng
NPC_MAX_LEVEL = 15                    # Cấp NPC tối đa
NPC_DIFFICULTY_SCALE = 1.25           # Tăng độ khó theo thời gian
NPC_FACTION_VARIETY = 6               # Số loại phe NPC
NPC_TRADER_CHANCE = 0.18              # % xuất hiện thương nhân
NPC_PIRATE_CHANCE = 0.33              # % xuất hiện hải tặc
NPC_DEFENDER_CHANCE = 0.22            # % hệ thống tự vệ
NPC_AI_INTELLIGENCE = 0.65            # Độ thông minh AI NPC

# NPC hành vi:
#  – Trader: tránh combat 90%, tăng giá 15%, có thể bị cướp
#  – Pirate: ưu tiên bắn tàu yếu/đơn lẻ, tấn công chủ động
#  – Defender: chỉ bắn mục tiêu thù nghịch hoặc vào vùng cấm
#  – Warlord: mini-boss, xuất hiện theo chu kỳ 15–20 phút
#  – Alien: sát thương cao, giáp yếu, rất nhanh

------------------------------------------------------------

===============================
COMBAT FORMULA — FLEET — NPCS
Version: 1.0
Copy-ready
===============================

PART A — COMBAT FORMULA (công thức + ví dụ đã tính)

1) Hệ số & hằng số
HIT_CHANCE_BASE = 80%        # độ chính xác cơ bản
EVADE_BASE = 5%              # tỉ lệ né cơ bản
CRITICAL_CHANCE = 8%         # tỉ lệ chí mạng
CRITICAL_MULT = 1.5          # chí mạng x1.5
DAMAGE_VARIANCE = ±10%       # biến thiên sát thương
ARMOR_REDUCTION_FACTOR = 0.65 # hệ số khi tính giảm theo armor
SHIELD_REGEN_COMBAT = 0.02   # 2%/s khi ngoài combat
FOCUS_FIRE_BONUS = 1.25      # bắn hội đồng tăng 25%

2) Công thức chính (text)
- RawDamage = BaseDamage * (1 ± DAMAGE_VARIANCE)
- ArmorEffect = ArmorPercent * ARMOR_REDUCTION_FACTOR
  (ArmorPercent là 0.00–1.00; ví dụ 20% → 0.20)
- DamageAfterArmor = RawDamage * (1 − ArmorEffect)
- Nếu crit: DamageAfterArmor *= CRITICAL_MULT
- Nếu target has Shield > 0 → apply damage to Shield first:
  ShieldNew = max(0, ShieldOld − DamageAfterArmor)
  If DamageAfterArmor > ShieldOld then RemainingDamage = DamageAfterArmor − ShieldOld; apply RemainingDamage to Hull after armor reduction.

3) Ví dụ số cụ thể
- BaseDamage = 100
- Var ±10% → RawDamage ∈ [90,110] → lấy 100 cho ví dụ
- Target Armor = 20% → ArmorPercent = 0.20
- ArmorEffect = 0.20 * 0.65 = 0.13
- DamageAfterArmor = 100 * (1 − 0.13) = 87.00
- Nếu crit: 87 * 1.5 = 130.50

4) Hit / Miss
- HitChance = HIT_CHANCE_BASE + WeaponAccuracy − TargetEvasion
- Minimum HitChance = 5%
- Ví dụ: WeaponAccuracy 10, TargetEvasion 8 → HitChance = 80 + 10 − 8 = 82%

5) Evade formula (dùng cho tính tự động)
- Evasion = EVADE_BASE + (ShipSpeed / 10)  (ShipSpeed đơn vị unit/s)
- Ví dụ: ShipSpeed = 300 → Evasion = 5 + 30 = 35%

6) Tầm & falloff
- Full damage within OptimalRange.
- Linear falloff from OptimalRange → MaxRange: damage scales to 50% at MaxRange.
- Ví dụ: OptimalRange = 500, MaxRange = 900. At distance 700 → falloff = (700−500)/(900−500)=0.5 → damage *= (1 − 0.5*0.5) = approx 0.75 (tùy hệ số bạn chọn).

--------------------------------------------------------------------------------

PART B — FLEET MANAGEMENT (Quản lý hạm đội) + phép tính ví dụ

1) Thiết lập & hằng số
MAX_FLEET_SHIPS = 40
COMMAND_POINTS_BASE = 10
CP_PER_SHIP = 1
FLEET_SPEED_FACTOR = 0.85    # khi gom nhiều tàu, speed = min(ship speeds) * FLEET_SPEED_FACTOR
FORMATION_BONUS = 1.10       # +10% phòng thủ nếu giữ formation
MORALE_MAX = 100
MORALE_LOSS_PER_LOST_SHIP = 8
REPAIR_RATE_OUT_OF_COMBAT = 1.5% per minute (ví dụ REPAIR_RATE = 0.015)

2) Quy tắc chi phí chỉ huy
- FleetCP = COMMAND_POINTS_BASE + sum(CP_PER_SHIP per ship)
- Ví dụ: Fleet có 20 tàu → FleetCP = 10 + 20 = 30
- Nếu FleetCP > MAX_FLEET_SHIPS (40) → không cho tạo (hoặc phạt hiệu suất)

3) Tốc độ hạm đội
- FleetSpeed = min(all ship MaxSpeed) * (1 − overload_penalty)
- overload_penalty = max(0, (FleetMass / FleetMassCapacity) − 1) * 0.3
- Ví dụ đơn giản: 10 tàu, min speed = 250 → FleetSpeed ≈ 250 * 0.85 = 212.5 (dùng FLEET_SPEED_FACTOR)

4) Hệ thống formation (lợi ích)
- Formation types: Line, Wedge, Circle, Scatter
- Formation Bonus áp dụng: Damage taken * (1 / FORMATION_BONUS) ; FormBonus default = 1.10
- Ví dụ: Nếu đội hình Line active → damage taken giảm ~9% (1/1.10=0.909)

5) Sĩ khí (Morale)
- MORALE ∈ [0,100]
- MORALE loss: mỗi tàu mất → −MORALE_LOSS_PER_LOST_SHIP
- MORALE effects:
  - MORALE > 75 → +10% damage
  - MORALE < 25 → −15% damage
- Ví dụ: ban đầu 100 → sau mất 3 tàu: 100 − 3*8 = 76 → vẫn giữ +10% damage

6) Tự sửa chữa & Reinforce
- REPAIR_RATE_OUT_OF_COMBAT = 1.5% hull per minute
- Auto reinforce: nếu AUTO_REINFORCE = true và available ships ở shipyard → thêm vào fleet (tuỳ config)

--------------------------------------------------------------------------------

PART C — NPC SYSTEM (Hệ thống NPC) + thông số mẫu đã tính

1) Hằng số & tỉ lệ
NPC_SPAWN_RATE = 0.12           # spawn chance per tick per region
NPC_MAX_LEVEL = 15
NPC_DIFFICULTY_SCALE = 1.25
NPC_FACTION_VARIETY = 6
NPC_TRADER_CHANCE = 18%
NPC_PIRATE_CHANCE = 33%
NPC_DEFENDER_CHANCE = 22%

2) Các loại NPC & hành vi tóm tắt
- Trader:
  - Avoid combat 90%
  - Carry trade goods, offer buy/sell at market ± market variation
- Pirate:
  - Aggressive, target single isolated ship
  - Spawn in clusters (2–6)
- Defender:
  - Station/Planet defenders
  - Only attack hostile targets
- Warlord (mini-boss):
  - Spawn cyclically, higher loot
- Alien:
  - High speed, high dmg, low armor (special faction)

3) Spawn logic (ví dụ)
- Each region tick (10s), roll random: if rand < NPC_SPAWN_RATE → spawn NPC
- Choose type by weighted chance: Pirate 33, Trader 18, Defender 22, Others fill remaining

4) NPC scaling over time
- NPC Level = base + floor(GameTimeHours / 3) * growthFactor
- Example: after 6 hours, growth adds floor(6/3)=2 → scale * (NPC_DIFFICULTY_SCALE^2)

5) Trader economics (sample)
- Trader buys at MarketPrice * (1 − 0.05) ; sells at MarketPrice * (1 + 0.05)
- Trader risk: if path crosses PirateZones → chance of loss 10–35% depending on zone.

6) Pirate raid composition example
- Early game raid (threat ~2): 3 × Fighters + 1 × Frigate
- Mid game raid (threat ~5): 6 × Fighters + 2 × Corvettes + 1 × Destroyer
- Boss raid (threat >10): includes Warlord / Dreadnought

--------------------------------------------------------------------------------

PART D — SAMPLE TABLES (đã tự tính, copy-ready)

A) Mining Station Output per Level (Base = 12 resource/min, multiplier 1.35 per level)
Level 1: 12.00 /min
Level 2: 16.20 /min
Level 3: 21.87 /min
Level 4: 29.52 /min
Level 5: 39.86 /min
Level 6: 53.81 /min
Level 7: 72.64 /min
Level 8: 98.07 /min
Level 9: 132.39 /min
Level10: 178.72 /min

B) Research Tech Cost (Base 500 Science, multiplier 1.6 per level)
Level1: 500
Level2: 800
Level3: 1,280
Level4: 2,048
Level5: 3,276.80
Level6: 5,242.88
Level7: 8,388.61
Level8: 13,421.78
Level9: 21,474.84
Level10: 34,359.74

C) Build / Upgrade Costs (example: Mining Station)
Base build cost: Metal 200 / Crystal 50 / Time 120s
Upgrade multiplier per level: 1.5
Level1 cost: Metal 200 / Crystal 50 / Time 120s
Level2 cost: Metal 300 / Crystal 75 / Time 180s
Level3 cost: Metal 450 / Crystal 112 / Time 270s
Level4 cost: Metal 675 / Crystal 168 / Time 405s
(rounded to integers where needed)

D) Ship build time sample (Shipyard level 1, speed = 1x)
Example ship metal cost / base build points:
- Frigate: Metal 500 → BuildTime = 500 / (ShipyardSpeed * 10) seconds = 50s
- Cruiser: Metal 2,000 → BuildTime = 2000 / 10 = 200s
(Adjust divisor 10 as ShipyardSpeed constant to tune)

--------------------------------------------------------------------------------

PART E — HOW TO INTEGRATE (gợi ý dev)
1) Put combat formulas in Combat module (damage pipeline: weapon → hit check → shield → armor → hull)
2) Fleet module should manage groups, CP, formation states and call Combat module when fleets meet
3) NPC manager spawns NPCs based on region config and uses AI combat + non-combat behaviors already in your AI files
4) Tech/Research hooks call LAB module using tech costs table above
5) Building upgrades use Mining Station table & upgrade multiplier to compute outputs/time/cost

--------------------------------------------------------------------------------

END OF FILE
===============================

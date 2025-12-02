# ============================
# 1. SHIP DATA (TÀU CHIẾN)
# ============================

[SHIP_SMALL_FIGHTER]
name = "Fighter"
hull = 1200
armor = 300
shield = 500
speed = 3.5
turn_rate = 2.1
cargo = 10
weapon_slots = 2
size = "small"
role = "interceptor"

[SHIP_MEDIUM_FRIGATE]
name = "Frigate"
hull = 3500
armor = 900
shield = 1400
speed = 2.2
turn_rate = 1.5
cargo = 40
weapon_slots = 4
size = "medium"
role = "general_combat"

[SHIP_HEAVY_DESTROYER]
name = "Destroyer"
hull = 7500
armor = 2000
shield = 3000
speed = 1.6
turn_rate = 1.0
cargo = 80
weapon_slots = 6
size = "large"
role = "frontline_tank"


# ============================
# 2. WEAPON DATA (VŨ KHÍ)
# ============================

[WEAPON_LASER_BASIC]
name = "Basic Laser"
type = "laser"
damage = 35
fire_rate = 0.4
energy_cost = 6
range = 520
accuracy = 0.92

[WEAPON_PLASMA_CANNON]
name = "Plasma Cannon"
type = "plasma"
damage = 80
fire_rate = 1.2
energy_cost = 18
range = 420
accuracy = 0.85

[WEAPON_RAILGUN]
name = "Railgun"
type = "kinetic"
damage = 150
fire_rate = 1.8
energy_cost = 0
range = 680
accuracy = 0.78
armor_penetration = 40

[WEAPON_MISSILE_TRACKING]
name = "Tracking Missile"
type = "missile"
damage = 250
reload = 4.5
ammo = 20
tracking = 0.7
range = 900


# ============================
# 3. MATERIAL & RESOURCES
# ============================

[RESOURCE_IRON]
name = "Iron"
rarity = "common"
use = "ship_hull"

[RESOURCE_TITANIUM]
name = "Titanium"
rarity = "uncommon"
use = "armor_upgrade"

[RESOURCE_ENERGY_CORE]
name = "Energy Core"
rarity = "rare"
use = "shield_generator"

[RESOURCE_PLASMA_FUEL]
name = "Plasma Fuel"
rarity = "uncommon"
use = "plasma_weapon"

[RESOURCE_QUANTUM_CHIP]
name = "Quantum Chip"
rarity = "rare"
use = "AI, advanced systems"

[RESOURCE_DARK_MATTER]
name = "Dark Matter"
rarity = "epic"
use = "warp_drive, high tier weapons"


# ============================
# END OF FILE
# ============================

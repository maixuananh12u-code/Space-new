{
  "resources": {
    "Metal": { "type": "basic", "description": "Dùng để xây tàu và công trình." },
    "Crystal": { "type": "basic", "description": "Dùng cho vũ khí năng lượng và nâng cấp." },
    "Fuel": { "type": "consumable", "description": "Dùng để di chuyển tàu." },
    "Energy": { "type": "generated", "description": "Dùng cho hoạt động và công trình." },
    "Credits": { "type": "currency", "description": "Tiền tệ chung dùng cho giao dịch." }
  },

  "ships": [
    {
      "id": "frigate_01",
      "name": "Frigate",
      "class": "Frigate",
      "hp": 1200,
      "armor": 100,
      "shield": 300,
      "speed": 3.2,
      "cp_cost": 1,
      "weapons": ["laser_mk1"],
      "build_cost": { "Metal": 120, "Crystal": 40, "Fuel": 20 },
      "role": "Skirmisher"
    },
    {
      "id": "destroyer_01",
      "name": "Destroyer",
      "class": "Destroyer",
      "hp": 2400,
      "armor": 200,
      "shield": 450,
      "speed": 2.6,
      "cp_cost": 2,
      "weapons": ["laser_mk1", "kinetic_mk1"],
      "build_cost": { "Metal": 220, "Crystal": 80, "Fuel": 40 },
      "role": "Balanced"
    },
    {
      "id": "cruiser_01",
      "name": "Cruiser",
      "class": "Cruiser",
      "hp": 5000,
      "armor": 450,
      "shield": 900,
      "speed": 2.0,
      "cp_cost": 4,
      "weapons": ["plasma_mk1", "missile_mk1"],
      "build_cost": { "Metal": 500, "Crystal": 180, "Fuel": 80 },
      "role": "Heavy Assault"
    }
  ],

  "weapons": [
    {
      "id": "laser_mk1",
      "name": "Laser Cannon Mk I",
      "type": "energy",
      "damage": 55,
      "fire_rate": 1.2,
      "accuracy": 0.85,
      "effectiveness": {
        "vs_shield": 1.2,
        "vs_armor": 0.7,
        "vs_hull": 1.0
      }
    },
    {
      "id": "kinetic_mk1",
      "name": "Kinetic Gun Mk I",
      "type": "kinetic",
      "damage": 75,
      "fire_rate": 0.9,
      "accuracy": 0.8,
      "effectiveness": {
        "vs_shield": 0.6,
        "vs_armor": 1.3,
        "vs_hull": 1.1
      }
    },
    {
      "id": "plasma_mk1",
      "name": "Plasma Cannon Mk I",
      "type": "plasma",
      "damage": 120,
      "fire_rate": 0.6,
      "accuracy": 0.75,
      "effectiveness": {
        "vs_shield": 1.1,
        "vs_armor": 1.1,
        "vs_hull": 1.1
      }
    },
    {
      "id": "missile_mk1",
      "name": "Missile Launcher Mk I",
      "type": "missile",
      "damage": 180,
      "fire_rate": 0.45,
      "accuracy": 0.65,
      "effectiveness": {
        "vs_shield": 0.5,
        "vs_armor": 1.4,
        "vs_hull": 1.3
      }
    }
  ],

  "armor": {
    "light": {
      "base_armor": 100,
      "damage_reduction": 0.08
    },
    "medium": {
      "base_armor": 250,
      "damage_reduction": 0.15
    },
    "heavy": {
      "base_armor": 500,
      "damage_reduction": 0.25
    }
  },

  "planets": {
    "types": [
      {
        "id": "terran",
        "name": "Terran",
        "slots": 6,
        "resource_bonus": { "Metal": 1.0, "Food": 1.2 },
        "habitability": 1.0
      },
      {
        "id": "desert",
        "name": "Desert",
        "slots": 4,
        "resource_bonus": { "Crystal": 1.3 },
        "habitability": 0.7
      },
      {
        "id": "ice",
        "name": "Ice World",
        "slots": 3,
        "resource_bonus": { "Fuel": 1.4 },
        "habitability": 0.6
      },
      {
        "id": "volcanic",
        "name": "Volcanic",
        "slots": 2,
        "resource_bonus": { "Metal": 1.5 },
        "habitability": 0.5
      }
    ]
  },

  "buildings": [
    {
      "id": "mine_metal",
      "name": "Metal Mine",
      "output": { "Metal_per_min": 12 },
      "energy_upkeep": 3,
      "slots_required": 1,
      "upgrade_mult": 1.35
    },
    {
      "id": "crystal_drill",
      "name": "Crystal Extractor",
      "output": { "Crystal_per_min": 8 },
      "energy_upkeep": 4,
      "slots_required": 1,
      "upgrade_mult": 1.35
    },
    {
      "id": "farm",
      "name": "Hydroponic Farm",
      "output": { "Food_per_min": 14 },
      "energy_upkeep": 2,
      "slots_required": 1
    },
    {
      "id": "research_lab",
      "name": "Research Laboratory",
      "output": { "Science_per_min": 10 },
      "energy_upkeep": 5,
      "slots_required": 1
    },
    {
      "id": "shipyard",
      "name": "Shipyard",
      "output": { "ProductionSpeed": 10 },
      "energy_upkeep": 8,
      "slots_required": 2
    }
  ],

  "tech_tree": [
    {
      "id": "tech_laser_mk2",
      "name": "Laser Upgrade Mk II",
      "tier": 1,
      "cost": 600,
      "prereq": [],
      "effects": { "laser_damage_mult": 1.2 }
    },
    {
      "id": "tech_engine_mk2",
      "name": "Engine Upgrade Mk II",
      "tier": 1,
      "cost": 650,
      "prereq": [],
      "effects": { "fleet_speed_mult": 1.15 }
    },
    {
      "id": "tech_mining_mk2",
      "name": "Advanced Mining",
      "tier": 1,
      "cost": 500,
      "prereq": [],
      "effects": { "mine_output_mult": 1.35 }
    },
    {
      "id": "tech_shield_mk2",
      "name": "Shield Mk II",
      "tier": 2,
      "cost": 1200,
      "prereq": ["tech_laser_mk2"],
      "effects": { "shield_hp_mult": 1.25 }
    }
  ],

  "factions": [
    {
      "id": "nova_empire",
      "name": "Nova Empire",
      "personality": "Aggressive",
      "starting_resources": { "Metal": 300, "Crystal": 150, "Fuel": 200 },
      "ai_style": "military"
    },
    {
      "id": "aurora_union",
      "name": "Aurora Union",
      "personality": "Balanced",
      "starting_resources": { "Metal": 250, "Crystal": 200, "Fuel": 150 },
      "ai_style": "balanced"
    },
    {
      "id": "helion_collective",
      "name": "Helion Collective",
      "personality": "Scientific",
      "starting_resources": { "Metal": 200, "Crystal": 250, "Fuel": 150 },
      "ai_style": "research"
    }
  ]
}

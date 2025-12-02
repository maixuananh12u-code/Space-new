========================================
CORE SYSTEMS — FULL PACKAGE (COPY READY)
Filename suggestion: CoreSystems_Full.md
Version: 1.0
========================================

INTRO
This document bundles core systems needed to run the game's main loop and link all modules:
- Gameplay Loop
- UI Structure
- Time / Tick System
- Planet & Building System
- Technology (Tech Tree)
- Navigation (Grid / Movement across Galaxy)

Use this as the canonical spec to implement engine logic or to paste into your GDD repo.

----------------------------------------
1) GAMEPLAY LOOP (MAIN FLOW)
----------------------------------------
Purpose: define one game cycle that repeats, drives economy, AI, combat, research, construction.

Loop tick = GAME_TICK (default 1 second)
High-level steps per loop (order matters):
1. TickTimeAdvance: advance global time by GAME_TICK.
2. IncomePhase: collect resource generation from planets/buildings (per minute rates prorated to tick).
3. MaintenancePhase: apply upkeep costs (ships/buildings) if maintenance system active.
4. AIPhase: run AI Non-Combat decisions (expand, build, trade).
5. MovementPhase: move fleets between tiles (apply FleetSpeed, collisions, arrival checks).
6. EncounterPhase: resolve NPC/player encounters (trigger combat if opposing forces meet).
7. CombatPhase: run combat resolution for all active battles (use Combat Formula).
8. Repair/Recovery Phase: apply out-of-combat repair and shield regen.
9. Build/Research Phase: progress ship/building production and tech research queues.
10. UI Update: refresh player UI elements / send events to client.

Example loop timing:
- GAME_TICK = 1s → Income/minute rates converted to per-second for accuracy.
- Some subsystems (AI, market update) may run on slower sub-ticks (e.g., every 5s or 30s) to save CPU.

Core rules:
- Deterministic order: Movement -> Encounters -> Combat ensures fair resolution.
- Use queues for build/research; progress = (productionRate / requiredCost) * GAME_TICK.

----------------------------------------
2) UI STRUCTURE (LAYOUT & CORE PANELS)
----------------------------------------
Goal: minimal but complete UI screens/panels for core gameplay.

Top-level UI screens:
- Main Menu
- In-Game HUD
- Galaxy Map (grid)
- Planet View
- Fleet Manager
- Ship Detail Panel
- Shipyard / Production Panel
- Research / Tech Tree Panel
- Diplomacy / Alliance Panel
- Market / Trade Panel
- Pause / Settings

HUD elements (in-combat & out-of-combat):
- Top bar: Resources (Metal, Crystal, Fuel, Energy, Credits)
- Left pane: Fleet list / Selected fleet
- Right pane: Context actions (Build, Research, Move, Attack)
- Bottom bar: Quick actions, Notifications, Time control (Pause / 1x / 2x / 5x)
- Minimap/Galaxy mini: shows grid with owned tiles, enemy presence, selected tile

Galaxy Map specifics:
- Tile info popup: owner, security level, resources, stations, fleets present
- Path drawing: show calculated path and fuel/time cost when plotting move
- Selection: click tile to open Planet View or station window

Planet View:
- Top: Planet name, type, population, stability
- Middle: Building slots grid (visual 2×2 / 3×3 depending on planet tier)
- Bottom: Actions: Build / Upgrade / Queue / Transfer resources

Fleet Manager:
- Fleet list with CP usage, morale, speed, current mission
- Fleet detail view: ship composition, formation, repair status

Tech Tree UI:
- Visual nodes, prerequisites, cost/time buttons, progress bars

Design notes:
- Keep UI modular: panels are independent widgets to reuse.

----------------------------------------
3) TIME & TICK SYSTEM
----------------------------------------
Purpose: unify time handling across all systems.

Constants:
- GAME_TICK = 1.0 (seconds)  -- base simulation tick
- SLOW_TICK = 5.0 (seconds) -- run heavy AI / market updates
- MINUTE = 60 * GAME_TICK

Time helpers:
- convertPerMinuteRateToPerTick(rate_per_minute) = rate_per_minute / 60 * GAME_TICK
- progressIncrement = (productionPower * GAME_TICK) / requiredCost

Subsystems scheduling:
- Income/Resource: every GAME_TICK (for smoothness)
- AI decisions: every SLOW_TICK
- Market price update: every 30 * GAME_TICK
- NPC spawn checks: every SLOW_TICK

Determinism:
- For multiplayer or replay, ensure order and random seeds are stable per tick.

----------------------------------------
4) PLANET & BUILDING SYSTEM
----------------------------------------
Goal: planets are economic & strategic nodes. Provide building slots, population, yields.

Planet model (per planet):
- id, tileCoord (x,y), type (Terran/Desert/Ice/Volcanic/Gas/Barren/Bio), population, stability, resourceRates, buildingSlots, defenseLevel

Key stats:
- Resource_Rate: baseResourcePerMinute (per resource type)
- PopulationGrowthRate: base per minute, influenced by Food and Stability
- Stability: [-100..+100] affects output and rebellion chance

Planet Tiers:
- Outpost (1 slot)
- Colony (3 slots)
- Developed (6 slots)
- Core Planet (9 slots)

Building list (examples):
- Mining Station (Metal/Crystal/Other outputs) -- scalable level 1..N
- Power Plant (Energy generation)
- Farm (Food production)
- Research Lab (Science/Tech points)
- Shipyard (produces ships, queue)
- Defense Platform (planet defense turret)
- Storage Depot (increases local cargo cap)
- Trade Hub (enables trade missions; increases market access)

Building rules:
- Each building consumes buildCost: {metal, crystal, timeSec, energyUpkeep}
- Buildings provide perMinute output; convert to perTick when applying
- Buildings have upgrade paths: upgradeMultiplier (output/time/cost)

Sample building math (copyable):
- MINE_BASE_OUTPUT = 12 (resource units per minute)
- MINE_UPGRADE_MULT = 1.35
- output(level) = MINE_BASE_OUTPUT * (MINE_UPGRADE_MULT^(level-1))

Population and growth:
- Growth per minute = BaseGrowth * (FoodSupply / FoodDemand) * StabilityFactor
- If FoodSupply < FoodDemand → population declines at declineRate

Storage and transfer:
- Each planet has localStorageCapacity; transports move resources between tiles
- TransferTime = distance / shipSpeed (use fleet speed formula)

Planet capture & control:
- To capture a planet: reduce defenseHP to 0, occupy with ground troops or capture module OR complete occupation mission (depending on game design)
- Occupied planets can revolt if Stability < threshold

----------------------------------------
5) BUILDING & PRODUCTION QUEUES
----------------------------------------
Production model:
- Each ship/building has Cost {metal, crystal, timeSec}
- Production progresses as:
  progress += (ShipyardProductionPower * GAME_TICK)
- Finish when progress >= timeSec

Shipyard rules:
- ShipyardLevel increases productionSpeed = baseSpeed * (1 + (level-1)*0.25)
- Shipyard queue length = baseQueue + level

Auto-reinforce:
- If AUTO_REINFORCE enabled, queued ships can be automatically added to fleet if criteria met (available CP, docked)

Maintenance:
- Optional: periodic resource drain for maintenance (ships/buildings)
- Example: MAINTENANCE_PER_SHIP = 2 credits / minute

----------------------------------------
6) TECHNOLOGY (TECH TREE)
----------------------------------------
Tech node model:
- id, name, tier, prerequisites[], cost {sciencePoints}, researchTimeSec, effects (unlock/modify stats)

Tech categories:
- Military (weapons, armor, ship hulls)
- Economy (mining efficiency, production speed)
- Science (radar, anomaly analysis)
- Propulsion (warp, engine upgrades)
- Special (ancient tech, dark matter harness)

Research rules:
- Research points generated by Research Labs and planetary science output
- ResearchQueue: player/lab pools science into active tech
- Research speed multiplier from Alliance / bonuses

Sample tech cost curve:
- BaseCost = 500 science points
- cost(level) = BaseCost * (1.6^(level-1))  -> precomputed table recommended

Tech effects (examples):
- Laser Mk II: +20% laser damage
- Shipyard Mk II: +25% ship production speed
- Mining Mk II: +35% mine output

----------------------------------------
7) NAVIGATION & GRID MOVEMENT (GALAXY GRID)
----------------------------------------
Grid model:
- Galaxy is NxN grid (tile coordinates x:0..N-1, y:0..N-1)
- Tile contains: owner (faction/null), systems[], warpGates, hazards

Movement basics:
- Fleets move tile-to-tile along orthogonal neighbors by default (N/S/E/W)
- Optional diagonal moves if unlocked
- MovementCost between adjacent tiles:
  baseCost = 1 unitDistance
  costModifier = tileHazardMultiplier (nebula >1.2, asteroid >1.1, blackhole huge)
  fuelCost = baseFuelPerTile * costModifier * FleetMassFactor
  timeCost = baseTimePerTile / FleetSpeedModifier

Pathfinding:
- Use A* on grid where tile cost = timeCost (or fuelCost) to return optimal path
- For performance, cache paths for large fleets and invalidated when tiles change ownership/hazard

Warp/Jump logic:
- Two modes: SubLight (tile-by-tile) and WarpJump (long jump via WarpGate)
- WarpJump requires Fuel and cooldown; instant or fast movement between gates
- Gate network is pre-generated or player-built

Blockers & Outcomes:
- Entering hostile tile may trigger ambush/pirate spawn or auto-combat
- When multiple fleets meet on same tile -> encounter resolved (combat module)

Fleet arrival:
- On arrival, execute queued actions: occupy, reinforce planet, trade, dock, attack

----------------------------------------
8) DATA & INTEGRATION NOTES
----------------------------------------
Integration tips for devs:
- Expose per-tick APIs: onTick(), onSlowTick()
- Keep data normalized: separate static definitions (units, costs) from dynamic state
- Use deterministic RNG with seeded random for reproducible outcomes
- Maintain event logs for debugging (combat log, AI decisions)
- For large maps, partition galaxy into regions/chunks for performance

----------------------------------------
9) SAMPLE CONSTANTS (copy into config)
----------------------------------------
GAME_TICK = 1.0
SLOW_TICK = 5.0
GALAXY_SIZE = 30
MINE_BASE_OUTPUT = 12
MINE_UPGRADE_MULT = 1.35
SHIPYARD_BASE_SPEED = 10.0
RESEARCH_BASE_COST = 500
FLEET_CP_BASE = 10
MAINTENANCE_PER_SHIP = 2  # credits/min

----------------------------------------
END OF CORE SYSTEMS PACKAGE
========================================

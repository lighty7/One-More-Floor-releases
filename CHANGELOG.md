# Changelog

Notable changes, newest first. The format follows [Keep a Changelog](https://keepachangelog.com/).
Builds are published on the [Releases](https://github.com/lighty7/One-More-Floor-releases/releases) page;
one per build (`v0.1.<build>-alpha`).

## Unreleased

### Added
- Touch controls for phones: a move stick wherever your left thumb lands (push past the ring
  to sprint), drag to look, fire / aim / reload / jump / duck / melee / swap buttons, plus
  use, build and upgrade buttons when they apply. On by default on phones, a switch and a look
  speed in Settings > Controls. Menus get a close button; double-tap equips an item. The
  Android APK is now in every release.
- Android build (arm64 APK, CI download for testing; joins the releases with touch controls):
  Compatibility renderer, starts on Low quality, 60 FPS cap, at most 20 wandering zombies.
  Leaving the app opens the pause menu and saves (except at night, so it can't skip a wave).
- Linux (x86_64) build of the game: a `Linux` export preset, built by CI and published on
  every release as `OneMoreFloor-<version>-Linux.zip`.
- New city road network: a ring road, curved arteries meeting at a central plaza and irregular
  streets in between, all from the seed, on a fixed-size map. `tools/city_map.gd` draws any seed from above; `road_tests`
  checks 100 seeds (connected, no crossings, plaza and arteries, never a grid).
- The pause menu shows the map's seed, with a button to copy it.
- Weather options in Settings > Gameplay: fixed weather or the daily roll, rain / weather fog /
  lightning flashes on or off, rain amount.
- Arena: the host picks the match weather (or random each match); dedicated servers take
  `--weather=`.
- Documentation: code style guide, testing guide, contributing guide, this changelog, pull
  request and issue templates, a new README with screenshots.
- `tests/run_all.sh` runs every test suite with a summary.
- CI checks formatting and lint (gdtoolkit) on every push and pull request.
- Every script has a doc comment, and so do the public functions whose name doesn't say it all.

### Changed
- Every game key (hotbar 1-4 and wheel, reload, drop, map, K/B/C menus, build rotate / upgrade /
  cancel, arena loadout and scoreboard) now goes through an input action instead of a hard-coded
  key, ready for touch controls. Same default keys.
- The city is rebuilt on the new road network (no more 5x5 grid): a map four times wider, buildings
  lining every street with their doors to the road, districts that follow the roads, and new
  landmarks (city park, gas station, and a farm, cabins or junkyard at the end of each out-road).
  Every room, upstairs included, and every landmark can be reached on foot, and the base core
  can't be placed where zombies can't follow (roofs, sealed corners). Navigation bakes in tiles,
  so a much bigger map is ready faster and building only rebakes around the base.
- First-person view: the gun and arms have their own narrower field of view (no stretching at
  the screen edges, never through walls), the arms keep their real length instead of stretching
  to reach long guns, hands at true size, and new hip and sprint holds.
- Every gun has hand-picked hold points: the right hand on the real handle, the left hand on the
  real foregrip / pump / fore-end, and the sight line through the optic's centre, so scopes and
  red dots line up with the crosshair when aiming. The carbine model is levelled.
- Hands: each finger and the thumb are posed for what the hand holds (trigger finger on the
  grip, the left hand round a vertical foregrip, under a handguard or wrapped over the right
  hand on a pistol, fists when unarmed) instead of one curl for every finger. The hands lie flat
  against the gun, so fingers no longer curl over a pistol's slide or the sights.
- More ammo: drops are about a magazine and come more often; containers hold more. Then 25% more
  again in every zombie drop, container and dawn payout (pistol drops 18-33, rifle 30-50, shotgun
  10-18).
- Less muzzle smoke from your own gun (none while aiming down the sights).
- Multiplayer protocol 3: update the dedicated server together with the game.
- Tests: the tracer check moved into `combat_tests`; `run_tests` renamed `logic_tests`.
- Code: every declaration is statically typed and an untyped one no longer compiles; members
  other scripts use are public (no more reaching into `_private` ones).

- Code: the player script is split into the player (movement, health, input), its weapons
  and its first-person view.

### Removed
- The old whirlwind / blink-strike abilities (no longer unlockable) and other unused code.
- The unused hand-made test floor inside every dungeon floor (built and thrown away on each floor).

### Fixed
- Phones: FIRE and AIM did nothing (shooting waited for a captured mouse, which a touchscreen
  never has). The touch controls also hide while the arena loadout is open, and let go of AIM
  when they hide.
- DONE (right-click) always leaves build mode, even when the piece preview can't be shown.
- Some rooms could never be entered: a front door or the inner doorway sometimes landed on the
  wall splitting the front rooms, leaving two gaps too narrow to pass. Upper floors are easier to
  reach: the stair ramp starts from a landing and runs straight onto the floor above.
- Restarting (pause menu) or New Game on the end screen built the same map again; both now
  use the typed seed or a new random one.
- Zombies no longer hit you through walls when they're close to the other side.
- New walls change zombie paths within about a second (was about two).
- The Settings panel was wider than the screen, hiding the switches and lists on the right.
- Loot containers without a table pointed at a loot table that doesn't exist.
- A white placeholder sword could show in view when starting unarmed.
- The engine logged a bogus "missing dungeon_floor.gd" error on every load (a circular load).

## 0.1 alpha
Earlier releases (`v0.1.x-alpha`), most recently:
- **Arena (multiplayer):** free-for-all for up to 10 players with timed rounds, server-checked hits
  with lag compensation, scoreboard, kill feed, synced building and damage; a dedicated Linux server
  with a systemd service and installer.
- **Weapons:** recorded gunshots per gun, travelling tracers, impacts by surface, bullet holes;
  a permanent gun shop with upgrades; more snipers (Kar98k, hunting rifle, anti-materiel rifle).
- **Base:** storage chests, realistic building pieces with doors, gates, windows and roofs.
- **Clean-up:** unused assets removed (game data 359 → 218 MB).

See the [releases](https://github.com/lighty7/One-More-Floor-releases/releases)
for the full history.

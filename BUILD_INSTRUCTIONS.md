# DiaSwords — Build Instructions

## Build via GitHub Actions (recommended)
1. Unzip this, make sure hidden files are visible (Windows: View → Hidden items;
   Mac: Cmd+Shift+.) so the `.github` folder comes along.
2. Push everything to a GitHub repo (drag-and-drop upload, or git push).
3. If `.github/workflows/build.yml` doesn't show up in your repo after upload,
   create it manually: Add file → Create new file → name it
   `.github/workflows/build.yml` → paste in the contents of that file from this zip.
4. Go to the **Actions** tab — it builds automatically.
5. When green, open the run → **Artifacts** → download **DiaSwords**.
6. Unzip it, you'll find `DiaSwords.jar`.
7. Drop it into your server's `plugins/` folder, restart.

## Build locally instead
Requires JDK 21 + Maven.
```
cd DiaSwords
mvn package
```
Output: `target/DiaSwords.jar`

## What's in this version

**4 swords** (all Netherite Sword base, admin-give only):

| Sword | Trigger | Effect |
|---|---|---|
| Dash | Shift + right-click | Dash forward, brief fall-damage immunity |
| Lightning | Passive (on hit) | 10% chance per hit to strike lightning + bonus damage |
| Vampire | Passive (on hit) | Heals you a % of damage dealt, capped per hit, optional heal sound |
| Explosive | Shift + right-click | Fires a real fireball, explodes on impact, block damage off by default, shooter immune to own blast by default |

Frost and Vortex have been removed from this version.

## Commands
`/diaswords give <player> <sword>` — sword names: `dash`, `lightning`, `vampire`, `explosive`
`/diaswords list` — list sword types
`/diaswords reload` — reload config without restarting

## Configuration (config.yml)
Everything is tunable — cooldowns, damage, proc chance, heal %, fireball power, etc.
New in this version:
- `general.ability-used-sound` — set `false` to mute all ability sounds server-wide (particles still show)
- `general.default-enchants` — a list of enchantments (by Minecraft ID, e.g. `sharpness`,
  `looting`, `mending`, `unbreaking`, `fire_aspect`, `sweeping_edge`) automatically applied
  to every sword given via `/diaswords give`. Levels can exceed vanilla max since these
  are unsafe/admin enchants.
- `vampire-sword.heal-sound` — plays a short chime when the vampire sword actually heals you

After editing config.yml on your server, run `/diaswords reload` to apply changes.

## Notes
I wrote and reviewed this code carefully by hand, including verifying the exact Paper
1.21.11 API methods and Minecraft enchantment registry keys. I could not compile it
myself (no internet access in my sandbox), so please test it before going fully live,
and let me know if the build fails or anything behaves unexpectedly.

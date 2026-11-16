# Dead Man's Deck: Free Asset List (v2, Sea of Thieves direction)

Look target (GDD 2.2): Sea of Thieves readability + Dredge atmosphere. Real PBR textures,
believable proportions, with the "stylized" part coming from **lighting, fog and color**
(turquoise fog #14B8A6, amber lanterns #F59E0B) rather than from cartoony models.

**Anchor source: Poly Haven's "Smuggler's Cove" (17th-century, CC0).** Everything else should match its look.

## Ship, deck, props (Poly Haven, CC0, no account needed)
Download from https://polyhaven.com, pick **FBX** or **glTF** and **2K** textures (4K is too heavy).

| Asset | Use in game | Link |
|---|---|---|
| Dutch Ship Large 01 / 02 | L'Écorché (player galleon) | https://polyhaven.com/a/dutch_ship_large_01 |
| Dutch Ship Medium | Background ships in the fog | https://polyhaven.com/a/dutch_ship_medium |
| Ship Pinnace | Boarding raft (fracture with Chaos) | https://polyhaven.com/a/ship_pinnace |
| Cannon 01 | 4 broadside cannons | https://polyhaven.com/a/cannon_01 |
| Wooden Handle Saber | Player cutlass | https://polyhaven.com/a/wooden_handle_saber |
| Wooden Barrels 01 / Barrel 01-03 | Sapper powder barrel, deck clutter | https://polyhaven.com/a/wooden_barrels_01 |
| Wooden Lantern 01 / Lantern 01 | Amber lights at firing posts | https://polyhaven.com/a/wooden_lantern_01 |
| Wooden Crate 01/02, Wooden Bucket, Treasure Chest | Deck dressing, Altar base | https://polyhaven.com/models |
| Seadogs Compass | Detail prop | https://polyhaven.com/a/seadogs_compass |
| Modular Wooden Pier | Planks for the 8 railings / repair pieces | https://polyhaven.com/a/modular_wooden_pier |
| Wood plank textures + night/overcast HDRIs | Deck material, sky | https://polyhaven.com/textures , https://polyhaven.com/hdris |

Overview of the whole set: https://polyhaven.com/collections/smugglers_cove

## Enemies and weapons (Fab, free; log in with your Epic account)
"Personal" Fab license = free for non-commercial use (fine for a uni project; selling on Steam
as the GDD imagines would need the paid license).

| Asset | License | Use | Link |
|---|---|---|---|
| **Human Skeleton** (Salt Lake Manor): rigged, modular, aged bone texture, Unreal format | CC-BY (credit the author) | Skeleton Swordsman + Sapper (add a Poly Haven barrel) | https://www.fab.com/listings/b3b80a03-58b6-4125-b1ef-0b8508f12ed6 |
| **Wheellock Pistol** (Dan3D): realistic PBR, Unreal format | Personal: free | Flintlock pistol (right click) | https://www.fab.com/listings/d4d2461e-73b9-4859-a227-d43a35e0d664 |

## Animations
- **Mixamo** (free, Adobe account): https://www.mixamo.com. Upload the skeleton FBX, then download
  sword attack, walk, climb, hit react and death animations. Import into Unreal and retarget with the IK Retargeter.
- **Unreal's built-in Third Person pack** (Content Drawer → Add → Add Feature or Content Pack →
  Third Person): walk/run/idle for the skeletons until the Mixamo animations are in.

## Built into Unreal (no download)
- **Water** plugin: ocean around the ship
- **Exponential Height Fog + Volumetric Fog**: turquoise #14B8A6
- **Point lights** on the lanterns: amber #F59E0B
- **Sky Atmosphere + Volumetric Clouds**: night/dusk
- **Fracture mode (Chaos)**: break the pinnace and railing planks
- **FPS arms**: start with the template arms; the sabre/pistol attach to their hand sockets

## Audio
| Pack | License | Use | Link |
|---|---|---|---|
| Sonniss GDC 2026 Game Audio Bundle | Royalty-free (no AI training) | Cannon fire, wood breaking, waves, ship bell, creaks | https://sonniss.com/gameaudiogdc |
| Kenney Impact / RPG audio | CC0 | Sword hits, reload clicks | https://kenney.nl/assets/category:Audio |

## Font
- **Pirata One** (Google Fonts, OFL): HUD titles and menus: https://fonts.google.com/specimen/Pirata+One

## Import tips
- Folders: `Content/Assets/PolyHaven/`, `Content/Assets/Characters/Skeleton/`, `Content/Assets/Weapons/`.
- Poly Haven models are real-world scale in meters; Unreal uses cm. Check the scale on import (Import Uniform Scale = 100 if it comes in tiny).
- Use 2K textures; the ship at 4K is 400+ MB.
- Keep a `CREDITS.txt`: required for the CC-BY skeleton, good practice for everything else.

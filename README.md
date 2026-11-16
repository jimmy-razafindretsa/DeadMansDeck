# Dead Man's Deck — *Le Pont du Revenant*

A first-person arcade **boarding-defense wave shooter** built in **Unreal Engine 5.8** (Blueprint-only).

You are the **Revenant Captain**, alone on the deck of the cursed galleon *L'Écorché*. You defend it against waves of skeleton boarders rising out of the spectral fog. Shatter their rafts at sea with heavy broadside cannons (Chaos physics). When their grappling hooks smash through your railings, switch to cutlass and flintlock.

📄 **Full Game Design Document (French):** [`DeadMansDeck_GDD_FR.pdf`](DeadMansDeck_GDD_FR.pdf) · text version: [`Docs/GDD.md`](Docs/GDD.md)

## At a Glance

| | |
|---|---|
| **Genre** | FPS Wave Defense / Arcade Gunner |
| **Engine** | Unreal Engine 5.8 (Chaos Destruction, Lumen) |
| **Platform** | PC (Windows / Mac) |
| **Team** | Solo developer |
| **Rating** | ESRB T (13+) |
| **Target delivery** | Early December 2026 |

## Key Features
- **Two scales of combat:** switch instantly between heavy artillery at sea and close-quarters sabre/pistol fights on deck.
- **Tactical Chaos destruction:** 8 destructible, repairable railing segments act as physical barricades.
- **Revenant's Pact (double survival gauge):** you lose if your HP **or** the ship's hull integrity reaches 0.
- **Active Reload:** press again inside the golden window to reload faster and gain bonus damage.
- **Altar of Souls:** spend Soul Shards between waves to unlock deck weapons.

## Core Loop
**Spot (360°)** → **Artillery** → **Chaos impact** → **Skirmish on deck** → **Lull** (repair and upgrade). One run takes 15–20 minutes over 8–10 waves.

## Controls

| Action | Keyboard / Mouse | Gamepad |
|---|---|---|
| Move / Aim | WASD + Mouse | Left / Right stick |
| Sabre / Fire cannon | Left Click | RT / R2 |
| Flintlock pistol | Right Click | LT / L2 |
| Active Reload | R | X / Square |
| Take/leave cannon · Repair/Altar | E · F (hold) | Y · B |

## Milestones

| Milestone | Target | Deliverables |
|---|---|---|
| M1 — Engine & Greybox | Nov 8, 2026 | Galleon greybox, FPS controller, broadside cannon ballistics |
| M2 — First Playable | Nov 15, 2026 | Spline raft approach, Chaos raft/railing destruction, NavMesh + skeleton, melee |
| M3 — Core Loop Complete | Nov 22, 2026 | Wave director, hull + player HP, railing repair, Active Reload, Altar of Souls |
| M4 — Alpha (Look & Feel) | Nov 29, 2026 | Dark Cartoon art pass, Lumen fog, 3D audio, full HUD, final wave |
| M5 — Gold Master | Early Dec 2026 | Wave balancing, 60 FPS optimization, menus, packaged build |

## Getting Started
1. Install **Unreal Engine 5.8**.
2. Clone the repo and open `DeadMansDeck.uproject`.
3. The startup map is `/Game/FirstPerson/Lvl_FirstPerson`.

Contributor and agent guidelines are in [`AGENTS.md`](AGENTS.md).

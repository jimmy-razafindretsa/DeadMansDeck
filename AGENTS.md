# AGENTS.md — DeadMansDeck

The rules for any coding agent working in this repository. They are mandatory.

## 1. Project Overview

**Design source of truth:** the French GDD v1.0. Read [`Docs/GDD.md`](Docs/GDD.md), the text version. Don't parse [`DeadMansDeck_GDD_FR.pdf`](DeadMansDeck_GDD_FR.pdf), which is the original with figures. Check the GDD before designing any gameplay system, enemy, weapon, HUD element, or control binding. Follow its **Vital / Désiré** priorities and milestone schedule (M1–M5, ending early December 2026). If a request conflicts with the GDD, flag the conflict to the user.

**Game summary:** a first-person arcade boarding-defense wave shooter. The player is the Revenant Captain defending the galleon deck: cannons sink skeleton rafts, and sabre plus flintlock clear boarders. Destructible Chaos railings act as barricades. The player loses if their HP or the hull integrity reaches 0.

| Item | Value |
|---|---|
| Engine | Unreal Engine **5.8** (`EngineAssociation` in `DeadMansDeck.uproject`) |
| Project type | **Blueprint-only**: no `Source/` folder, no C++ modules |
| Template base | First Person (Manny/Quinn mannequins, Level Prototyping kit) |
| Startup / default map | `/Game/FirstPerson/Lvl_FirstPerson` (World Partition, One File Per Actor) |
| Default GameMode | `/Game/FirstPerson/Blueprints/BP_FirstPersonGameMode` |
| Input | Enhanced Input (`EnhancedPlayerInput` / `EnhancedInputComponent`) |

**Enabled plugins** (from `.uproject`):
- `ModelingToolsEditorMode` (Editor only)
- `GameplayStateTree`
- `ModelContextProtocol` (editor MCP server, `http://127.0.0.1:8000/mcp`, see `.mcp.json`)
- `AllToolsets` (MCP toolsets: Scene, Actor, Blueprint, Material, UMG, etc.)

## 2. Directory Map & Boundaries

```text
DeadMansDeck_GDD_FR.pdf     Original GDD (binary; use Docs/GDD.md instead)
Docs/GDD.md                 GDD text version (read this for design questions)
Config/                     Engine/Game/Input/Editor .ini (text, safe to read and edit)
Content/
├── Characters/Mannequins/  Template anims (Pistol/Rifle/Unarmed/Death), meshes, rigs, mats
├── FirstPerson/            Lvl_FirstPerson.umap, Blueprints/ (Character, PC, GameMode, CameraMgr), Anims/
├── Input/                  IMC_Default, IMC_MouseLook, Actions/ (IA_*), Touch/ (UI_*)
├── LevelPrototyping/       Interactables (BP_DoorFrame, BP_JumpPad, BP_WobbleTarget), meshes, mats
├── Collections/, Developers/
└── __ExternalActors__/, __ExternalObjects__/   World Partition OFPA data (managed by the editor)
```

- Put new gameplay content under `Content/DeadMansDeck/<Feature>/` (for example `Cards/`, `Player/`, `UI/`, `Core/`). Do not mix it into template folders.
- **Never** scan, read, grep, `cat`, diff, or edit binary `.uasset` / `.umap` files directly.
- **Never** read or index these build/cache folders: `Binaries/`, `Intermediate/`, `Saved/`, `DerivedDataCache/`, `.vs/`.
- **Never** touch `__ExternalActors__/` or `__ExternalObjects__/` by hand. Change level actors only through the editor.
- You may list file *names* (for example `find Content -name "BP_*"`) to discover assets.

## 3. Naming Conventions

Every **new** asset must use one of these prefixes. Template assets keep their original names (for example `SKM_`, `UI_`, `Lvl_`). Do not rename them unless asked.

| Prefix | Asset type | Prefix | Asset type |
|---|---|---|---|
| `BP_` | Blueprint class | `SK_` | Skeletal mesh |
| `BPI_` | Blueprint interface | `ABP_` | Animation Blueprint |
| `WBP_` | Widget Blueprint (UMG) | `IA_` | Input Action |
| `M_` | Material | `IMC_` | Input Mapping Context |
| `MI_` | Material instance | `DT_` | Data table |
| `MF_` | Material function | `E_` | Enum |
| `SM_` | Static mesh | `S_` | Struct |
| `T_` | Texture | `L_` | Level (new maps) |

Use PascalCase after the prefix (`BP_CardDeck`, `WBP_HealthBar`). Do not use spaces or special characters.

## 4. Blueprint-Only Workflow

- Do **not** create C++ (`.h` / `.cpp`, `Source/`, `.Build.cs`, `.Target.cs`) unless the user explicitly asks to convert the project to C++.
- **Order of preference** for touching assets:
  1. **Unreal MCP tools** (`unreal-mcp` server) when the editor is running and connected.
  2. **Editor Python** (`import unreal`) run inside the editor.
  3. **Manual instructions** for the user when no editor bridge is available.
- Save every modified asset explicitly. Never leave dirty packages.

```python
import unreal

asset = unreal.EditorAssetLibrary.load_asset("/Game/DeadMansDeck/Player/BP_Player")
# ...modify via SubobjectDataSubsystem / set_editor_property...
unreal.EditorAssetLibrary.save_loaded_asset(asset)
```

Useful Python APIs: `EditorAssetLibrary`, `EditorLevelLibrary` / `EditorActorSubsystem`, `SubobjectDataSubsystem`, `AssetToolsHelpers`, `BlueprintEditorLibrary`.

### Levels (`.umap`)
- **Warn the user before modifying any level.** Binary maps cannot be merged, and an open map may be locked or overwritten.
- Prefer changes inside Blueprints over per-level actor edits when the result is the same.

### Manual Blueprint specs (no editor bridge)
When you describe Blueprint logic for the user to wire by hand, include all of the following:
- The **Blueprint asset path and parent class**.
- **Variables:** name, type (for example `Integer`, `Float`, `Actor Object Reference`, `S_CardData Array`), default value, and instance-editable or replicated flags.
- **Event dispatchers** and their parameters.
- **Interfaces** (`BPI_*`) with function signatures.
- The **node graph**: numbered steps naming exact nodes (`Event BeginPlay` → `Get Player Controller` → `Cast To BP_FirstPersonPlayerController` → …), branch conditions, and pin connections.

Keep each graph as a separate fenced block per function or event.

## 5. Git & GitHub Rules

### Atomic commits
- Each commit is **one** logical, self-contained change: one feature, one fix, or one config update. Never bundle unrelated changes.
- Use imperative Conventional Commit messages:

```text
feat(player): add flashlight battery drain timer
fix(cards): prevent drawing from empty deck
chore(config): set default map to L_MainMenu
```

- Stage specific paths (`git add Content/DeadMansDeck/Cards/`). Do not use `git add -A` across unrelated work.
- Review `git status` before committing. Commit only assets related to the change, because the editor often dirties unrelated packages.

### Zero AI attribution
- **NEVER** add `Co-Authored-By:` trailers, "Generated by…" lines, AI or agent signatures, badges, or any mention of Claude, AI, or agents in:
  - commit messages, PR titles or descriptions, branch names
  - code or Blueprint comments, or any repository file
- Commits are authored **only** by the local git user (`git config user.name` / `user.email`). Never override the author.

### Binary safety
- **Never** run destructive commands on `Content/` or `Config/` without explicit user confirmation:
  `git checkout -- .`, `git restore .`, `git reset --hard`, `git clean -fd`, `git stash` (for assets), or force-push.
- `.uasset` / `.umap` cannot be merged. Overwriting them loses work permanently.
- Do not rewrite pushed history unless the user asks.
- Keep build/cache folders ignored (see `.gitignore`). Before adding any file over 50 MB, propose Git LFS (GitHub rejects files over 100 MB).

## 6. Quick Checklist
- [ ] No C++ added; changes made via MCP, Python, or manual spec
- [ ] New assets prefixed correctly and placed under `Content/DeadMansDeck/`
- [ ] Modified assets saved; user warned before any `.umap` change
- [ ] One logical change per commit, imperative message, no AI attribution

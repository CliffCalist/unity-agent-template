# Unity Project Organization

This document defines the Unity project structure and naming rules for project-owned assets. The conventions make an asset's owner, location, and type easy to identify.

The main principle: keep an asset with the feature that owns it. Use name prefixes to identify asset types instead of separate top-level folders for each type.

Keep project-owned files in `Assets/_Project`. Third-party assets may remain in their imported package folders; do not move or rename them mechanically.

These rules are a working standard, not a requirement to create every possible folder or name segment. Add structure when it improves navigation and readability.

## Naming

### General rules

Project-owned file and GameObject names contain no spaces. Use `PascalCase` for words and `_` to separate logical name segments.

An asset name should make sense regardless of its location:

```text
Prefix_Owner[_Context][_Variant]
```

| Segment | Meaning |
| --- | --- |
| `Prefix` | Technical asset type. |
| `Owner` | Feature or scope that owns the asset. |
| `Context` | Asset role within its owner; include it when clarification is needed. |
| `Variant` | Meaningful difference between variants; include it only when needed. |

Do not repeat information already conveyed by the prefix or context. For example, `SO_Player` does not need an additional `Config` segment.

| Prefix | Type |
| --- | --- |
| `P_` | Prefab |
| `SO_` | ScriptableObject asset |
| `M_` | Material |
| `T_` | Texture or sprite |
| `SCN_` | Scene |
| `SFX_` | Sound effect |
| `BGM_` | Music |
| `VFX_` | Visual effect |
| `ANIM_` | Animation clip |
| `AC_` | Animator controller |

Add a new prefix only when it is clear and genuinely makes assets easier to find.

### UI prefabs

These rules apply to prefabs. UI textures, materials, and ScriptableObject assets follow the general naming rules for their types.

Basic reusable UI elements have `UI` as their owner: `P_UI_Control_ButtonPrimary`, `P_UI_Popup_Base`. UI belonging to a specific feature uses that feature as its owner: `P_Shop_Popup_Offer`, `P_Economy_Widget_Wallet`.

The first context segment after the owner identifies the UI prefab role:

| Role | Meaning | Example |
| --- | --- | --- |
| `Screen` | Full-screen UI state | `P_Shop_Screen_Main` |
| `Popup` | Modal or semi-modal window | `P_Shop_Popup_ConfirmPurchase` |
| `Panel` | Large part of a screen or popup | `P_Shop_Panel_ProductDetails` |
| `Widget` | Small reusable UI block | `P_Economy_Widget_WalletBalance` |
| `View` | Presentation of a gameplay or model entity | `P_Character_View_Stats` |
| `Item` | List, grid, or inventory element | `P_Shop_Item_Product` |
| `Control` | Basic interactive component | `P_UI_Control_ButtonPrimary` |

### Models

FBX and other model files have no technical prefix. Their names include the owner and meaningful context: `TurkishSauna_Hanger_Bedroom.fbx`, `Services_Bottle.fbx`.

A prefab wrapping a model gets `P_`. Add `Model` to the context when it distinguishes the prefab from others: `P_TurkishSauna_Place_Model`.

### Hierarchy

The root GameObject of a prefab has the same name as the prefab asset. Name child GameObjects by their local role without repeating the owner:

```text
P_Shop_Popup_Offer
  Background
  Content
  TXT_Title
  IMG_Icon
  BTN_Close
```

Short role prefixes such as `BTN_`, `TXT_`, and `IMG_` are suitable for UI. For gameplay, names such as `Visual`, `Collider`, `SpawnPoint`, and `InteractionArea` are usually enough. Spell out unclear abbreviations.

## Project Structure

Base structure for project-owned files:

```text
Assets/_Project/
  Features/
  Scenes/
  Scripts/
```

`Features` contains feature-owned assets: prefabs, configuration, art, audio, and VFX. Keep an asset with its single clear owner. Do not collect all feature prefabs, materials, or settings in top-level `Prefabs`, `Materials`, or `Settings` folders.

This structure suits projects with enough features and dependencies to benefit from owner-based grouping. A small project may use a simpler structure without empty folder levels.

### Feature Structure

Example feature structure:

```text
Assets/_Project/Features/
  MyFeature/
    Art/
      Animations/
      Materials/
      Models/
      Sprites/
      Textures/
      VFX/
    Configs/
    Prefabs/
      UI/
```

These are possible folders, not a template to recreate in full. Create folders when they separate existing assets by useful context. One or two configuration assets can remain directly in the feature folder.

Related features may be grouped under a category, for example `Features/Services/TreatmentRooms/TurkishSauna/`. A category is unnecessary for a single feature.

Use `Prefabs/UI/` to separate UI prefabs when the feature also has gameplay prefabs. If all of its prefabs are UI, they may sit directly in `Prefabs/`.

### Shared Assets

`_Shared` contains assets used by multiple features when no single feature clearly owns them:

| Usage | Location |
| --- | --- |
| One feature | That feature folder |
| Multiple features in one category | `Features/FeatureCategory/_Shared/` |
| Multiple independent features | `Features/_Shared/` |

For example, decorative models shared by several services may live in `Features/Services/_Shared/Art/Models/`. A reusable prefab without its own logic does not necessarily become a separate feature. If a shared part gains its own logic and responsibility, make it a separate feature.

### Scenes

Keep project scenes in `Assets/_Project/Scenes/` with the `SCN_` prefix: `SCN_Preload.unity`, `SCN_Gameplay.unity`, `SCN_MainMenu.unity`.

A folder for baked scene data may repeat the scene name, for example `Assets/_Project/Scenes/SCN_Gameplay/`. Do not mechanically rename third-party sample scenes.

## Scripts

Recommended separation of scripts by responsibility:

```text
Assets/_Project/Scripts/
  Core/       — gameplay logic and game rules
  UI/         — state presentation and interaction handling
  Bootstrap/  — startup and composition
```

`Core` does not depend on `UI` or control its internal state. `UI` may read `Core` state or subscribe to its events. `Bootstrap` connects these parts when a scene or feature starts.

When gameplay needs a user action, `Core` defines a narrow contract named for the domain need. For example, `IRewardSelection` describes reward selection rather than a specific `Popup` or `Window`. UI implements the contract, and Bootstrap supplies that implementation to Core.

### Odin Inspector

If the project uses Odin Inspector, code attributes describe data rules and allowed values, such as `[Required]` and `[MinValue(0)]`.

Configure inspector presentation through Odin Visual Designer: grouping, order, decorative headers, spacing, and colors. Usually, 1–3 meaningful attributes per field are enough; visual settings should not clutter the code.

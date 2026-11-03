# Unity project file organization

This convention defines naming rules for project-owned assets and GameObjects in a Unity project. It also describes the folder structure for assets.

An asset's name identifies its type, owning feature, context, and variant. This helps you understand its purpose without opening it.

The folder structure follows the naming scheme: an asset's name indicates where to find it and where to add similar assets. Grouping assets by usage indicates which parts of the project an addition, deletion, or change might affect. This narrows the scope of searches and checks during development.

## Contents

- [Naming](#naming)
  - [Asset type prefixes](#asset-type-prefixes)
  - [UI assets](#ui-assets)
  - [Models](#models)
  - [GameObjects in a prefab](#gameobjects-in-a-prefab)
- [Folder structure](#folder-structure)
  - [Feature folders](#feature-folders)
  - [Shared assets](#shared-assets)

## Naming

Do not use spaces in project-owned filenames or GameObject names. Use `PascalCase` for words and `_` to separate logical name segments.

The [C# convention](unity-csharp-conventions.md) defines naming rules for scripts and types.

An asset's name should make sense regardless of its folder. Name model files without a type prefix, as described in [Models](#models). For assets whose types appear in the [prefix table](#asset-type-prefixes), use this scheme:

```text
Prefix_Owner[_Context][_Variant]
```

Square brackets mark optional segments and are not part of the name.

| Segment | Meaning |
| --- | --- |
| `Prefix` | Asset type |
| `Owner` | Feature or scope that owns the asset |
| `Context` | Asset role within its feature or scope |
| `Variant` | Difference between asset variants |

A consistent naming scheme helps narrow searches by asset type, owner, context, or variant. You can combine segments: for example, `P_Shop_` helps find shop prefabs, while `P_Shop_Item_` narrows the search to prefabs for its list or grid items.

If you need to clarify an asset's role, add `Context`. If you need to distinguish asset variants, add `Variant`.

The context can contain multiple segments separated by `_`. For example, in `P_Shop_Popup_Offer_Christmas`, `Shop` identifies the owner, `Popup_Offer` is the context, and `Christmas` is the variant.

Do not repeat information already conveyed by the prefix or context. For ScriptableObject configuration assets, do not add `Config` merely to identify them as configurations: the `SO_` prefix is sufficient for that purpose. Use `SO_Player` instead of `SO_Player_Config`. Additional context should clarify the asset's purpose, as in `SO_Player_Movement`.

### Asset type prefixes

| Prefix | Type |
| --- | --- |
| `P_` | Prefab |
| `SO_` | ScriptableObject asset |
| `M_` | Material |
| `PM_` | Physics material (3D or 2D) |
| `T_` | Texture or sprite |
| `SCN_` | Scene |
| `SFX_` | Sound effect |
| `BGM_` | Music |
| `VFX_` | Visual effect |
| `ANIM_` | Animation clip |
| `AC_` | Animator Controller or Animator Override Controller |

### UI assets

For UI assets, follow the general naming rules for their asset types.

For basic UI prefabs that do not belong to a specific feature, use `UI` as `Owner`: `P_UI_Control_ButtonPrimary`, `P_UI_Popup_Base`.

For UI prefabs belonging to a specific feature, use that feature's name as `Owner`: `P_Shop_Popup_Offer`, `P_Economy_Widget_Wallet`.

After `Owner`, use the prefab's role as the first segment of `Context`:

| Role | Meaning | Example |
| --- | --- | --- |
| `Screen` | Full-screen UI state | `P_Shop_Screen_Main` |
| `Popup` | Modal or semi-modal window | `P_Shop_Popup_ConfirmPurchase` |
| `Panel` | Large part of a screen or popup | `P_Shop_Panel_ProductDetails` |
| `Widget` | Small UI block that displays data or provides related controls | `P_Character_Widget_Stats` |
| `Item` | UI element that represents one entry in a list or grid | `P_Shop_Item_Product` |
| `Control` | Basic interactive component | `P_UI_Control_ButtonPrimary` |

### Models

For FBX and other model files, do not use an asset type prefix. Include the owning feature or scope and the model's role in the name: `Shop_Counter.fbx`, `Character_Backpack.fbx`.

For a prefab containing a model, use the `P_` prefix. If you need to distinguish it from other prefabs, add `Model` to the context: `P_Shop_Counter_Model`.

### GameObjects in a prefab

Give the root GameObject the same name as the prefab asset. Name child GameObjects by their role within the prefab. Do not repeat the feature or scope name:

```text
P_Shop_Popup_Offer
  Background
  Content
  TXT_Title
  IMG_Icon
  BTN_Close
```

For UI objects, you can use short role prefixes such as `BTN_`, `TXT_`, and `IMG_`. For gameplay objects, names such as `Visual`, `Collider`, `SpawnPoint`, and `InteractionArea` are usually enough. If an abbreviation is unclear, spell out the name.

## Folder structure

Keep project-owned assets in `Assets/_Project`. This folder separates them from third-party assets, plugins, and imported packages.

Use `PascalCase` without spaces for folder names. For special folders, use the names specified in this convention: `_Project` and `_Shared`.

Example folder structure:

```text
Assets/_Project/
  Features/
  Scenes/
  Scripts/
```

| Folder | Purpose |
| --- | --- |
| `Features/` | Contains feature folders and their categories |
| `Scenes/` | Contains project-wide scenes that do not belong to a specific feature |
| `Scripts/` | Contains centrally organized project code when code is not split into assemblies by feature |

Place feature folders in `Features/`. Keep each feature's assets in its folder. You can group related features into categories. For example, in `Features/Characters/Enemies/Zombie/`, `Characters/` and `Enemies/` are categories, while `Zombie/` contains the feature's assets. A category is unnecessary for a single feature.

If a scene belongs to a specific feature, keep it in that feature's `Scenes/` folder. If code is split into assemblies by feature, keep each feature's code in its own `Scripts/` folder.

For small projects, you can use a *type-based* structure instead of a *feature-based* structure. In that case, keep assets in `Prefabs/`, `Materials/`, `Textures/`, and other folders for their types under `Assets/_Project/`.

### Feature folders

Within a feature, group assets by type (*type-based*). Example folder structure:

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
    Scenes/
    Scripts/
```

Simplify the hierarchy when nested folders do not help separate assets. You can keep one or two assets in the nearest parent folder: for example, textures directly in `Art/`, or in the feature folder if there are no other asset groups. If `Art/` contains only one asset type, you can name it after that type, such as `Textures/`, without an additional nesting level.

Add `Scenes/` and `Scripts/` folders under the conditions described in the introduction to [Folder structure](#folder-structure).

If a feature has both gameplay and UI prefabs, keep UI prefabs in `Prefabs/UI/`. Preserve this separation when simplifying the hierarchy. If all of the feature's prefabs are UI prefabs, keep them directly in `Prefabs/`.

### Shared assets

Use by multiple features does not necessarily make an asset shared. If an asset belongs to a specific feature, keep it in that feature's folder.

If multiple features use an asset and none of them owns it, keep the asset in `_Shared/` under their nearest common category. If there is no common category, use `Features/_Shared/`.

| Ownership and usage | Location |
| --- | --- |
| An asset belongs to a specific feature | That feature's folder |
| Features with a common category use an asset without a specific owner | `_Shared/` under the nearest common category |
| Features without a common category use an asset without a specific owner | `Features/_Shared/` |

If weapon models do not belong to a separate weapon feature but are used by both `Zombie` and `Skeleton`, place them in `_Shared/` under their common category, `Enemies/`:

```text
Assets/_Project/Features/Characters/Enemies/
  Zombie/
  Skeleton/
  _Shared/
    Models/
```

Within `_Shared/`, group assets by type and simplify nesting as described in [Feature folders](#feature-folders).

In a shared asset's name, use the common scope as `Owner`. For example, a material used by several enemy types might be named `M_Enemies_Dissolve`. For basic UI prefabs, use `Owner = UI` as described in [UI assets](#ui-assets).

# Unity asset migration

This convention defines the workflow for renaming and moving Unity assets. Use the [project file organization convention](unity-project-organization.md) to determine asset ownership, names, and target paths.

## Contents

- [Boundaries](#boundaries)
- [Migration workflow](#migration-workflow)
  - [1. Get approval for the feature or category](#1-get-approval-for-the-feature-or-category)
  - [2. Build the migration map](#2-build-the-migration-map)
  - [3. Rename assets according to the map](#3-rename-assets-according-to-the-map)
  - [4. Move and validate assets](#4-move-and-validate-assets)
  - [5. Delete the map](#5-delete-the-map)

## Boundaries

- Do not edit, rename, or move scripts, assembly definitions, or their folders. Read code to check dependencies.
- Preserve the user's existing changes, behavior, serialized values, save IDs, references, and instance overrides. The only exception is synchronizing instance names in step 3.
- Do not commit or check in changes. The user does this after reviewing them.

## Migration workflow

### 1. Get approval for the feature or category

Determine asset owners and target locations using the [project file organization convention](unity-project-organization.md). Check dependencies to distinguish assets owned by the selected feature from shared assets and assets owned by other features.

Present the selected feature or category, variants, and proposed migration scope to the user. Get approval before making changes. Each migration can cover a subset of variants.

### 2. Build the migration map

Inspect pending changes. Create a temporary map outside the project with these entries:

```text
Current path → New name → Target path
```

Determine new names and target paths using the [project file organization convention](unity-project-organization.md). Resolve name and path conflicts before applying the map.

Check code and assets for dependencies on names and paths. Include string-based loading, Editor tools, and animation bindings. If migrating an asset requires a script change, leave the asset in place and explain why to the user.

### 3. Rename assets according to the map

Apply the new names. After renaming a prefab, update its root GameObject name according to [GameObjects in a prefab](unity-project-organization.md#gameobjects-in-a-prefab). Preserve GUIDs, importer settings, and prefab inheritance.

For each renamed prefab, find its instances in project scenes. Give their root GameObjects the new prefab name and save the affected scenes. For example, if scene instances of `P_Animal_Source_Cat` are named `P_AnimalSource_Cat`, rename them to `P_Animal_Source_Cat`. Preserve all other instance overrides.

### 4. Move and validate assets

Use Unity asset operations to move assets. If you move files outside the Editor, move their existing `.meta` files with them. Update references outside code as needed. Delete old folders only when they are empty.

Compare the result with the agreed map and verify that names and locations follow the [project file organization convention](unity-project-organization.md). Check GUIDs and references, and confirm that there are no unrelated changes. Wait for importing to finish, then check the Console. If the migration affects feature loading or behavior, validate the relevant scenario in Play Mode.

### 5. Delete the map

After validation, delete the temporary map and finish the task. Do not create separate reports or permanent migration maps. Do not perform extra actions solely for reporting.

In the work summary, mention only blockers, skipped assets, or required checks that were not completed, if any.

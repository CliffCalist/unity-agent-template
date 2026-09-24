# Unity C# Conventions

This convention defines C# script structure, member names, and dependency direction in Unity projects.

## 1. Script folders

Separate scripts into `Core`, `UI`, and `Bootstrap` as described in [Unity Project Organization](unity-project-organization.md#scripts). Separate assemblies are optional.

## 2. Naming

| Element | Format | Example |
| --- | --- | --- |
| Types, methods, properties, events, public fields | `PascalCase` | `PlayerMovement`, `TakeDamage`, `CurrentHealth`, `DamageTaken`, `MaxHealth` |
| Private fields | `_camelCase` | `_currentHealth` |
| Local variables and parameters | `camelCase` | `damageAmount` |

A `bool` field or property name should read like an answer to a question. Common prefixes are `is`, `has`, and `can`: `_isGrounded`, `HasTarget`, `CanAttack`.

An event names what happened, without an `On` prefix and usually in the past tense: `DamageTaken`. `Pre` and `Post` mark invocation order relative to the action: `PreDamageTaken`, `PostDamageTaken`.

An event handler method starts with `On`: `OnDamageTaken`.

## 3. Script and type structure

### Types per file

Prefer one type per `.cs` file, with matching names: `PlayerMovement.cs` contains `PlayerMovement`.

A type used only by the main type may be nested and `private`. Put a type used by other systems in its own file.

### Member order

Members appear **only in this order**:

1. Serialized and public fields, excluding constants.
2. Nonserialized private fields.
3. Constants (`const`), regardless of accessibility.
4. Events.
5. Properties.
6. Constructor or initialization methods.
7. Unity lifecycle methods, if the type is a Unity component.
8. Other methods.
9. Nested types.

Omit groups that are absent. Leave **three blank lines** between adjacent groups.

### Semantic subgroups

Keep related members together. For example, `Player` fields for movement, attack, and inventory form separate subgroups.

- Leave **two blank lines** between subgroups of fields, constants, events, or properties.
- Leave **three blank lines** between subgroups of methods.

### Unity lifecycle

Keep Unity lifecycle methods (`Awake`, `Start`, `OnEnable`, `Update`, `FixedUpdate`, `OnDisable`, and others) together after the constructor or initialization methods. They may be wrapped in `#region Lifecycle`.

In a class that is no longer small, lifecycle methods can show the order of actions by calling clearly named methods:

```csharp
private void Update()
{
    UpdateMovement();
    CheckInteractions();
}
```

`UpdateMovement` and `CheckInteractions` remain in their semantic groups. Short logic may stay directly in the lifecycle method.

### Regions in larger scripts

When a script is roughly 350 lines or longer and has several semantic subgroups of 2–4 methods, those subgroups may be organized in `#region` blocks by responsibility. A region may cover one or several related subgroups, such as `#region Movement`, while preserving blank lines between them. Do not create regions for every method or solely because the script reached a line count.

## 4. Dependency architecture

A class that composes several parts into one behavior defines their relationships and call order. A component performs its own work but does not make decisions for the class that coordinates it or use that class to invoke other components.

For example, `Player` coordinates `PlayerMovement` and `PlayerAttack`. `PlayerMovement` reports a jump through a `Jumped` event; `Player` handles it in `OnJumped` and decides what happens next.

Direct calls from the coordinating class to its components are appropriate. A component can report upward through a return value or event. If it needs a specific capability from another system, provide a narrow contract. A reference to a higher-level class is acceptable as long as the component does not start controlling that class's decisions. Add abstractions only when needed.

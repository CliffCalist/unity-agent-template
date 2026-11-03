# C# code style for Unity

This convention builds on [Microsoft's C# coding conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) and refines naming and code organization in Unity projects. Its main focus is script structure: member order, semantic grouping, and visual separation of code.

If this convention specifies a different rule, follow it instead of the corresponding Microsoft recommendation. Otherwise, follow Microsoft's recommendations within the C# version and capabilities supported by the project.

The [project file organization convention](unity-project-organization.md#folder-structure) defines where to place scripts in folders.

## Contents

- [Naming](#naming)
- [Attributes](#attributes)
  - [Attribute placement](#attribute-placement)
  - [Odin Inspector](#odin-inspector)
- [Code organization](#code-organization)
  - [Types per file](#types-per-file)
  - [Member order](#member-order)
  - [Semantic grouping and regions](#semantic-grouping-and-regions)
  - [Unity lifecycle methods](#unity-lifecycle-methods)
- [Script formatting example](#script-formatting-example)

## Naming

| Element | Format | Example |
| --- | --- | --- |
| Types, methods, properties, events, public fields | `PascalCase` | `PlayerMovement`, `TakeDamage`, `CurrentHealth`, `DamageTaken`, `MaxHealth` |
| Private fields | `_camelCase` | `_currentHealth` |
| Constants (`const`) and `static readonly` fields, regardless of accessibility | `UPPER_SNAKE_CASE` | `MAX_HEALTH`, `DEFAULT_OFFSET` |
| Local variables and parameters | `camelCase` | `damageAmount` |

The `UPPER_SNAKE_CASE` rule takes precedence over the rules for public fields, private fields, and local variables.

Name `bool` fields and properties so that the name reads as an answer to a question. Use prefixes such as `is`, `has`, and `can`: `_isGrounded`, `HasTarget`, `CanAttack`.

Name an event after what happened. Do not add the `On` prefix. Usually, use the past tense, as in `DamageTaken`. If you need to indicate when an event is raised relative to an action, use `Pre` and `Post`: `PreDamageTaken`, `PostDamageTaken`. Start event handler method names with `On`: `OnDamageTaken`.

## Attributes

### Attribute placement

Place the serialization attributes `[SerializeField]` and `[SerializeReference]` on the same line as the field declaration. Place all other attributes above the field, each on a separate line.

Leave one blank line between Inspector fields within the same semantic group, regardless of the number of attributes. The attributes and field declaration form a single block: do not separate them with blank lines.

```csharp
[Min(0f)]
[SerializeField] private float _acceleration = 5f;

[Min(0f)]
[SerializeField] private float _maxSpeed = 10f;
```

At semantic group and category boundaries, use the spacing defined in [Semantic grouping and regions](#semantic-grouping-and-regions).

### Odin Inspector

If the project uses Odin Inspector, keep field attributes that define validation, value constraints, or other data rules in code. These attributes should be visible alongside the field declaration.

Do not use Odin attributes that serve only to change the Inspector's visual presentation in scripts. Configure headers, labels, units, prefixes, and grouping through Odin Visual Designer.

This restriction applies to Odin's visual attributes. It does not prohibit Unity attributes such as `[HideInInspector]`.

## Code organization

### Types per file

Prefer one type per `.cs` file. The filename should match the type name: `PlayerMovement.cs` contains `PlayerMovement`.

If only the file's main type uses a type, you can nest it with the `private` modifier. If other systems use the type, place it in its own file.

### Member order

Arrange member categories in this order:

1. Fields displayed in the Inspector.
2. Fields and auto-implemented properties not displayed in the Inspector, excluding constants and `static readonly` fields.
3. Constants (`const`) and `static readonly` fields, regardless of accessibility.
4. Properties with accessor implementations.
5. Events.
6. Methods.
   1. Constructors.
   2. Unity lifecycle methods, if the type is a Unity component.
   3. Initialization methods.
   4. Other methods.
7. Nested types.

The first category contains fields visible in the Inspector, rather than all serialized or public fields. For example, a field with `[HideInInspector]` belongs to the second category regardless of accessibility. Constants and `static readonly` fields always belong to the third category.

Place auto-implemented properties that are not displayed in the Inspector and have no custom accessor implementations alongside fields outside the Inspector. This rule also applies to properties with only `get` or with restricted access to `set`. Place properties with at least one implemented accessor in the separate property category. Placing an auto-implemented property alongside fields does not change its naming: use `PascalCase`.

Omit categories that are absent from the type.

### Semantic grouping and regions

Within each category, organize related members into semantic groups. For example, three acceleration settings fields and two braking settings fields belong to the same Inspector field category but form two semantic groups.

Separate categories and semantic groups with blank lines:

| Boundary | Number of blank lines |
| --- | --- |
| Between member categories | 3 |
| Between semantic groups within a category, except methods | 2 |
| Between semantic groups of methods | 3 |
| Between Inspector fields within the same semantic group | 1 |

Do not add these spacing values together: for example, leave two blank lines in total between semantic groups of Inspector fields. Category and group boundary rules do not determine spacing between every pair of members within a group. Inspector fields follow the separate one-blank-line rule.

Use regions named by purpose to mark the main semantic groups of methods, such as `#region Acceleration` and `#region Braking`. A region can contain one or more semantic groups. Choose regions based on the methods' purpose, rather than the file's line count.

Do not nest regions. Separate smaller semantic groups within a region with three blank lines. For example, calculating acceleration and accounting for external forces can form separate groups within `Acceleration`.

Regions do not change the order of member categories. Do not combine fields and methods into a single region solely because they serve a common purpose.

### Unity lifecycle methods

In Unity components, group lifecycle methods in `#region Lifecycle`. Place this region after constructors and before initialization methods. Lifecycle methods include `Awake`, `Start`, `OnEnable`, `Update`, `FixedUpdate`, `OnDisable`, and others.

In these methods, show the order of actions through calls to methods named by purpose. Place the logic itself in the corresponding semantic groups outside `Lifecycle`:

```csharp
#region Lifecycle

private void Update()
{
    UpdateAcceleration();
    UpdateBraking();
}

#endregion
```

Place `UpdateAcceleration` and `UpdateBraking` in the `Acceleration` and `Braking` regions, respectively.

## Script formatting example

```csharp
using System;
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    [Min(0f)]
    [SerializeField] private float _acceleration = 5f;

    [Min(0f)]
    [SerializeField] private float _maxSpeed = 10f;


    [Min(0f)]
    [SerializeField] private float _braking = 8f;

    [Min(0f)]
    [SerializeField] private float _stopThreshold = 0.01f;



    [HideInInspector]
    [SerializeField] private float _currentSpeed;
    private float _externalAcceleration;
    public bool IsAccelerating { get; set; }



    private const float MIN_SPEED = 0f;
    private static readonly Vector3 LOCAL_FORWARD = Vector3.forward;



    public float CurrentSpeed => _currentSpeed;



    public event Action Stopped;



    #region Lifecycle

    private void Awake()
    {
        Initialize();
    }

    private void Update()
    {
        UpdateAcceleration();
        UpdateBraking();
        Move();
    }

    #endregion



    private void Initialize()
    {
        _currentSpeed = MIN_SPEED;
        _externalAcceleration = 0f;
        IsAccelerating = false;
    }



    #region Acceleration

    private void UpdateAcceleration()
    {
        if (!IsAccelerating)
        {
            return;
        }

        var acceleration = CalculateAcceleration();
        _currentSpeed = Mathf.Clamp(
            _currentSpeed + acceleration * Time.deltaTime,
            MIN_SPEED,
            _maxSpeed);
    }

    private float CalculateAcceleration()
    {
        return _acceleration + _externalAcceleration;
    }



    public void SetExternalAcceleration(float acceleration)
    {
        _externalAcceleration = acceleration;
    }

    #endregion



    #region Braking

    private void UpdateBraking()
    {
        if (IsAccelerating || _currentSpeed <= MIN_SPEED)
        {
            return;
        }

        _currentSpeed = Mathf.MoveTowards(
            _currentSpeed, MIN_SPEED, _braking * Time.deltaTime);

        if (_currentSpeed <= _stopThreshold)
        {
            Stop();
        }
    }

    private void Stop()
    {
        _currentSpeed = MIN_SPEED;
        Stopped?.Invoke();
    }

    #endregion



    #region Movement

    private void Move()
    {
        transform.Translate(LOCAL_FORWARD * _currentSpeed * Time.deltaTime);
    }

    #endregion
}
```

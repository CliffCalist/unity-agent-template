# Unity user documentation

This convention defines how to write documentation for people who use Unity and the Inspector but do not read code. Help readers understand settings, make configuration decisions, and complete tasks.

## Contents

- [Writing guides](#writing-guides)
- [Scope and navigation](#scope-and-navigation)
- [Inspector reference](#inspector-reference)
  - [Labels and coverage](#labels-and-coverage)
  - [Grouping and tables](#grouping-and-tables)
  - [Effects and value sources](#effects-and-value-sources)
- [Explanations and illustrations](#explanations-and-illustrations)
- [Authoring and verification](#authoring-and-verification)

## Writing guides

Use the following guides for general writing advice:

- Purpose and organization: start with [Diátaxis in five minutes](https://diataxis.fr/start-here/). Then consult the guidance for [tutorials](https://diataxis.fr/tutorials/), [how-to guides](https://diataxis.fr/how-to-guides/), [reference](https://diataxis.fr/reference/), or [explanation](https://diataxis.fr/explanation/), depending on the reader's need.
- Language and presentation: start with the [Google developer documentation style guide highlights](https://developers.google.com/style/highlights). Use the [full guide](https://developers.google.com/style) for specific questions. Apply its general guidance to the intended audience and requested language. Do not assume programming knowledge or adopt Google product-specific rules.

Do not create a separate page of each type for every system. Choose the materials needed for the agreed documentation scope.

Explicit user instructions and local project requirements take precedence over these guides. If explicitly approved examples exist for the relevant document type, use them. Existing documentation is not automatically an approved template.

## Scope and navigation

If an asset contains settings for several systems, its guide does not need to explain all of those systems.

Explain each topic in detail in one primary location. Elsewhere, provide only the context needed for the current task and link to the relevant section.

Use Markdown with relative file and image links. Follow the project's documentation location and naming rules. Place a linked table of contents near the beginning and update it when headings change.

## Inspector reference

### Labels and coverage

Before describing settings, explain which object or asset to select and which component or group to open.

Keep field, group, option, and button labels exactly as displayed in Unity, including in translated guides.

Cover every user-editable setting within the documented scope, including inherited and nested settings. If another topic already provides the primary reference, link to it instead of repeating field descriptions. Mention generated, hidden, or read-only data only when it helps the reader use the system.

### Grouping and tables

Group settings to match the Inspector. Use compact tables with the following information:

- Field label.
- Actual unit or scale for numeric settings.
- Purpose and visible result or behavior change. Combine these in one column when separate columns would repeat information.

Do not invent units or add a separate units column when the settings being described do not need them.

Document each nested field in its own group's reference table. In the parent table, briefly describe the group and link to its reference. If fields have different sources for their stored values, identify those sources without moving the fields out of their group.

### Effects and value sources

Describe what happens when the reader increases or decreases a value, selects an option, or assigns a reference. Include limits and dependencies that matter when choosing settings. Distinguish examples from defaults and current asset values.

If a setting is stored in another component or asset, identify where to edit it and which objects the change affects. For example, distinguish instance settings from settings in a shared configuration asset.

State any required apply, rebuild, or restart actions. Explain relevant Play Mode behavior, including whether changes persist after leaving Play Mode.

## Explanations and illustrations

Use concrete examples or diagrams to explain spatial settings. In comparisons, state the viewpoint and which quantities remain fixed. Before creating a new illustration, check whether an existing one can be reused.

Include implementation details only when they affect configuration decisions.

## Authoring and verification

Before writing, check behavior against current code, Inspector presentation, and relevant assets. Keep investigation notes separate from the user guide.

If you cannot confirm a label, unit, or behavior, do not present an assumption as fact. Report the uncertainty in the work summary.

Verify field coverage within the agreed scope, units, links, and illustrations. When possible, preview the rendered Markdown. Report verification limits in the work summary. Source inspection alone does not establish visual quality or gameplay feel; these require observation in Unity.

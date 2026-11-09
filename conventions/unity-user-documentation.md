# Unity user documentation

## Purpose and audience

This convention defines how to write documentation for clients, game designers, and other users who work through the Unity Editor and Inspector and do not read code. Documentation should help readers complete tasks, understand system behavior, and choose settings.

## Contents

- [Purpose and audience](#purpose-and-audience)
- [Documentation types](#documentation-types)
  - [Manual](#manual)
  - [System reference](#system-reference)
- [Organizing materials](#organizing-materials)
  - [Topic scope](#topic-scope)
  - [Getting started](#getting-started)
  - [Primary location](#primary-location)
  - [Navigation](#navigation)
- [Writing and formatting](#writing-and-formatting)
- [Describing the system and Inspector](#describing-the-system-and-inspector)
  - [Operating principles](#operating-principles)
  - [Access and labels](#access-and-labels)
  - [Grouping and coverage](#grouping-and-coverage)
  - [Fields and values](#fields-and-values)
  - [Buttons and other elements](#buttons-and-other-elements)
  - [Storing and applying changes](#storing-and-applying-changes)
  - [Tables](#tables)
- [Examples and illustrations](#examples-and-illustrations)
- [Verifying documentation](#verifying-documentation)

## Documentation types

Use two documentation types: manuals and system references. Choose materials based on reader needs and the agreed documentation scope. Not every system needs both types.

### Manual

A manual helps readers achieve a specific result through a sequence of actions. It can introduce a system or address a work task.

Start by identifying the task, required knowledge, and initial conditions. Then describe the steps and explain how to verify the result.

For an introduction, provide a prepared path that requires minimal prior knowledge and leads to a predictable result. For a work task, build on the stated prerequisites and describe the actions needed for that task. Briefly explain the reason for an action when it helps the reader perform it.

### System reference

A system reference helps readers understand how a system works and find information about its settings and available actions.

Organize the material so readers can both work through the topic to understand it and quickly find a specific element.

Explain the effects of settings and the conditions for using them. Descriptions should help readers make decisions rather than merely repeat Inspector labels or tooltips.

## Organizing materials

### Topic scope

Define which system or task the document covers. If an asset contains settings for several systems, the document does not need to describe all of them.

Write manuals and system references as separate documents. If both types are needed, link them to each other. Each type can include several documents for individual topics or tasks.

### Getting started

If several manuals require the same preparation, create a shared getting-started manual. Describe the location and purpose of the required assets and the basic actions needed to prepare for working with the system.

In other manuals, list this material as a prerequisite and link to it instead of repeating the preparation steps.

### Primary location

Describe each topic in detail in one primary location. Place the full description of a setting in the system reference and the sequence for completing a task in a manual.

Elsewhere, provide the context needed for the current task and link to the primary description. Manuals can include brief explanations, and system references can include usage examples.

### Navigation

Document and section titles should identify their topic or task. Add a linked table of contents near the beginning of long documents and update it when headings change.

Use Markdown with relative file and image links. Follow the project's documentation location and naming rules.

## Writing and formatting

For language, tone, and formatting, use the [Google developer documentation style guide](https://developers.google.com/style). Start with the [highlights](https://developers.google.com/style/highlights) and consult the full guide for specific questions.

Apply the general guidance to the audience and language of the document. Do not adopt Google product-specific rules.

Explicit user instructions and local project requirements take precedence over the guide. If explicitly approved examples exist for the relevant document type, use them. Existing documentation is not automatically an approved template.

## Describing the system and Inspector

### Operating principles

If choosing settings requires an understanding of a shared operating principle, explain it before describing the relevant system or group. Readers should not have to reconstruct this explanation from individual field descriptions.

Include implementation details only when they help readers use the system or choose settings.

### Access and labels

Explain which object or asset to select and which component or section to open. If these actions are already described in material listed as a prerequisite, link to it.

Keep field, group, option, button, and other element labels exactly as displayed in Unity, including in translated documents.

### Grouping and coverage

Group descriptions to match Inspector groups and nesting, regardless of where values are stored. Cover every editable setting and user action within the stated topic scope, including inherited and nested elements and those added by a custom Inspector. If the primary description is already in another document, link to it.

Describe generated, hidden, or read-only data when it helps readers use the system.

### Fields and values

Explain each field's purpose and the effect of changing it. Depending on the field type, describe what happens when the reader increases or decreases a value, selects an option, or assigns a reference.

For numeric settings, state the units or explain the scale when needed to understand the value. Include limits and dependencies that matter when choosing settings. Distinguish examples from defaults and current asset values.

### Buttons and other elements

For each button, explain the action it performs and the result the reader will get. State required prerequisites, availability conditions, and significant consequences, such as replacing previously created data.

For lists and other composite elements, describe the available operations and the significance of element order if it affects behavior. For indicators and information panels, explain how to interpret the displayed state and whether the reader needs to act.

### Storing and applying changes

Identify where to edit values and which objects a change affects. In particular, distinguish instance settings from settings in a shared configuration asset. If a value is stored in another component or asset, identify it.

State any required apply, rebuild, or restart actions. Explain relevant Play Mode behavior, including whether changes persist after leaving Play Mode.

### Tables

Use compact tables for elements of the same kind. Group them to match the Inspector. Describe nested groups in separate tables when needed, and link to them from the parent group.

Use columns for the element label and description. Include units, limits, and other information in the description or in separate columns when this makes comparison easier. Do not create columns that duplicate information or are unnecessary for the elements being described.

## Examples and illustrations

Add examples, screenshots, or diagrams when they help explain an action, relationship, or result. Use concrete examples or diagrams for spatial settings. In spatial comparisons, state the viewpoint. When comparing the effects of a setting, explain what changes and which conditions remain fixed.

Before creating a new illustration, check whether an existing one can be reused. Make sure images and captions match the behavior being described.

## Verifying documentation

Before writing, check behavior against current code, Inspector presentation, and relevant assets. Keep investigation notes separate from user documentation.

Check the prerequisites, steps, and expected results of manuals. In system references, check coverage within the stated scope, element labels, units, and behavior. For all documents, check links and illustrations and, when possible, preview the rendered Markdown.

If you cannot confirm a label, unit, or behavior, do not present an assumption as fact. Report uncertainty and verification limits in the work summary. Source inspection alone does not establish visual quality or gameplay feel; these require observation in Unity.

# Unity user documentation

## Purpose and audience

Write for clients, game designers, and other Unity Editor users who do not read code. Help them understand behavior, choose settings, and complete tasks. Use code to establish facts, then explain responsibilities and observable results in familiar language.

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
- [Selecting information](#selecting-information)
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

Use manuals and system references according to reader needs and the agreed scope. Not every system needs both.

### Manual

A manual helps readers achieve a specific result. State the task, prerequisites, and initial conditions, then describe the steps and how to verify the result. Explain reasons where they help readers act or choose between alternatives.

### System reference

A system reference explains how a system works and what its settings and actions do. Introduce the necessary concepts and make individual elements easy to find. Support both a first reading and looking up one field.

## Organizing materials

### Topic scope

Define the system or task the document covers. Keep explanations within that scope: sharing a GameObject, prefab, or Inspector does not by itself make separate components one documentation topic.

Use heading levels to distinguish the system, its subsystems, and explanations within a subsystem. Keep subsystems with comparable responsibilities at the same level. Group related subsystems so their relationship is apparent.

Keep manuals and references in separate documents and link related materials. Split them by topic or task when useful.

### Getting started

Put preparation shared by several manuals in a getting-started manual: required assets, their purpose, and setup actions. Link to it as a prerequisite instead of repeating the steps.

### Primary location

Describe each topic in detail in one primary location. Explain a setting in the reference for the system whose behavior it controls. Describe the workflow for supplying, copying, or applying its value where that workflow belongs. These may be different documents.

Do not replace a system's field descriptions with links solely because another asset supplies the values. Where several components expose the same setting, choose one primary description and provide enough context with links elsewhere.

Explain shared principles once and field-specific behavior alongside the field. Elsewhere, provide brief context and links. Manuals may include explanations, and references may include usage examples.

### Navigation

Document and section titles should identify their topic or task. Add a linked table of contents near the beginning of long documents and update it when headings change.

Use Markdown with relative file and image links. Follow the project's documentation location and naming rules.

## Writing and formatting

Use the [Google developer documentation style guide](https://developers.google.com/style), starting with its [highlights](https://developers.google.com/style/highlights). Adapt general guidance to the audience and language; omit Google product-specific rules.

Explicit user instructions and local project requirements take precedence over the guide. If explicitly approved examples exist for the relevant document type, use them. Existing documentation is not automatically an approved template.

Say what the system does and what the reader will observe. Split sentences with several conditions, effects, or exceptions. Use lists to make separate responsibilities or conditions apparent.

Introduce terms before relying on them. Avoid explaining unfamiliar concepts through other unfamiliar terms or field names.

## Selecting information

Include information that helps readers understand behavior, choose a value, act, or diagnose a relevant problem. Remove repetition and irrelevant detail while preserving the causal links needed for understanding.

Include implementation details only when they affect expectations or decisions. Translate calculations into behavior: for example, describe the range over which an effect activates rather than an internal eligibility coefficient.

State limitations and exceptions where omitting them would create a misleading expectation or a likely mistake. Avoid accumulating statements about everything a setting does not affect.

Assume the Unity basics stated in the prerequisites. Explain them at the point of need for introductory tasks, without repeating them throughout references.

Simplify while preserving conditions and scope. A target, estimate, or partial effect must not become a guarantee. Prefer a concise qualification to a long account of the algorithm.

## Describing the system and Inspector

### Operating principles

Start with the system's responsibility. For a subsystem, briefly explain what it contributes and how it relates to other systems when that relationship matters.

Explain shared principles before the fields that depend on them. Use a diagram where it clarifies the relationship. Readers should not have to reconstruct a principle from table rows or understand controls not yet introduced.

Adapt this order to the topic; a simple feature may need only a short explanation and its settings.

### Access and labels

Identify the object or asset and component the reader needs. Keep access instructions brief; link to shared preparation instead of repeating it.

Keep field, group, option, button, and other element labels exactly as displayed in Unity, including in translated documents.

### Grouping and coverage

Within the agreed scope, cover editable settings and available actions, including inherited and nested elements and custom Inspector controls. Follow recognizable Inspector groups and labels, while placing conceptual explanations where readers need them.

Describe read-only indicators when they help readers interpret the system, and identify them as read-only. Include hidden or generated data only when readers need it for the documented task or decision.

### Fields and values

Begin with what the field controls. Explain the behavior that helps the reader choose its value, option, or reference.

Explain increases or decreases when they add information beyond the definition. Avoid filler such as saying a higher minimum requires a higher value. State useful consequences for behavior.

State units or scale and relevant limits. Explain behavior below, across, and beyond thresholds or transition ranges. Include dependencies that affect choices or results. For curves, identify both axes and the effect of changing the output.

Use numeric examples when they clarify a relationship. Distinguish them from defaults and current asset values.

### Buttons and other elements

For a button, explain the action and result, its required inputs, and any availability conditions or significant consequences, such as replacing existing data.

For lists, describe operations and any effect of element order. For indicators, explain the state and whether action is needed.

### Storing and applying changes

Explain storage and application when readers need that information to make a change take effect or understand its scope. Distinguish instance settings from shared assets where this affects other objects.

State required apply, rebuild, or restart actions at the point of need. Explain copying or overwriting behavior in the relevant workflow and link to it when necessary. Avoid repeating the same persistence or application instructions across field descriptions.

### Tables

Use tables when related fields or states benefit from scanning and comparison. A button with one parameter may be clearer in paragraphs. Inspector elements do not automatically require a table.

Usually use an element label and description. Add columns only when they help comparison. Group rows by the relevant Inspector groups; split a table when distinct groups or long explanations make it difficult to use.

## Examples and illustrations

Use examples, screenshots, or diagrams when they explain a relationship more clearly than text alone, especially for spatial settings. Place them alongside the relevant explanation and identify the viewpoint, labels, or colors needed to read them.

Let text and illustrations complement each other without repeating the explanation in captions. Mark illustrative values or proportions if they could be mistaken for measurements. In comparisons, identify what changes and what stays fixed.

Before creating a new illustration, check whether an existing one can be reused. Make sure images and captions match the behavior being described.

## Verifying documentation

Before writing, check behavior against current code, Inspector presentation, and relevant assets. Keep investigation notes separate from user documentation.

Review factual accuracy and reader understanding separately:

- **Accuracy:** verify behavior, labels, units, limits, and dependencies. Check reference coverage or manual prerequisites, steps, and expected results. Ensure simplifications preserve conditions and scope.
- **Understanding:** read in order with the audience's prerequisites. Check clear responsibilities, terms before use, practical field descriptions, and a reason for each detail. Remove repetition, obvious filler, unnecessary cross-references, and sentences that require rereading.

Check links and illustrations and, when possible, preview the rendered Markdown. A correct list of fields or a successful link check does not establish that the explanation is understandable.

If you cannot confirm a label, unit, or behavior, do not present an assumption as fact. Report uncertainty and verification limits in the work summary. Source inspection alone does not establish visual quality or gameplay feel; these require observation in Unity.

---
name: canvas-apps-generate-app
version: 1.0.0
description: Generate a complete, visually distinctive Power Apps canvas app with YAML. USE WHEN the user wants to create, build, or generate a Canvas App or pa.yaml files.
author: Microsoft Corporation
user-invocable: true
---

# Generate a Canvas App

Create a complete Power Apps canvas app for the following requirements:

$ARGUMENTS

## CRITICAL: Review Guidance First

Before designing anything, you MUST read and internalize both reference documents:

- `${CLAUDE_PLUGIN_ROOT}/references/TechnicalGuide.md` — Technical best practices, control selection, validation workflow, formulas, layout strategies
- `${CLAUDE_PLUGIN_ROOT}/references/DesignGuide.md` — Design principles, aesthetic guidelines, anti-patterns to avoid, visual composition

Read both files before planning any layout or choosing any control types.

## Generation Workflow

1. **Discover** — Call `list_controls`, `list_apis`, and `list_data_sources` to understand what is available before making any design decisions. Controls you don't know exist can't influence your design.
2. **Plan** — Using what you learned from discovery, think through the full app: how many screens it needs and what major phases of work are required. Call `TaskCreate` once per task to capture every screen and phase (e.g., "Design screen layout and aesthetic", "Implement Home screen", "Implement Detail screen", "Validate and fix compilation errors"). Do not begin implementation until all tasks are created.
3. **Design** — Choose an aesthetic direction and layout strategy. Identify the primary screens, visual hierarchy, and control types. Use `describe_control` to verify property names and variants for any control you plan to use. Call `TaskUpdate` to mark the Design task complete when done.
4. **Implement** — Write the `.pa.yaml` files following conventions from `${CLAUDE_PLUGIN_ROOT}/references/TechnicalGuide.md`. Include state initialization in `OnVisible`, event handlers with guard clauses, and Power Fx formulas with the `=` prefix. Call `TaskUpdate` to mark each screen's task complete as each screen is finished.
5. **Validate** — Call `compile_canvas` after implementing each screen. Fix any errors before moving on — do not defer validation to the end.
6. **Iterate** — Repeat validate → fix until all screens compile clean. Call `TaskUpdate` to mark the validation task complete when all screens pass.

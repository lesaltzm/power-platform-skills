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

- `references/TechnicalGuide.md` — Technical best practices, control selection, validation workflow, formulas, layout strategies
- `references/DesignGuide.md` — Design principles, aesthetic guidelines, anti-patterns to avoid, visual composition

Read both files before planning any layout or choosing any control types.

## Generation Workflow

1. **Discover** — Call `list_controls`, `list_apis`, and `list_data_sources` to understand what is available before making any design decisions. Controls you don't know exist can't influence your design.
2. **Design** — Choose an aesthetic direction and layout strategy. Identify the primary screens, visual hierarchy, and control types. Use `describe_control` to verify property names and variants for any control you plan to use.
3. **Implement** — Write the `.pa.yaml` files following conventions from `TechnicalGuide.md`. Include state initialization in `OnVisible`, event handlers with guard clauses, and Power Fx formulas with the `=` prefix.
4. **Validate** — Call `compile_canvas` after implementing each screen. Fix any errors before moving on — do not defer validation to the end.
5. **Iterate** — Repeat validate → fix until all screens compile clean.

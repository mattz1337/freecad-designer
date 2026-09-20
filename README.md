# FreeCAD Designer

A Codex skill for creating, inspecting, modifying, and exporting CAD models through FreeCAD MCP.

Use it for new designs or changes to existing projects: parametric parts, imported geometry, sketches, surfaces, assemblies, technical drawings, and preparation for manufacturing or visualization. It adapts the workflow and checks to the request rather than treating every project as a 3D print.

## Requirements

- Codex with local skill support.
- FreeCAD and a working FreeCAD MCP connection configured in Codex.
- Tools for inspecting and editing documents; Python execution is useful for advanced workflows.

This repository contains skill instructions, not FreeCAD, a workbench, or an MCP server. Available operations depend on your installed workbenches and MCP tools. The skill checks those capabilities instead of promising unsupported operations.

## Install

Ask Codex:

```text
Use $skill-installer to install https://github.com/mattz1337/freecad-designer
```

Alternatively, copy the repository into a `freecad-designer` folder in your Codex personal skills directory. Keep `SKILL.md`, `agents/`, and `references/` together. If it does not appear after installation, restart Codex.

## Examples

```text
Use $freecad-designer to inspect my existing FreeCAD model, increase the
mounting-hole spacing to 60 mm, and check the dependent features.
```

```text
Use $freecad-designer to design an enclosure around this STEP model,
with an editable wall thickness and a dimensioned technical drawing.
```

```text
Use $freecad-designer to build a hand-cranked miniature conveyor using
PLA and TPU, with repeated components and checked motion positions.
```

```text
Use $freecad-designer to inspect this imported surface model, explain
the open boundaries, and repair the geometry where practical.
```

## Workflow

The skill clarifies important constraints, inspects existing geometry before editing, chooses suitable modeling tools, preserves useful feature history, and checks the actual result in FreeCAD. It provides the files the task needs: an updated FCStd, exports, drawings, source macros, or assembly guidance as appropriate.

It distinguishes native parametric models from script-generated shapes, direct editing from recovered feature history, and pose previews from solved mechanisms. Geometry checks do not establish physical strength, print fit, manufacturing feasibility, or real-world performance by themselves.

## Contents

- `SKILL.md`: general CAD workflow, including existing-model revisions.
- `references/freecad-workflow.md`: execution, linked parts, motion, and verification details.
- `references/manufacturing.md`: optional functional and manufacturing guidance.
- `agents/openai.yaml`: Codex skill metadata.

See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills) for discovery and configuration.


# FreeCAD Mechanical Designer

A Codex skill for designing printable mechanical parts and working assemblies using a connected FreeCAD MCP server.

The workflow covers practical design questions, hardware fits, captive nuts, print orientation, repeated components, motion checks, and verified exports. It is useful for mechanisms, clamps, enclosures, and small mechanical systems.

## Requirements

- Codex with local skill support.
- FreeCAD and a working FreeCAD MCP connection configured in Codex.
- MCP tools that can inspect and modify documents and execute FreeCAD Python for the full workflow.

This repository contains instructions, not a FreeCAD installation or MCP server. Tool capabilities vary by server; the skill discovers the available tools before using them.

## Install

Ask Codex:

```text
Use $skill-installer to install https://github.com/mattz1337/freecad-mechanical-designer
```

Alternatively, copy this repository into a `freecad-mechanical-designer` folder in your Codex personal skills directory. Keep `SKILL.md`, `agents/`, and `references/` together. If the skill does not appear after installation, restart Codex.

## Use

```text
Use $freecad-mechanical-designer to create a miniature conveyor with a
hand crank. Use PLA for the rigid parts and TPU for the belt. Ask for
missing constraints, then build and verify it through FreeCAD MCP.
```

Other examples:

- Design a screw-fastened enclosure around a supplied display STEP model.
- Revise a shelf clamp so its captive nut is retained against the screw force.
- Create a hand-cranked lift with repeated linked components and a motion preview.

For fitted Gridfinity organizers, use a dedicated Gridfinity skill when available.

## Expected results

Depending on the request, Codex creates an FCStd project, printable STL parts, STEP interchange geometry, source macros, and assembly instructions with a hardware list. It checks solid validity, relevant interference, sampled motion positions, and exported meshes, and inspects an actual model view.

The skill distinguishes live parametric features from script-generated geometry, and pose previews from solved mechanical assemblies. CAD checks do not establish physical strength, print fit, or real-world operation; those need suitable prototype testing.

## Repository contents

- `SKILL.md`: design and delivery workflow.
- `references/freecad-workflow.md`: FreeCAD execution, linked parts, motion, and export guidance.
- `agents/openai.yaml`: skill name and invocation metadata for Codex.

See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills) for skill discovery and configuration.

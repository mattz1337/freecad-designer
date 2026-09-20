---
name: freecad-mechanical-designer
description: Design and revise printable mechanical parts and working assemblies through FreeCAD MCP, including enclosures, clamps, mechanisms, hardware fits, motion checks, and print exports. Use for functional CAD projects; fitted Gridfinity organizers should use gridfinity-designer when available.
---

# FreeCAD Mechanical Designer

Turn an idea into an inspectable FreeCAD project, printable components, and practical assembly instructions. Work in the user's language. Ask only questions that materially affect the mechanism, fit, or manufacturing choices; continue independent work while answers are pending.

## Establish the design

- Identify intended function, envelope, loads, motion, mating parts, materials, printer constraints, and available hardware. Distinguish a visual model from a working prototype.
- Reuse answers from the current conversation about printer, materials, hardware, and fastening preferences. Treat project-specific choices as context, not permanent restrictions for unrelated designs.
- Measure supplied CAD or use official dimensioned drawings for purchased components. Do not derive precision mounting holes or connector clearances from a product title or perspective photo. If dimensions are missing, identify what remains provisional and make useful progress without claiming a fitted result.
- State important assumptions and the selected mechanism briefly. Do not add a mandatory approval gate when creation is already authorized.

## Engineer for assembly and printing

- Follow the load path through fasteners, bearings, joints, and thin sections. Retain captive nuts against a solid shoulder in the direction of screw force; an open pocket or glue alone must not be presented as positive retention.
- Separate clearance, sliding, press, and threaded fits. Record whether an allowance is radial or diametral. Treat printed tolerances as material/process dependent; use a small fit coupon when uncertainty would waste a large print.
- Provide tool access, a feasible assembly sequence, axial retention, and space for actual screw heads, washers, nuts, and protruding threads. Check screw length against the whole stack.
- For moving mechanisms, consider friction, stiffness, layer direction, travel stops, moving envelopes, and adjustment. Use purchased shafts or bearings when loads warrant them; printable shafts are a choice for suitable light-duty prototypes, not a universal default.
- For flexible belts, distinguish the assembled envelope from the relaxed printable belt. Explain tension adjustment and the dependency on TPU properties. A static belt model does not demonstrate transport performance.
- Choose part splits and print orientations deliberately. Inspect bridges, overhangs, bed footprint, thin walls, and access for support removal. Avoid cosmetic complexity that compromises function unless requested.

## Build through FreeCAD MCP

Discover the actual available MCP tools and read their schemas. Before writing model code, read [FreeCAD execution and verification](references/freecad-workflow.md).

- Create a meaningfully named new document for a new project. For revisions, inspect the existing document and preserve unrelated objects and user work.
- Prefer native constraints, expressions, spreadsheets, and feature dependencies for dimensions the user will edit. Use App::Link for genuinely identical repeated components and App::Part for sensible grouping.
- A script-generated BREP with descriptive properties is not a live parametric model. If that approach is appropriate, deliver the generator and explain which inputs require rebuilding. Do not call a collection of placements a solved mechanical assembly.
- Save source macros alongside outputs. Avoid reliance on transient Python globals or a single machine's absolute output path. Preserve distinct prototype and assembly placements.

## Verify and deliver

- Recompute; inspect object error states, null shapes, validity, expected solids, and assembly bounding box. Check relevant pairwise interference with a stated volume tolerance and explicit treatment of intentional contact.
- For motion, check meaningful poses and end positions. Report sampled collision checks as samples, not proof of continuous clearance or physical performance. A pose macro must preserve rest placements and rotate around the correct axes.
- Inspect an actual FreeCAD image of the finished model. Verify that repeated parts are visible and hidden library geometry is not duplicating the assembly.
- Export an FCStd, and per-unique-part STLs when printing is intended. Provide STEP when useful for interchange. Normalize print exports without changing the assembled model; verify mesh closure and quantities. Do not export linked parts with transforms applied twice.
- Include a compact hardware BOM, print orientation notes, assembly sequence, important tolerances, and unresolved prototype limitations. Package a ZIP for multiple files when useful.
- Report the outcome, dimensions, meaningful object/part names, verification results, and any unresolved warnings. Record corrected modeling errors in the verification report when relevant. Keep claims about printed or real-world tests separate from CAD checks.

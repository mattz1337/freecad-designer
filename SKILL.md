---
name: freecad-designer
description: Create, inspect, modify, repair, and export CAD models using FreeCAD MCP. Use for new or existing FreeCAD projects, imported geometry, parametric sketches and solids, surfaces, assemblies, technical drawings, and CAD preparation for manufacturing or visualization.
---

# FreeCAD Designer

Help the user accomplish their CAD task through FreeCAD MCP, from a small edit to a new design. Match the deliverable to the request: an inspected model, corrected feature, drawing, assembly, visualization, or manufactured part. Do not impose printing, mechanical design, or an export bundle on every task. Work in the user's language.

## Establish the task

- Determine whether the user wants a new project, an edit to an existing model, analysis, conversion, or a drawing. Reuse known dimensions and preferences from the conversation.
- Ask only for missing information that materially affects the result. Continue independent inspection or modeling while answers are pending. Do not introduce a mandatory approval gate for work already authorized.
- Identify units, critical dimensions, intended use, reference geometry, and required outputs. Establish manufacturing, loads, materials, or printer constraints only when relevant.
- Measure supplied CAD or use authoritative dimensioned drawings for purchased parts. Do not infer precision mounting positions from a product title or perspective photo. Label provisional dimensions and assumptions.
- Discover the actual available MCP tools and read their schemas. Confirm the necessary workbench or capability before promising its result. If unsupported, explain the limitation and use a suitable available CAD approach when it preserves the user's goal.

## Inspect before modifying

- Inspect relevant documents, object names and types, feature dependencies, constraints or expressions, placements, visibility, and recompute errors. Identify the actual edit target before mutating it.
- Preserve unrelated geometry and user changes. Prefer modifying the existing driving sketch, parameter, or feature to adding a disconnected replacement. Trace dependent features after an edit.
- For imported STEP solids, distinguish direct geometric edits from native feature-history edits. For meshes, assess topology and resolution before conversion; conversion does not restore original design intent or smooth analytic surfaces automatically.
- Keep a recoverable baseline for substantial or destructive revisions, using an appropriate saved copy or transaction. Do not silently overwrite the source import or discard unsaved documents. A new project gets a new document; a revision should retain useful structure and names.

## Model appropriately

Before writing model code, read [FreeCAD execution and verification](references/freecad-workflow.md). For functional parts, mechanisms, or manufacturing preparation, also read [Manufacturing and mechanical design](references/manufacturing.md).

- Choose sketches, Part Design features, Part operations, surfaces, Draft geometry, assemblies, or drawing tools to suit the task and available workbenches. Do not force every object into a solid or every design into a single Body.
- Prefer native constraints, expressions, spreadsheets, and feature dependencies for dimensions the user expects to edit. Avoid redundant constraints, accidental external references, and fragile face/edge references when a stable datum or sketch reference is practical.
- Use meaningful object names and sensible grouping. Use App::Link for genuinely identical repeated components where appropriate. Preserve coordinate systems and placement relationships when importing or assembling geometry.
- A script-generated BREP with descriptive properties is not a live parametric model. If using a generator, deliver its source and explain which inputs require rebuilding. A set of placements or pose macro is not a solved mechanical assembly.
- For surfaces and open shells, verify the intended topology and boundaries rather than demanding a solid. For technical drawings, check projection, scale, dimensions, units, page fit, and legibility against the model.
- Keep source macros independent of transient Python globals and unnecessary absolute machine paths. Use domain-specific skills when they improve a specialized task, without treating their availability as a prerequisite for general CAD work.

## Verify in proportion to the change

- Recompute and inspect relevant error states and geometry validity. Check dimensions and placements against the request, including downstream effects of revisions. Use topology expectations appropriate to the object type.
- For assemblies, check relevant interference and intentional contact. For moving parts, inspect meaningful poses and endpoints, stating sample coverage and remaining uncertainty.
- Inspect the actual FreeCAD model from views that reveal the change. Check visible instances and hidden construction geometry. For drawings or visual deliverables, inspect the rendered output too.
- Export only the formats needed. Preserve units, intended world/local coordinates, and useful structure. Verify exported geometry or meshes as appropriate; STL is unitless, so state the intended units. Do not apply instance transforms twice.
- Save the final document when a CAD deliverable is requested. For a small edit, concise confirmation and the updated file may suffice. For a substantial project, add appropriate source files, exports, checks, and assembly or manufacturing instructions.
- Report what changed, important dimensions, verification performed, and unresolved failures or warnings. Distinguish geometric checks from physical testing, solved simulations, and manufacturability claims.


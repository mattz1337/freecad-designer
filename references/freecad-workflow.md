# FreeCAD execution and verification

## Tool execution

Use discovered tool schemas as the authority for names and arguments. With this FreeCAD MCP, synchronous execute_code runs on the GUI thread and is appropriate for normal document construction. Import FreeCAD, FreeCADGui, Part, and other modules explicitly inside standalone macro namespaces.

Use App.listDocuments().get(name) to test whether a document exists; App.getDocument(name) can raise for a missing document. Use a unique project name or inspect the existing project before replacing anything. Do not close unrelated documents or discard unsaved user work.

Background execute_code_async must not access the GUI or mutate document objects directly. Perform pure geometry work there, then use its provided commit helper for document/GUI changes. For expensive or potentially unstable OCCT operations, prefer the available isolated headless tool; save results before importing them into the GUI. Do not assume a tool or commit helper exists without checking.

A timeout does not prove an operation failed or stopped. Inspect document/file state or job status before retrying mutations. Use one bounded retry after a healthy probe when appropriate; do not repeatedly queue the same build. Preserve completed output and report a persistent connection failure.

Dense texture sketches and repeated Boolean operations can take much longer than a smooth model. Choose an execution budget or isolated build before starting, and write progress checkpoints for long generators. After a GUI timeout, use an available status probe that does not itself require GUI dispatch; a temporarily stuck status can recover when the queued operation finishes. Verify the completed artifacts before deciding to rerun. File existence alone is insufficient if a generator initially copies its baseline to the output path.

## Repeated parts and motion

Keep master shapes in a library and assembly instances as App::Link objects. Test visibility after hiding masters. Check each instance's world-space bounds before export because linked shapes may already include placement.

For a simple pose driver, store each instance's rest placement and rotation center. For rotation R about center c, use a placement with translation c - R(c), then multiply by the rest placement. Rotate all mechanically coupled components consistently. A visual pose driver is distinct from joints, contact solving, and flexible-body simulation.

## Checks and output

After recomputation, record:

- Document name, principal input dimensions, assumptions, and object names.
- isNull/isValid, expected topology (solid, shell, face, wire, or mesh), and invalid/error object states. Do not require intentional surfaces or wires to be closed solids.

- World-space overall bounds excluding hidden masters and reference geometry unless explicitly included.
- Positive common volume for candidate interference pairs, using bounding boxes first. State the numeric tolerance and intentional contacts/exclusions. Do not infer correctness from zero intersection alone: gaps, nut capture, bearing fits, and tool access require separate review.
- Motion sample angles or translations and any detected collisions. Restore the intended delivered pose afterward.
- For requested print exports: per-part STL quantity, intended units, orientation, bounds, and closed-mesh result. For other exchanges, check the relevant topology, placement, and dimensions after export or reimport.

An invalid dependent fillet can retain a cached, geometrically valid Shape. Check feature states through the dependency chain, repair changed edge references where necessary, and recompute before accepting the tip or exporting it.

For STL orientation, copy the shape, rotate the copy to the chosen print orientation, and translate its bounding-box minimum to the build plane. Leave document placements intact. Use appropriate tessellation rather than excessive mesh density. Relaxed flexible parts may need a separate export geometry; document that difference.

Save FCStd after final recompute and pose restoration. Save and inspect at least one useful rendered view. Keep exported files and the report consistent with the final geometry, and exclude stale backups from the delivery ZIP.

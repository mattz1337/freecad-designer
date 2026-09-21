# Fitted parts and exterior revisions

Read when measurements or prototype feedback drive a fitted enclosure, grip, sleeve, or similar part. The [pocketknife grip example](../examples/pocketknife-grip/README.md) documents one application; its dimensions are not general defaults.

## Establish and preserve fit

- Record what each measurement spans and its datum. A caliper reading does not identify whether the jaws touch a hole edge, center, bevel, or exterior silhouette. Keep ambiguous offsets provisional rather than giving a photograph false precision.
- Separate directly measured dimensions, estimated outlines, print allowances, and user-confirmed observations. Correct the specific failed feature after a trial print instead of rescaling the whole model and changing successful interfaces.
- When the user confirms fit, preserve that exact FCStd and print exports before cosmetic work. Record the revision, confirmation scope, and file hashes. Do not silently replace it with a later variant or transfer its physical-test status to that variant.

## Protect functional geometry

- Define protected regions before an exterior-only revision: seating surfaces, retaining lips, moving clearances, window openings, and fastener seats as applicable. Compare in the same assembly coordinate system.
- Where solid geometry permits, intersect baseline and revision with each protected volume, then compute both directional differences: volume(A minus B) + volume(B minus A). State the tolerance and why the region covers the interface. Equal overall volume or unchanged bounding boxes cannot establish an unchanged cavity.
- Check wall thickness and retention separately. Numerical equivalence of selected regions is limited to those regions; it does not establish strength, continuous motion clearance, or the fit of a newly printed part.

## Match surface texture to the intended appearance

- Treat concept images as visual targets, not dimensioned geometry. Inspect actual CAD views from comparable directions before declaring the design matched.
- For broad texture coverage, derive a mask from the outer silhouette with a deliberate border, then subtract expanded windows and fastener exclusion zones. Clip a continuous pattern to this mask rather than placing small rectangular patches by convenience.
- Distinguish pattern pitch, groove width/depth, coverage, and smooth border width. Increasing coverage should not silently change individual diamond size. Report mask area as coverage area, not as the area of material removed by grooves.
- Preserve smooth hardware bearing areas and sufficient material below grooves. Confirm the slicer resolves narrow features. If a finishing operation uses a generated BREP, state that upstream edits require rebuilding rather than presenting it as a live parametric feature.

## Package evidence accurately

Keep physical-test notes separate from CAD validity and mesh checks. Label AI concepts, CAD renders, and prototype photos distinctly. For shared examples, use redacted derivatives of private inscriptions and inspect them visually; exclude uncensored originals, prompts containing private text, and machine-specific paths from the public package.

# Design QA — Địa Cầu

## Scope and result

**final result: blocked**

The frontend prototype and its principal UI controls are implemented and browser-tested. The original requirement for actual 3D ecosystems, free camera orbit and independently animated organisms is **not implemented**: this version uses generated raster reconstructions with pan and zoom. This is an unresolved P1 scope gap, not a finished 3D experience. Do not describe this deliverable as a completed 3D website or as passing full product QA.

## Evidence

- Source visual truth: `docs/approved-design.png`, 1488 × 1056 pixels.
- Implementation: `docs/implementation-desktop.jpg`, 1302 × 924 pixels, captured in the cloud browser from a 1488 × 1056 CSS iframe with transform scale 0.875, devicePixelRatio 1.
- Source was downsampled uniformly to 1302 × 924 for comparison. No unequal-axis distortion.
- State: Cambrian, 508 million years ago, paused, default pan/zoom, no dialog.
- Full comparison: `docs/design-comparison.jpg`.
- Focused sidebar comparison: `docs/journal-comparison.jpg`.
- Mobile: `docs/implementation-mobile.jpg`, 390 × 844 CSS viewport, dpr 1, no scaling. Timeline is intentionally placed above the journal on narrow screens to keep the main interaction accessible.
- Regular desktop was also inspected at 1363 × 936.

## Findings

- [P1, unresolved] The original 3D requirement is missing. Image assets cannot supply 360-degree geometry, lighting or life-form animation. Fix: supply/produce licensed, scientifically reviewed GLB assets for each ecosystem and replace the image stage with a Three.js renderer plus OrbitControls and raycasting. Keep the existing UI and chapter state.
- [P3] Generated scene details differ from the original image; core museum appearance, subjects and composition are maintained. This is a generated visual reconstruction, not an identical source-image crop or a validated scientific reconstruction.
- [P3] Secondary epoch specimen panels reuse their scene image, rather than supplying isolated organism models. This is explicitly a prototype limitation.

## Comparison history

1. First browser capture found [P1] scene and journal overflow into the timeline. Fix: constrain the grid row with minmax(0,1fr), set the scene item min-height:0 and position the scene image within the stage. Subsequent captures show separate, non-overlapping controls.
2. [P2] Cream rectangular image backgrounds were visibly different from the surface. Main Cambrian scene and isolated specimen were regenerated with transparent exterior backgrounds. The new capture shows the illustrations integrated with the cream surface.
3. [P2] Sidebar heading size/wrapping and scene scale drift. Adjusted desktop title and image scaling; reduced long-title size for other chapters. Compared reference and implementation in the same composite input; later typography refinement included in final capture.
4. [P2] On mobile, timeline was below the long journal. Reordered narrow-screen content as scene → timeline → journal. Fresh 390 × 844 capture confirms timeline visible directly below the play controls, with no horizontal overflow.
5. Fixed a same-chapter selection bug that could hide an already-loaded image, and added explicit Home/End/arrow navigation to the whole-history range.

## Fidelity surfaces

- Typography: local Noto Serif, Vietnamese subsets. Museum editorial hierarchy, dark-green display type and copper date. Local Be Vietnam Pro for compact utility controls. Long titles adapt without overlapping controls.
- Spacing/layout: desktop two-column layout, full-width two-tier timeline, aligned play/zoom controls. Mobile stacks information with timeline prioritized.
- Colors/tokens: cream #faf6ea, forest #183c29, copper #bb4c17, sage #dbe4d8. Focus outline uses copper; disabled controls visually distinct.
- Images: generated museum dioramas, WebP optimized; key scene/specimen use alpha. No custom SVG or CSS drawings substituted for reference art. Phosphor icons supply controls. These are raster images, **not true 3D**.
- Content/copy: Vietnamese, 8 curated scenes, rounded ages, sources and reconstruction limitations. Hint changed from orbit to image panning to match actual capability.

## Browser interaction checks

- Native period selection changes date, main scene and journal.
- Play switches to Pause and progresses through multiple chapters; Pause stops progression.
- Local range End selects 485 Ma in Cambrian.
- Whole-history range End selects Present; next-chapter control disables at the endpoint.
- Zoom activates the zoom-out control; reset returns default zoom.
- Specimen dialog opens with correct content; close works.
- Journey dialog lists all 8 chapters; choosing Cambrian restores its scene.
- Brand link resets to Cambrian without hiding the existing image.
- Desktop and mobile screenshots inspected; mobile timeline accessible.
- Browser console checked: observed errors were from the browser metadata extension (`chrome-extension://.../content-script.bundle.js`), not application code. No application JS error was observed in the checked messages.

## Next implementation work

Actual GLB ecosystems and live 3D rendering remain required to satisfy the full original request. The README describes the planned integration boundary. Do not publish as a completed scientific simulation.

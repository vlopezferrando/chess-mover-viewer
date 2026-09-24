# Chess mover — KST X06 thin version

Open https://vlopezferrando.github.io/chess-mover-viewer/

Iteration 8: **Ø43 mm × 20.0 mm installed height**, 1.1 mm thinner than the preceding 21.1 mm version. KST X06 servo with mounting tabs, custom extended-hub crank, 10×2 mm N42 magnet, full 6 mm lift, 13 mm wheels and optional plastic enclosure. Target horizontal speed is 150 mm/s, unvalidated.

Use **Show / hide enclosure**, individual layer checkboxes, lift slider, orbit/zoom and bottom view. The lower shell and lid have openings for wheels, contacts, camera, magnet and coils.

Earlier versions: [Ø43 / FS0307](43mm-fs0307.html), [Ø45](45mm.html), [Ø40](40mm.html).

The KST case is 7 mm thick; the complete mover saves 1.1 mm rather than the full 1.3 mm case difference. A stepped magnet tray and shortened rear motor saddle preserve retraction clearance. The front tray floor is 0.4 mm thick, with 0.2 mm nominal motor clearance. The camera lens is now 11.9 mm above the floor. At 19.8 mm overall height the tray loses clearance and the yoke intersects a rear coil; at 19.7 mm it also overlaps a drive motor.

The KST V6 rated torque at 6 V is about 39 mN·m, compared with a cautious assumed retraction-load scenario of 12.5 mN·m. These are preliminary sizing figures, not measured hardware performance. [KST product/specification](https://kstservos.com/collections/x-series/products/x06-v6-0-hv-micro-digital-metal-gear-glider-1-8kg-torque-servo-motor). [Actuator comparison](ACTUATOR_STUDY.md).

Nominal checks passed: valid connected parts, static overlaps, Ø43 containment, height, 23 sampled lift poses, 26 gear phases and camera center path. STEP reimport gives 46 valid solids, 43×43×20 mm bounds. Viewer controls tested using DOM/WebGL stubs; static previews inspected. No real-browser rendering test.

This remains a packaging prototype. KST geometry is drawing-derived, not manufacturer STEP. The hub bore does not model a working spline: matching horn/insert, screws and retention remain to be designed. Structural strength, tolerances, real camera focus/FOV, electronics/routing, contact loading, magnetic chassis interactions, release, 150 mm/s motion, accuracy and tipping remain unqualified. Tightest listed radial shell gap remains about 0.12 mm. Not fabrication-ready.

Self-contained HTML/WebGL snapshot hosted with GitHub Pages.

# Chess mover viewer — Ø45 mm version

Open https://vlopezferrando.github.io/chess-mover-viewer/

Iteration 6: nominal 45 mm diameter including optional plastic enclosure, 21.1 mm installed height between conducting plates (previously 25.2 mm), 13 mm wheels, 10×2 mm N42 magnet and 6 mm lift. Target speed is 150 mm/s, not validated performance.

Use **Show / hide enclosure**, or the separate lower-shell and lid checkboxes. Wheel, upper/lower contact, camera, magnet and coil openings are modeled. Bottom view shows the camera opening. Drag to orbit, scroll to zoom, and use the lift slider to inspect motion.

The earlier Ø40 mm viewer is preserved at [40mm.html](40mm.html).

This is a nominal packaging concept, not fabrication-ready hardware. Smaller magnet and shorter travel contribute to the height saving; diameter alone does not explain it. The magnet choice depends on friction and needs physical validation. Provisional camera, servo shaft, contact and electronics envelopes require real-part verification. Fasteners, tolerances, structural strength, camera field of view/focus, magnetic effects of the chassis, release, speed, accuracy and tipping are not qualified.

Nominal geometry checks passed: part validity/connectedness, static overlaps, circular containment, height, 23 sampled lift poses, 26 gear phases, and camera center optical path. Viewer controls were tested with DOM/WebGL stubs; no real-browser rendering test was performed. Preview renders were inspected.

Self-contained HTML/WebGL viewer: no installation or account needed. GitHub Pages serves this static snapshot.

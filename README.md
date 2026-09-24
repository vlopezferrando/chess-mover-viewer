# Chess mover viewer — Ø43 mm candidate

Open https://vlopezferrando.github.io/chess-mover-viewer/

Iteration 7 repacks the Ø45 concept into **43 mm diameter and 21.1 mm installed height**, including optional plastic enclosure. It retains 13 mm wheels, a 10×2 mm N42 magnet, 6 mm lift and FS0307 servo. Target speed is 150 mm/s, not validated performance.

Use **Show / hide enclosure**, or separate lower-shell and lid checkboxes. Openings accommodate wheels, upper/lower contacts, camera, magnet and coils. Drag to orbit, scroll to zoom; use the lift slider and bottom view.

Earlier viewers: [Ø45 mm](45mm.html), [Ø40 mm](40mm.html).

The reduced diameter needs relocated coils, contacts, magnet and actuator, a smaller PCB and modified yoke/pin geometry. It saves 8.7% plan area versus Ø45 without reducing height. The same layout at Ø42 still intersects its enclosure. Ø42 is not ruled out after further redesign.

**Only 0.12 mm nominal radial clearance remains at a contact sleeve.** This is a compact packaging candidate, not fabrication-ready hardware. Ø45 is more forgiving for a first physical build. Actual part measurements and manufacturing tolerances are essential.

Checks passed: valid connected parts, static overlaps, circular containment, installed height, 23 sampled lift poses, 26 gear phases, and camera center optical path. STEP reimport: 46 valid solids, 43×43×21.1 mm. Viewer controls tested with DOM/WebGL stubs; preview renders visually inspected. No real-browser rendering test.

Read the [smaller lift actuator study](ACTUATOR_STUDY.md) for manufacturer sources and force-based sizing. Alternatives are research candidates and have not replaced the servo in this CAD.

Magnetic chassis effects, physical release, speed, accuracy, tipping, fasteners, structural strength, camera field of view/focus, electrical/RF design and production tolerances remain unqualified. Self-contained HTML/WebGL snapshot hosted through GitHub Pages.

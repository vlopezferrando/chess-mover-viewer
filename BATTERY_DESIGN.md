# Battery mover and charging dock — Ø43 × 25.2 mm

[Open the offline viewer](index.html). Use **Inspect battery**, **Show docking station**, the docking-distance slider, and the independent enclosure/lid layers. Downloads include [mover STEP](mover_step.zip), [dock STEP](dock.step).

This is a nominal packaging design. The battery is a documented reference cell, while charging electronics and dock contacts are space allowances, not a complete electrical or manufacturable design. Prior iterations remain unchanged.

## Dimensions and changes

| Quantity | Previous plate-powered KST | Battery version |
|---|---:|---:|
| Outside diameter | 43 mm | **43 mm** |
| Highest mover geometry above floor | 20.0 mm including contacts | **25.2 mm** |
| Floor-to-board underside | 20.0 mm | **25.4 mm** |
| PCB top | 19.0 mm | 24.4 mm |
| Servo case top | 18.8 mm | 24.2 mm |
| Magnet / coil top | 19.5 mm | 24.9 mm |
| Camera lens height | 11.9 mm | **11.9 mm** |
| Magnet and stroke | 10 × 2 mm N42 / 6 mm | unchanged |
| Wheels | 13 mm | unchanged |
| Battery | none | 100 mAh, 1S, supplier-rated 2 A maximum continuous |

The 100 mAh cell sits horizontally above the drive motors. The servo, roof PCB and lift move upward together by 5.4 mm. Removing top/bottom sliding contacts means the new mover's highest geometry is its lid, 0.2 mm below the board underside. Thus the mover-height increase is 5.2 mm, and required floor-to-board space increases by 5.4 mm. The battery is not placed over the camera or in the magnet travel path.

The cradle includes edge guards and two hangers reaching the roof. A relief in the old motor saddle clears the shelf. The downward camera stays in place with longer supports and a flex routing allowance. Four top coils, KST X06, two N20 motors, transmission and optional shell remain. The front shell gains a recessed docking-pad carrier. Continuous upper/lower conducting sheets and all four sliding contacts are removed.

### Space budget

- Battery body: x = −16…13 mm; y = −8.25…7.25 mm; z = **11.6…16.35 mm**.
- Supplier maximum thickness: **4.4 mm at delivery, 4.75 mm after cycling**. The viewer uses 4.75 mm, not an unrealistically thin new-cell-only envelope.
- Shelf: z = 11.2…11.5 mm; **0.3 mm above the nominal motor top**, and 0.1 mm below the cell. This thin shelf still needs strength and insulation design.
- Lowest servo rail: z = 16.6 mm, leaving **0.25 mm over the cycled cell envelope**. Do not clamp or load the cell with the servo.
- Straight battery tab allowances: maximum **7 mm length and 2.2 mm width**; nominal tab spacing represented. Weld insulation, tab-location tolerances and final lead bends require supplier confirmation. We do not assume folded tabs save space.
- Added electronics allowances: **9 × 6 × 1.4 mm** charger/protection/charge-tracking area and **6 × 7 × 2 mm** boost-converter/inductor area. Existing ESP32, motor-driver and memory allowances remain. These are not validated component placement/routing or thermal results.
- A local height study compares 25.2, 25.0 and 24.8 mm while preserving this shelf and moving the upper mechanism. The 25.0 mm trial leaves only 0.05 mm battery-to-rail clearance; 24.8 mm overlaps. The selected 25.2 mm uses a provisional 0.25 mm nominal gap. This is **not a full manufacturing tolerance budget or proof of a global minimum**.

See `output/space_study.json` and `output/height_comparison.csv`. The old 20 mm upper layout is also tested against the new cell envelope, exposing its collisions. A larger diameter might permit side-by-side repacking; that search is outside this local study.

## Reference battery and power constraints

Reference: **Honcell HCG431528HP20 / HCG-431528**, 100 mAh, 3.7 V nominal, approximately 2.9 g, bare cell. [Manufacturer page](https://www.honcell.com/lithium-battery/cells/hcg-lipo-battery-cells/1933) and [2024 manufacturer datasheet](https://www.honcell.com/Public/Uploads/uploadfile/files/20240809/DATASHEETHCG4315283.7V100mAhCELL2024.pdf); saved in `sources/honcell_100mah.pdf` with an inspected drawing render. Dimensions include the complete body/seal envelope, but exclude the separately modeled tabs.

The sheet specifies 2 A maximum continuous discharge at 10–45°C. Its 4 A pulse figure is only **2–3 milliseconds**; it is not permission to run stalled motors at 4 A. The final motor winding, drive-current limiting, converter losses, servo transient and coil load must fit the battery budget. At 3.0 V and 85% converter efficiency, 2 A would provide only 5.1 W; practical limits need margin for voltage sag and temperature. The reference cell is not yet purchased or electrically tested.

Use a regulated servo supply: a 1S cell cannot provide a steady 6 V. Reserve cell protection, temperature sensing, charger power-path management and reverse-current blocking. CAD does not implement these circuits. No battery connector is claimed to fit; supplier-welded tabs/leads are represented, with service access requiring detail design.

A 150 mAh cell is not automatically interchangeable. The sourced [Blade BLH4210 150 mAh high-discharge battery](https://www.horizonhobby.com/product/150mah-1s-3.7v-45c-lipo-battery-ph-1.25-ultra-micro/BLH4210.html) is 42 × 12 × 5 mm: its 43.68 mm footprint diagonal exceeds the 41.4 mm shell bore. This build therefore implements the documented **100 mAh** reference. A shorter 150 mAh alternative would require its own drawing and clearance checks.

## Docking contacts and operation

Two **3 × 3 mm mover pads**, on 7 mm centre spacing, face forward (−Y). Their exposed plane is y = −20.5 mm, with z centre 9.5 mm. They are recessed within the 43 mm circular envelope and connect to the **charger input**, not directly across the bare battery. Polarity in the model: x = −3.5 is GND; x = +3.5 is +5 V. PCB-mounted or flex-mounted plated pads on an insulating carrier are intended; finish, termination and fastening are provisional.

The external dock has two axial spring-contact envelopes and approach rails. Spring barrels are on the station, saving mover volume. Modeled compressed tips touch the pad planes. The concept allocates approximately 1 mm working compression, but no purchased contact, spring rate, retention force or free-tip CAD has been selected. The 1.2 mm tips have a geometric ±0.9 mm pad-centering allowance before an entire tip leaves a 3 mm square; this is not demonstrated docking accuracy. The nominal dock footprint is 50 × 31 mm, outside the mover boundary.

The viewer's docking slider moves the mover 0–45 mm along +Y away from the seated pose. This is ideal kinematic inspection, not automatic navigation. `check_dock.py` tests sampled straight approaches against the fixed, compressed dock geometry and verifies pad/tip surface alignment. It does not simulate contact compression, yaw error, bounce or electrical connection. **A passive detent or other holding arrangement is still needed** if spring force can push the mover away; holding stalled drive motors while charging is not assumed acceptable. The shell and dock remain concept geometry, not ready-to-print fixtures.

Intended charging sequence: lower magnet, approach a perimeter marker, align slowly, establish contact, confirm input voltage/charge status, disable drives and sleep unnecessary loads, then undock with an energy reserve. Tentative standard charge current is **100 mA (1C)**; full CC/CV charging is not instantaneous. Temperature limits and supplier initial-charge instructions apply. The 200 mA maximum rating is not the default charging setting. Each mover requires its own charge controller. Low-battery detection should combine voltage under known load with charge tracking; voltage alone during acceleration is not a precise state-of-charge estimate.

## Magnet, coils and remaining limitations

Without the former 0.1 mm copper layer, nominal magnet-to-steel distance is **3.5 mm engaged and 9.5 mm retracted** (0.5 mm clearance + 3 mm nonmagnetic board + lift). Existing magnetic force/release calculations used 3.6/9.6 mm; they have **not** been rerun or requalified here. Battery pouch metal, motor steel, servo gears and PCB copper remain omitted from that FEM. Coil resonance, battery heating and RF behaviour need measurement in the new stack.

The previously targeted **150 mm/s** is retained but not demonstrated. Battery current limits could affect acceleration and available torque. Full tolerance stack, heat flow, pouch protection, wire bends, fasteners, snap features, servo-horn retention, optical field of view and close focus remain unresolved. Carry forward the KST crank/spline and thin carrier limitations in [iteration 8](https://github.com/vlopezferrando/chess-mover-viewer/blob/main/ACTUATOR_STUDY.md).

## Reproduce and validation

From the repository root:

```sh
cad_01_mover/.venv/bin/python -m cad_09_battery.src.build
cad_01_mover/.venv/bin/python -m cad_09_battery.src.validate
cad_01_mover/.venv/bin/python -m cad_09_battery.src.space_study
cad_01_mover/.venv/bin/python -m cad_09_battery.src.check_dock
cad_01_mover/.venv/bin/python -m cad_09_battery.src.check_step
node cad_09_battery/src/check_viewer.cjs
```

Uses the pinned CAD dependencies in `requirements.txt`, the original motor asset and earlier gear/mesh utilities. Geometry dimensions are in millimetres. `parameters.json` is generated metadata, not a separate input file. `build.py` is the authoritative parametric layout.

Reports in `output/`: part validity/connectedness and interference checks, 23 lift poses, 26 gear phases, cylindrical containment, camera centre path, STEP round-trip, local height study, nine dock-approach poses and viewer-control checks. Overlap reporting threshold is 0.01 mm³. These are sampled nominal geometry checks, not continuous-motion or fabrication qualification. Viewer controls use DOM/WebGL stubs; static PNGs are visually inspected. No real-browser rendering test is claimed.

The selected build passed all listed nominal checks: 52 valid connected mover solids, no reported static/lift/gear overlaps, 43 × 43 × 25.2 mm STEP bounds, clear camera centre path and nine clear sampled dock approaches. The local 25.0/24.8 mm alternatives fail the selected battery-clearance criterion. Static overview, battery, docking and underside previews were visually inspected.

Shared viewer: https://vlopezferrando.github.io/chess-mover-viewer/ . Earlier plate-powered KST version: `43mm-kst-plate.html`.

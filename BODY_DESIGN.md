# Detailed coplanar body — first fit prototype

This revision turns the packaging concept into **three separate body parts with recessed underside fasteners, motor stops, integral axle bridges, a servo/battery carrier, a camera nest and PCB capture ledges**. It is a fit-and-assembly prototype for supplier review. It is not a released powered mechanism or a finished PCB design.

## Dimensions and deliberate changes

- **Ø44 mm × 21 mm**, retaining 21.2 mm nominal floor-to-board space and 13 mm wheels. Three Ø3.6 mm screw posts need up to a 44 mm envelope at the selected clear locations; this is a local packaging result, not proof that no possible 43 mm body exists. The front is flattened at Y=-21.5 mm to preserve the rail interface.
- Battery remains beside the servo, with the existing assumed **17.6 × 14.6 × 8 mm design envelope**. Its bottom moves from 11.6 to **12.1 mm**, leaving 0.1 mm nominal roof clearance. This is *not* a confirmed swollen-cell tolerance: supplier dimensions remain a release blocker. Do not clamp a real pouch cell into an undersized pocket.
- Main shell wall **1.2 mm**, floor **0.6 mm**, lid **0.8 mm**. Wheel/optical openings and local reliefs mean those are design dimensions, not a global minimum-thickness certification.
- Equipment shelf **1 mm**; a solid **0.8 mm servo bed** reinforces it without increasing height. It replaced two narrow ribs after the first stiffness screen. Battery shelf and side/end guards retain the cell without using it as a structural support for the servo.
- Axle bridges: two **1.5 × 2.8 mm arms** per wheel, with Ø3.2 mm nominal bores. Actual axle/gear coupling and axial retention remain undecided.
- Left rear coil moves from (-11.2,13.3) to **(-12.4,12.4) mm**, 1.5 mm displacement, to clear the lid's lift-guide socket. No coil electrical design is implied.
- Camera nest supports the existing sensor/lens envelope above the entrance pupil. It does not establish a selected camera or a confirmed retention/adhesive method.
- Three low-friction anti-tip pads are modeled with **0.1 mm nominal floor clearance**. The wheels remain the nominal floor contacts; slight pitch brings a pad into contact. Actual tire compliance, pad height, floor flatness, wheel load share and traction need measurement.

## Body joint and manufacturing detail

1. **Lower chassis**: open-top motor saddles, axial end stops, integral outboard axle bridges, front charging-contact carrier and magnet pocket, three screw-bearing seats and pad recesses.
2. **Removable equipment carrier**: servo bed and case stops, battery shelf/guards, camera nest, PCB ledges, peripheral wall. Its stepped underside mates with the chassis with a **0.1 mm nominal axial seam**; this is subject to coupon calibration.
3. **Lid**: PCB capture surface, three deep threaded bosses and two lift-guide sockets. Two separate elastomer pads apply provisional servo restraint; their free/compressed dimensions are assumptions and require measured preload.

Three nominal **M1.6 × 16 socket-head screws enter from underneath**: Ø3 × 1.6 mm heads sit in open Ø3.7 mm access pockets, with bearing seats at Z=4 mm. Ø1.8 mm clearances pass through the chassis/carrier. The lid has Ø3.56 mm bosses extending down to Z=15 mm, with through Ø1.25 pilot bores intended for **post-print M1.6 tapping**, not printed threads. Nominal thread engagement is **5 mm**, and screw tips finish 1 mm below the roof. This avoids the weak thin-walled counterbore collars of an initial top-entry trial. The threaded boss has about **1.15 mm radial material** around its pilot.

No installation torque or pullout capacity is qualified. Test the resin/thread process on the coupon before assembling the body. See [HPC's screw dimensional reference](https://shop.hpceurope.com/pdf/gb/CHC.pdf); select an actual available screw/material before ordering hardware.

The lid guide sockets have **0.4 mm nominal radial walls** (Ø2.5 outside, Ø1.7 bore), and only about 1 mm pin bonding length. They are explicitly a delicate feature requiring supplier review and retention/load tests. If unsuitable, use separate metal bushings or enlarge/reposition these mounts; do not infer strength from successful STL export. The print pack excludes the small gears, wheels, crank, tray and pins because their manufacturing interfaces are not yet detailed.

Charging contacts remain custom spring envelopes; the new carrier anchors their support to the chassis. Power rail force, contact wear, magnet retention/release and electrical charging remain unvalidated. The PCB outline now reserves screw/guide clearance and a through-pocket over the raised battery; the largest connected board region is retained. It is still not routed or proof that all circuitry fits.

## Assembly sequence to evaluate

1. Inspect and calibrate bores/joints using the coupon. Clean/cure parts using the service's specified process, tap pilot holes and verify them with screws before installing electronics.
2. Install the reference motor/gear/wheel/axle assemblies in the lower chassis; verify end-stop and saddle fits. **Shaft shortening, wheel/gear fixation and axle end retention still need exact manufactured parts**, so this currently means a fit trial, not permission to run loose gears.
3. Assemble the servo, crank, pin and magnet carriage as a module **outside the carrier**. The reference crank has no completed spline/pin-retention detail. This subassembly must be engineered before a powered build; the body assumes it can be supplied as an assembled module.
4. Lower that module into the separate equipment carrier. Fit the camera into its nest and place the battery with its leads through the rear guard openings. Establish real sensor and cell retention after selecting those parts.
5. Place the equipped carrier onto the motor chassis, with calibrated motor shims. Route leads before closing: shown channels are allowances, not a complete harness design. The body must not pinch leads or press battery terminals against the shell.
6. Place the PCB on the ledges, then lower the lid and its guide pins through the guide clearances/carriage. Hold the stack in a soft assembly fixture and install the three screws from underneath through the checked tool paths. First dry-assemble without the battery so loose parts cannot fall onto it. Test the actual guide fit before bonding pins.
7. Verify unpowered wheel freedom, lift travel, contact alignment and camera view. Perform load/retention tests before powering motors or servo.

Sampled straight insertion checks cover the servo/lift module into an empty carrier, equipped carrier onto the chassis/drive, and lid/guide insertion with the remaining assembly present. They do not validate all manual operations, lead bends, finger access, camera adhesive, servo spline or the reference drivetrain's unresolved joints.

## Initial force calculations

`src/force_screen.py` uses SI units and writes JSON/CSV. It is **analytical screening, not FEA**:

- Existing magnetic sample: 0.366 N for a 10 × 2 N42 magnet at 3.6 mm gap and 4 mm lateral offset; motor/servo steel was absent from that simulation.
- With assumed 0.1 N guide resistance, 50% efficiency and factor 3: **12.50 mN·m lift torque screen**. This is not a measured worst-case demand or a check of the supplied servo voltage/duty cycle.
- Revised solid servo bed: approximately **0.009–0.046 mm deflection** across assumed E=1–2.5 GPa and 50–100% effective stiffness, versus a provisional 0.05 mm budget. Midspan beam stress is about 0.74–1.48 MPa; no allowable material strength or certified safety factor is assigned.
- Axle-arm screen: approximately **0.004–0.019 mm deflection**, sweeping assumed 30–60 g mover masses, 5 g vertical loading and equal wheel/arm sharing. Actual mover mass is not established.

The stepped servo-bed beam includes its thinner end sections. Its supports/load sharing and the axle-arm idealization still omit 3D notches, contact preload, warpage, creep, printed anisotropy and adhesive strength. These results justified geometry changes but do not qualify the body. Measure bed compliance, axle alignment, guide binding, thread pullout and the actual lift load in the assembled chassis.

## Reproduce

Use the pinned environment in `../cad_10_coplanar/requirements.txt` and the existing setup instructions in `../cad_01_mover/README.md`. At repository root:

```sh
MPLCONFIGDIR=/tmp/mover-mpl cad_01_mover/.venv/bin/python -m cad_13_body.src.build
cad_01_mover/.venv/bin/python -m cad_13_body.src.validate
cad_01_mover/.venv/bin/python -m cad_13_body.src.check_dock
cad_01_mover/.venv/bin/python -m cad_13_body.src.check_exports
MPLCONFIGDIR=/tmp/mover-mpl cad_01_mover/.venv/bin/python -m cad_13_body.src.camera_study
cad_01_mover/.venv/bin/python -m cad_13_body.src.force_screen
MPLCONFIGDIR=/tmp/mover-mpl cad_01_mover/.venv/bin/python -m cad_13_body.src.interface_drawing
cad_01_mover/.venv/bin/python -m unittest discover -s cad_13_body/tests
node cad_13_body/src/check_viewer.cjs
```

Open `output/mover_viewer.html` and choose **Inspect body parts** or **Explode body assembly**. The exploded view explains the structure, not a collision-free assembly trajectory. STEP assemblies, separate body STEP/STL, coupon, force screens and geometric reports live in `output/`. The STL ZIP is named **body_fit_prototype.zip** deliberately. Read [PRINT_BRIEF.md](BODY_PRINT_BRIEF.md) before requesting manufacture. No quote has been requested and nothing has been ordered.

## Final nominal checks

54 valid connected modeled parts; 12 lift poses, 24 insertion samples and three underside driver paths pass. Fifteen rail approach/parking samples pass. Each of the three body STEP files reimports as one valid solid within Ø44 mm; all four STL files (including coupon) are watertight under the mesh edge check. Intentional screw/pilot overlap represents unmodeled threads and is recorded separately. Camera geometric clear area is 118.4 mm² versus 110.1 mm² previously, under the same assumed lens model; actual optics remain unqualified. Three analytical-formula tests and the viewer-control stub pass; no live-browser rendering test was performed.

Build commands refer to the local engineering source workspace. This viewer repository contains exported artifacts, not a standalone copy of the complete source project.

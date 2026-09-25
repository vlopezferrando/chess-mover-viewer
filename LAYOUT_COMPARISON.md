# Two battery layouts: side-by-side and below the motors

[Open A: side-by-side](side-by-side/index.html) · [Open B: bottom battery](bottom-battery/index.html) · [Camera comparison](side-by-side/camera_comparison.png)

Both are separate parametric CAD assemblies with STEP downloads, optional shell/lid, docking pads, a dock, full 6 mm magnet travel and 100 mAh reference batteries. They are packaging candidates, not production-ready or electrically validated hardware. The earlier stack remains in `cad_09_battery`.

## Result

| Quantity | Previous stack | A: battery beside servo | B: battery below motors |
|---|---:|---:|---:|
| Diameter | 43 mm | **43 mm** | **43 mm** |
| Mover height | 25.2 mm | **21.0 mm** | **25.2 mm** |
| Floor-to-board spacing | 25.4 mm | **21.2 mm** | **25.4 mm** |
| Wheel diameter | 13 mm | 13 mm | **20 mm** |
| Motor shaft height | 5.9 mm | 5.9 mm | **11.3 mm** |
| Camera lens height | 11.9 mm | **12.8 mm** | **16.0 mm** |
| Camera XY | (5, −13.5) | (0, −15.8) | (0, −15.8) |
| Floor window | Ø10 mm | **16 × 10 mm ellipse** | **16 × 10 mm ellipse** |
| Geometrically visible floor, assumed 60° × 45° lens | 61.8 mm² | **110.1 mm²** | **125.4 mm²** |
| RPM required for 150 mm/s, 1:1 transmission | 220 | 220 | **143** |

A saves **4.2 mm / 16.7% height** versus the previous battery stack. Motors remain in the lower layer; battery and servo share the upper layer. B trades height for larger wheels, a higher camera and a low battery. It does not reduce height versus the previous stack.

## A: put a thicker, shorter battery beside the servo

The previous thin cell's 29 × 15.5 mm body is awkward to pack beside the actuator. A manufacturer catalogue lists **LiPol LPHD7214017**, 100 mAh, 20C, **17 × 14 × 7.2 mm**. Its thicker body occupies much less plan area. Source: [LiPol manufacturer catalogue](https://www.lipolbattery.com/High-Discharge-20C-Lithium-Polymer-Battery-for-Camera-Drone.html), preserved as `sources/lipol_catalogue.html`.

This is a **catalogue candidate**, not a selected production cell. No individual supplier drawing, tab dimensions, availability confirmation, temperature-dependent discharge data or cycled-thickness specification has been obtained. The CAD uses an explicit **17.6 × 14.6 × 8.0 mm design envelope**, allowing 0.6 mm extra length/width and 0.8 mm extra thickness. These allowances are engineering assumptions, not manufacturer-certified tolerances or guaranteed swelling clearance. Another 3 mm is reserved at the terminal end. A suitable factory-wired version and real sample measurements are prerequisites for fabrication.

The battery is rotated 90° in plan, centred at (9.6, −1.2), z=11.6…19.6 mm. Its insulating shelf starts at z=11.2; side guards are relieved around the right wheel. The shelf-to-wheel gap is only about 0.1 mm at the nominal inner tire face; that is aggressive and needs tolerance allocation. The battery is not squeezed under the servo. The upper production PCB has a separate battery pocket.

The servo/lift group moves 2.6 mm left and 2 mm forward. Both alternatives now use **KST X06N**, the factory tabless version, rather than silently deleting the standard X06's tabs. A drawing-derived 20 × 16.6 × 7 mm case, 5 mm shaft offset, 2.7 mm projection and 4 mm shaft envelope are included. The shaft adapter still needs a real spline/retaining screw design. Source: [KST X06N manufacturer page](https://kstservos.com/products/x06n-v6-0-hv-micro-digital-metal-gear-glider-1-8kg-torque-servo-motor) and [manufacturer drawing](https://cdn.shopify.com/s/files/1/0570/1766/3541/files/X06N_V6.0_Technical_Specifcation.pdf?v=1700472342), saved and visually inspected in `sources/`.

A's servo occupies z=13.0…20.0 mm, overlapping the battery's vertical interval. The motors still occupy the lower region, because placing their long 32 mm shaft-inclusive shapes, the servo and battery all in the same layer was not established. The new cradle has a bridge around the left wheel and needs engineered attachment/retention. The carved PCB is one connected solid; an isolated scrap crescent is discarded. Electrical routing, RF keep-outs and board stiffness have not been proved.

The packing screen varies planar translation/rotation using conservative projected servo, crank, guide and battery shapes. It tried 29 × 15.5, 22 × 15, 17 × 14 and 15 × 15 mm battery footprints. The selected tabless arrangement was subsequently adjusted and checked in exact 3D. Nonzero search penalties are **not proofs of impossibility**, and this is not a global minimum-height proof. Reports: `output/packing_search.json`, `packing_diameters.json`, `packing_tabless.json`.

## B: battery under the drive motors, larger wheels

B retains the better-documented **Honcell HCG431528HP20 100 mAh cell**, with its **29 × 15.5 × 4.75 mm cycled envelope**, now at z=1.2…5.95 mm. The motor body bottoms are z=6.3 mm: **0.35 mm nominal vertical clearance**. The cradle is insulating; electrical insulation, puncture/crush protection and assembly tolerances require detail design. [Honcell source](https://www.honcell.com/lithium-battery/cells/hcg-lipo-battery-cells/1933); the saved full datasheet is in `cad_09_battery/sources`.

The 20 mm wheels have centres at z=10 mm and remain inside the Ø43 footprint. Motor axes rise to 11.3 mm. Motor lateral offsets and gear phase are recalculated to preserve the **6.2 mm gear centre distance** with the 1:1, 31-tooth transmission. The wheel openings grow accordingly. Sampled gear meshing and enclosure containment are checked again.

**Full 7 mm straight cell tabs collide with the larger right wheel.** This alternative explicitly requires supplier-trimmed tabs with welded flexible leads: CAD represents a 2.8 mm terminal allowance. It does not assume a user should fold, solder directly to or modify a bare pouch. Lead routing/strain relief is not finalized and the supplier configuration must be confirmed. The cell is not yet a fully packaged, protected battery assembly.

Larger wheels give **54% more linear speed at the same RPM**, but only **65% of the wheel force at the same axle torque**. 150 mm/s requires about 143 RPM instead of 220 RPM. This is kinematics, not a claim that the selected motor/battery can deliver the required loaded speed. Motor winding, current limits, magnetic drag, drivetrain losses and tire traction are still unknown.

## Does the low battery improve stability?

Lowering a battery helps if the other masses stay put. Here, the motors and upper assembly move up. `src/compare.py` makes the competing moments explicit rather than claiming a tipping result.

For an illustrative comparison with two 10 g motors, a 6 g servo and equal 3 g battery masses:

- Moving the battery centre from 15.6 to 3.575 mm changes vertical mass moment by **−36.1 g·mm**.
- Raising both motors 5.4 mm adds **108 g·mm**.
- Raising the servo 4.2 mm adds **25.2 g·mm**.
- Net change for just these components is **+97.1 g·mm**: the larger masses more than cancel the lowered battery.

The sensitivity table uses 6–12 g per motor and 2.5–4 g equal battery masses. All tested cases increase this partial vertical mass moment. These masses are explicit assumptions (apart from the nominal KST mass); the cells differ, other components are omitted and no whole-mover centre of gravity is claimed. Larger-wheel mass would also need accounting. Compared with A, B is therefore **not automatically more stable**.

The two inline wheels do not by themselves define a stable fore/aft support polygon. Final glides/casters or controlled shell contact, ground clearance, tire compliance and magnetic loading must be specified before a tipping simulation or stability guarantee. The current shell has 0.2 mm floor clearance. CAD collision clearance does not qualify rolling or rocking behaviour.

## Camera improvement and validation

Both cameras move to the front centre. The original 4 mm lens and 6 × 6 mm sensor island envelopes are retained. The floor cutout becomes a 16 × 10 mm ellipse centred at (0, −14.8). Camera connectors, flex and front electronics are repacked. This creates more usable view without inventing a thinner lens.

`src/camera_study.py` projects every non-camera mover triangle between the assumed entrance pupil and the floor, including motors, cradle and shell. Green pixels in the comparison mean an unobstructed straight ray; red means an obstruction. The comparison assumes **60° horizontal × 45° vertical FOV**, solely as a common test. At 240 × 240 samples, visible floor increases by about **78% for A** and **103% for B** relative to the previous geometry. The unclipped view rectangles are about 14.8 × 10.6 mm for A and 18.5 × 13.3 mm for B, but substantial portions remain blocked.

Doubling raster resolution from 120 to 240 changes estimated visible area by under **0.18%** across all three cases. Unit tests check unobstructed views, rejection of objects above the camera, and a known perspective shadow area. This is not a lens model: focus at 13–16 mm, entrance-pupil location, sensor aspect ratio, distortion, illumination and marker decoding all require hardware tests. Increasing physical field coverage can reduce pixels per marker.

The viewer's **Inspect camera view** button shows assumed cyan ray boundaries and the real surrounding geometry. The rays themselves are not clipped; use the comparison image for the occluded regions.

## What remains provisional

Both keep 10 × 2 mm N42 magnets, 6 mm vertical travel, four coils, production-electronics allowances, front charger pads and an external dock. Nominal magnet-to-washer gaps are 3.5/9.5 mm for a 3 mm board and 0.5 mm air clearance. Existing FEM used 3.6/9.6 mm and omits the battery/motor/servo metal; new magnetic or resonance simulations were not performed.

Power electronics are reserved volumes, not routed circuits. The small-cell current budget still requires measurement and protection/current limiting. Dock springs remain envelopes: preload, passive holding/detent, contact bounce, strain relief and autonomous navigation are unqualified. All supports, fasteners, servo cradle bonding/clamping, PCB seams and manufacturing tolerances require detailed engineering. No battery or servo has been purchased or modified.

For a compact first prototype, **A is the preferred packaging direction**, conditional on confirming the compact cell. B is a useful alternative if larger wheels and camera clearance prove more valuable than the extra height. Neither is fabrication-ready.

## Reproduce

Use the existing CAD environment and pinned dependencies in `requirements.txt`. `src/layout.py` is shared by both alternatives; original motor CAD and older gear/lift utilities are imported from this workspace.

```sh
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.build
cad_01_mover/.venv/bin/python -m cad_11_bottom_battery.src.build
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.validate
cad_01_mover/.venv/bin/python -m cad_11_bottom_battery.src.validate
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.check_step
cad_01_mover/.venv/bin/python -m cad_11_bottom_battery.src.check_step
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.check_dock
cad_01_mover/.venv/bin/python -m cad_11_bottom_battery.src.check_dock
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.camera_study
cad_01_mover/.venv/bin/python -m cad_10_coplanar.src.compare
cad_01_mover/.venv/bin/python -m unittest cad_10_coplanar.tests.test_camera
node cad_10_coplanar/src/check_viewer.cjs
node cad_11_bottom_battery/src/check_viewer.cjs
```

Optional packing screen: `python -m cad_10_coplanar.src.packing_search --tabless` or `--diameter 45` with the CAD environment. Parameters are in the shared `config()` function; generated `parameters.json` files describe the outputs.

Each output directory contains engaged/half-servo-travel/released STEP, dock and docked assembly STEP, shell STEP/STL, a ZIP containing the engaged mover and dock, the offline viewer, PNGs, component CSV and validation reports. The 55° intermediate STEP is explicitly **half servo travel**, not half vertical stroke.

**Both final assemblies passed:** 51 valid connected mover solids each, Ø43 containment, correct 21.0/25.2 mm height, no reported static collisions, 23 sampled lift positions, 26 gear phases, clear camera centre path, nine nominal dock approaches and STEP reimport. Overlap threshold is 0.01 mm³. Viewer controls are tested with DOM/WebGL stubs and rendered previews were inspected; no real-browser rendering test is claimed. There is no continuous-motion, force, tolerance or production qualification.

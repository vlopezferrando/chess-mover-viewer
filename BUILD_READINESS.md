# From packaging concept to working hardware

The selected Ø43 × 21 mm coplanar layout passes nominal CAD checks if the generated reports say so. It is not a tolerance-qualified assembly or a completed electronics design. There is no meaningful percentage-complete estimate: component selection and PCB placement can still change the shape.

## Body: a fit mock-up is nearer than an operational mover

The current model already separates a lower cup and lid, and has separate component supports and moving lift parts. But it lacks engineered joints and a demonstrated assembly path. Many supports are deliberately thin geometric allowances (including a 0.22 mm motor saddle), and cannot be treated as adequate printed load-bearing parts. Some clearances are around 0.1–0.3 mm before printer and purchased-part variation. Static noninterference is not proof of printability, strength or assembly access.

Proposed construction for the next mechanical revision:

1. Lower chassis holding motor saddles, independent axle supports, camera window and front charging cartridge.
2. Removable bridge/retainer clamping the motors and securing the servo cradle, with accessible screw paths.
3. Upper lid/PCB attachment; PCB should not be the sole structural load path for the servo or gears.
4. Separate magnet carriage and crank, with positive retention on pins and guides; removable battery restraint that does not squeeze the pouch.

This may be more than two printed parts even if the exterior looks like two pieces. Prefer screws/removable clamps for the first prototype. Reserve bosses and tool access before selecting screw sizes. Do not assume the existing envelope can absorb them. Wheels, axles and module-0.2 gears also require actual manufacture/part selection; tiny gears are not automatically suitable for the same printing process as the housing.

Before a functional print:

- Obtain exact purchasable N20 motor/gearbox/RPM variant, shaft drawing, X06N servo and spline/horn, lens/sensor/FPC, battery and termination drawings, wheels/tires/bearings, contact construction and magnet. Catalogue body dimensions alone omit tabs, plugs, lead exits and bend radii.
- Confirm the 17 × 14 × 7.2 mm candidate battery's high-current capability, maximum cycled envelope, protection arrangement and availability. Current CAD allowances are assumptions.
- Specify printer/process/material and print small fit coupons for shaft holes, motor pockets, joints and thin walls. Feed measured fit allowances back into the model; do not enlarge or shrink every part by an arbitrary universal tolerance.
- Check assembly sequence and service access: motors/axles/gears first, camera and leads, servo/lift and battery, PCB, then lid. Verify insertion sweeps, solder access, wire routing and fastener tool clearance. This order is a proposal, not a checked assembly procedure.
- Establish a stable floor support arrangement. Two wheels on one axle line alone do not establish a stable pitch support polygon; glides/casters or designed shell contacts need explicit clearances and loads.

Force cases for calculation and subsequent bench tests:

| Case | Needed evidence |
|---|---|
| Magnet separation | Magnetic force versus gap and lateral offset for actual steel/magnet/board; cam torque throughout stroke, guide friction, available servo torque at supply voltage |
| Lift structure | Crank pin shear/bending, tray and guides, servo cradle reaction; deflection compared with smallest running clearance |
| Driving / jam | Selected motor torque/current, wheel traction, axle bending, bearing retention, gear tooth/root loads and motor reaction paths |
| Docking / release | Spring curves and magnet pull curve through full retreat; traction margin, chassis pitch and contact compression stops |
| Handling / collision | Defined impact/load case, lid joints, screws and battery clearance; printed-material strength in intended orientation |

Use simple free-body/beam checks first, then FEA for the actual load-bearing geometry and print direction. Do not substitute isotropic bulk-plastic strength for tested printed parts. No structural FEA has been completed for this revision. A fit-only mock-up can precede those load checks, but a powered assembly should not be represented as qualified by it.

## PCB: still a functional block-space allocation

The CAD has a 41 mm board outline with large battery, servo and lift cutouts. Coloured IC/charger/boost boxes reserve volume; they are not placed real footprints, a netlist or routed circuitry. The full circular area is not usable PCB area, and narrow remaining bridges constrain routing and stiffness. We have not yet proved all required electronics fit.

Required decisions before a meaningful placement study:

- ESP32 variant, memory requirements, clock and reset/boot/programming circuitry, antenna location and keepouts. Metal motors, battery and magnets nearby make radio placement a genuine packaging constraint.
- Actual camera sensor and lens, interface, rails, clock, FPC/connector, required image rate and firmware resources. Optical working distance remains unproven.
- Two motor drivers sized from selected motor stall/start currents, chosen PWM/control scheme, optional encoder needs and connectors/solder points.
- Servo supply and transient load; determine whether the battery can supply it directly or needs conversion, and reserve inductor/capacitor height and copper area.
- Charger, battery protection, charge-current setting, power-path behaviour, low-battery measurement/fuel gauge, switches, test/programming pads and docking input protection.
- A complete power budget covering Wi-Fi/camera, motor startup, servo loading and any coils, including battery voltage sag and converter losses.
- Define what the four resonance coils actually do: inductance, frequency, Q, conductor geometry, capacitors, excitation/sensing circuits and copper/metal keepouts. Their visible rings are geometric placeholders, not an electrically designed subsystem. An initial board may explicitly reserve coils without populating their eventual circuits, but that would not confirm the final all-functions board fits.

Suggested sequence:

1. Freeze candidate component list and interface/power requirements; verify the electrical subassemblies with evaluation boards or bench wiring.
2. Create a complete schematic with real part numbers and footprints, including every passive and test point.
3. Import the current mechanical outline and height zones; perform a real placement and routing feasibility study (a 4-layer board is a candidate, not yet a requirement or proven solution).
4. Export the PCB assembly STEP back into this CAD; revise mounts, cutouts, camera flex routing, coil/antenna clearances and assembly access together.
5. Route, run electrical/design-rule checks, review return paths, thermal/current paths and manufacturability, then order a first assembled revision.
6. Bring up charging, power rails and MCU before motors/servo; measure startup brownouts, radio/camera performance and coil interaction. Revise board/body based on measured problems.

Recommendation: stop squeezing the envelope until the exact-part and real-PCB-placement steps are done. Keep Ø43 × 21 mm as a target, not a promise. Printing a larger accessible test chassis may accelerate validation while compact packaging develops. The PCB and enclosure must be iterated together; finalizing one before placing the other risks rework.

# Coplanar mover with wall-rail charging

Chosen architecture: Ø43 × 21.0 mm, 21.2 mm floor-to-board, 100 mAh catalogue battery beside KST X06N, 13 mm wheels, 10 × 2 mm piece magnet with 6 mm lift. This is a **packaging concept, not a manufacturing release**. Existing battery, lens, motor, PCB and structural caveats from [iteration 10](LAYOUT_COMPARISON.md) still apply.

## Charging arrangement

Two mover contacts share a vertical column at X=0, facing the front wall:

| Element | Height above floor | Nominal geometry |
|---|---:|---|
| Separate retaining magnet | 4 mm centre | Ø3 × 1 mm; packaging placeholder |
| GND contact | 8 mm centre | Custom compliant leaf allowance |
| +5 V charger input | 13.5 mm centre | Custom compliant leaf allowance |

The station has 100 mm long horizontal rails, 2.4 mm high, separated by insulating backing, plus a separate 3.4 mm high passive steel strip. The magnet-to-steel gap is 0.95 mm at the seated pose. Two insulating strips limit nominal overtravel against the shell. Rail materials/finish, contact material, preload, magnet grade/force, fasteners and tolerances remain unspecified. The spring geometry depicts a nominal seated position; it is neither a purchased part nor an elastic calculation. Its 6 mm leaf span and 0.08 mm thickness are packaging allowances only. The square tip is a stand-in for a rounded wiping contact.

The mover can park **anywhere along an equipped straight wall, facing it**. This is not charging at arbitrary room positions or headings. Wall corners, rail joins, yaw capture and end stops need separate design. Neither a continuous steel strip nor a round shell passively selects the correct heading: floor-marker navigation must align it. The along-rail slider illustrates different parking positions, not a sliding-while-charging recommendation.

Recommended first experiment: small recessed mover magnet against passive steel, with gold-plated low-force wiping contacts. Keep retention electrically separate from the power rails. Tune the retaining force through recess/gap changes. The displayed 3 × 1 mm magnet has **no verified force prediction**. Do not order it solely from this CAD.

## Why not just magnetic tape on the wall?

Magnetic rails exist. [FIRST4MAGNETS](https://www.first4magnets.com/comparing-our-flexible-adhesive-range) distinguishes ferrite magnetic tape, neodymium magnetic tape and passive steel tape. Magnetic tape plus a steel mover keeper is a plausible alternative that removes the extra permanent magnet from the mover. However, holding force varies with material, pole pattern, overlap and gap, and introduces a permanent magnetic field along the wall. Discrete wall magnets could instead produce preferred docking locations. Passive steel still interacts with the piece-carrying magnet, so either arrangement requires a full-assembly magnetic check, especially with that magnet lowered. Extra mover magnets can also attract other movers and ferrous debris; weak retention is preferable.

Compact commercial contacts are not automatically soft: [Harwin's catalogue](https://cdn.harwin.com/pdfs/Harwin_Product_Catalog_page_278.pdf) lists 0.49 N working force for S7131-45R. Two such contacts would require roughly 0.98 N just to counteract their springs. This is an example, **not a selected part**. A smaller current requirement does not itself guarantee a reliable low-force contact.

A holding magnet must exceed both contact spring forces plus disturbance margin. During retreat, springs initially assist separation; after they unload, the wheels must overcome the remaining magnetic attraction. Thus evaluate the entire force-versus-distance curve:

`required wheel force(d) = max(0, F_magnet(d) - sum(F_spring(d))) + rolling resistance`

Compare it with `min(2 * wheel_torque / wheel_radius, tire_mu * driven_wheel_normal_load)`. Motor torque, tire friction and wheel load are not yet measured. Also check pitch moments because the retaining magnet and contacts act at different heights; the nominal insulating stops do not prove stability. Pull ratings at ideal contact cannot establish this result: [K&J's test explanation](https://www.kjmagnetics.com/blog/testing-magnet-strength) describes thick steel and zero-gap conditions and the effect of gaps.

Bench acceptance: both contacts remain inside their rated compression range, contact voltage drop is within charger headroom, charging is stable across repeated placements, and the mover backs away at low battery without wheel slip. Test rail dirt/oxidation and tolerance extremes. Use current-limited rail supply, input protection and a real 1S charger/protection circuit, not direct battery connection. Rail current must cover simultaneously docked movers. Set charge current from the actual cell specification; 100 mAh capacity is not a charge-current rating. Exact supply, charge current and circuit remain undecided.

## Reproduce and inspect

Use the existing CadQuery environment from `cad_01_mover/README.md`, at repository root:

```sh
MPLCONFIGDIR=/tmp/mover-mpl cad_01_mover/.venv/bin/python -m cad_12_rail_dock.src.build
cad_01_mover/.venv/bin/python -m cad_12_rail_dock.src.validate
cad_01_mover/.venv/bin/python -m cad_12_rail_dock.src.check_dock
cad_01_mover/.venv/bin/python -m cad_12_rail_dock.src.check_step
MPLCONFIGDIR=/tmp/mover-mpl cad_01_mover/.venv/bin/python -m cad_12_rail_dock.src.camera_study
node cad_12_rail_dock/src/check_viewer.cjs
```

Open `output/mover_viewer.html`; choose **Show docking station**, then **Position along wall rail**. STEP assemblies, the rail assembly, shell STEP/STL files and checks are in `output/`. Shell STL export means a meshed CAD shape exists, not that the body is fabrication-ready. Existing and revised camera silhouettes are compared using the same assumed 60° × 45° lens; real close focus and optical recognition remain unverified. Viewer checks execute controls against a stub, not an actual browser rendering test.

See [BUILD_READINESS.md](BUILD_READINESS.md) for what separates this layout from a printable functional body and a routed PCB.

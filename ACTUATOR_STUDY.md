# Smaller lift actuator: force and packaging screen

The FS0307 is already laid on its 8.3 mm side above the drive motors. A lighter servo does not necessarily reduce height: the smallest relevant case dimension matters. Changing the actuator also changes shaft position, supports and the cam/yoke geometry. This comparison was prepared for the iteration 7 FS0307 layout. Iteration 8 now incorporates KST X06 into nominal CAD; alternatives below retain their original sizing context. Hardware strength and performance remain unvalidated.

## Retraction load

Existing Simulation 5 predicts 0.231 N downward on the washer (equal upward on the magnet in the isolated model) for a centered 10×2 N42 magnet at 3.6 mm separation. At 4 mm lateral offset, it predicts **0.366 N**. Centered force alone would undersize the actuator. Both values assume the modeled washer and omit nearby motor/servo steel and conducting-plate dynamics.

For vertical slider displacement z=e cos(theta), the ideal shaft torque magnitude is `F * e * abs(sin(theta))`. Current stroke is 6 mm over 70–180 degrees, with e=4.471 mm. Using the largest sampled engaged force over the whole stroke and the maximum moment arm gives **1.64 mN·m**. This is a conservative envelope relative to those samples, not proof of a global force maximum. A sample at another gap/offset or actual chassis attraction could exceed it.

Sizing scenarios use `(F + guide resistance) * e / efficiency * design factor`:

| Assumptions | Required shaft torque, 10×2 magnet |
|---|---:|
| Magnetic load only | 1.64 mN·m |
| 0.05 N guide resistance, 70% efficiency, factor 2 | 5.32 mN·m |
| 0.10 N guide resistance, 50% efficiency, factor 3 | 12.50 mN·m |

Guide resistance and efficiency are assumptions, not measurements. The factors are engineering allowances, not a certified safety factor. Carrier gravity assists lowering; raising and acceleration need separate checks. Shaft-bearing lateral load, backlash, jamming, wear, and duty cycle also matter. The piece's full weight is not added to this lowering force: it remains supported by the board.

## Candidate actuators (manufacturer data checked 2026-09-24)

| Candidate | Case dimensions | Torque / force information | Assessment |
|---|---|---|---|
| FEETECH FS0307, earlier baseline | 20×8.3×17.3 mm | 49.0 mN·m stall at 4.8 V | Strong nominal margin; stall is not continuous torque. |
| AGFRC C017CLS | 13.5×6.2×16 mm | 6.37 mN·m stall at 3.7 V; 7.35 at 4.2 V | Smaller but marginal: moderate scenario approaches stall and cautious scenario exceeds it. Do not select without measured loads. Needs a regulated 3.6–4.2 V supply. |
| KST X06 | 20×7×16.6 mm | Manufacturer linked sheet gives 40 mN·m rated at 6 V; 150 mN·m stall | Best documented servo candidate for a modest reduction. Case thickness saves 1.3 mm; 19.8 mm overall height is only stack arithmetic, not checked CAD. Check delivered revision, shaft and tabs. |
| Pololu 2359, 700:1 sub-micro planetary gearmotor | Ø6×21 mm body, shaft additional | 90 RPM no-load at 6 V; gearbox instantaneous torque limit ~24.5 mN·m | Promising custom actuator, potentially 2.3 mm less body thickness than FS0307. Requires separate H-bridge, position/end sensing, mounting, cam coupling and holding strategy. No full-layout fit claim. |
| AGFRC C1.5CLS PRO linear servo | 21.4×15.2×6 mm; 9 mm stroke | Maker lists g·cm torque for a linear output | Useful shape, but published units do not establish linear thrust. Do not convert the torque listing into force without screw/gear data or a clarified thrust rating. Horizontal installation also needs a bellcrank/wedge to lift vertically. |

Pololu warns against exceeding the gearbox limit or stalling and recommends a brushed motor operating current generally at or below 25% of stall current. For the 2359, the cautious 12.5 mN·m scenario is below that gearbox limit; that is a screening result, not a continuous rating. Nominal 110-degree travel at 90 RPM takes 0.204 s unloaded, longer under load. Reduction gearing does not automatically guarantee self-locking. End-position sensing plus a mechanical dwell/latch could avoid sustained holding current. Do not use the attractive 0.9 kgf·cm motor stall figure as the permissible gearbox torque.

The linear servo and geared motor might help package components side-by-side; neither guarantees a thinner complete mover. Wheels remain a 13 mm lower bound, but the optical module, 6 mm magnet stroke and carrier, PCB and contacts impose other bounds. The 150 mm/s horizontal speed target does not set the lift actuator speed directly.

## Sources

- [FEETECH FS0307 specification](https://www.feetechrc.com/Data/feetechrc/upload/file/20220608/6379029528194935652722624.pdf)
- [AGFRC C017CLS manufacturer page](https://agfrc.com/index.php?id=2427). Page contains conflicting case-material text; verify the actual part drawing and sample.
- [KST manufacturer-linked manuals](https://kstservos.com/pages/user-manual), [linked X06 sheet](https://cdn.shopify.com/s/files/1/0570/1766/3541/files/X06-2021423-172520969.pdf?v=1660891701). Link is labeled V6 on the site but serves a 2021 document; confirm supplied revision before design freeze.
- [Pololu 2359 specifications and operating limits](https://www.pololu.com/product/2359), [dimension drawing](https://www.pololu.com/file/0J1831/sub-micro-plastic-planetary-gearmotor-dimension-diagram.pdf)
- [AGFRC C1.5CLS PRO manufacturer page](https://www.agfrc.com/index.php?id=2438)

## What to measure first

Measure retraction force versus gap with the actual washer, board, magnet and nearby steel, including lateral offsets. Measure guide breakaway friction and check for binding. Then run the candidate actuator at the intended supply voltage across repeated loaded cycles, recording current, travel time, temperature and endpoint repeatability. Choose rated operating torque comfortably above measured peak load; stall torque is not an operating target.

Reproduce the numerical sizing screen with `cad_01_mover/.venv/bin/python -m cad_07_43mm.src.actuator_study`. CSV/JSON results are in `output/actuator_loads.*`. This reuses existing FEM data; it is not a new FEM simulation of the assembled mover.

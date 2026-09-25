# Supplier review / fit prototype — Barcelona

**Status: request-for-review package, not a manufacturing release for a working mover.** No files have been sent to a supplier. Dimensions are in millimetres. Do not apply automatic unit conversion or global fit scaling.

## Suggested service

Start with **INEO, Terrassa (Barcelona)**: [SLA service](https://www.ineo.es/es/?Itemid=148). Their published service covers locally produced resin technical prototypes. Ask them to recommend an engineering resin and review the delicate features, dimensional tolerances, cleaning and cure/orientation effects. Their page lists Accura Xtreme with a flexural modulus of 1.52–2.07 GPa, making it a candidate to discuss within the stiffness range screened here. That published range does not qualify these printed parts or their joints. This is a candidate supplier, not an endorsement based on a completed job or a quotation.

An alternative local route is [El Tucán's Barcelona printing service](https://eltucan.es/305-impresion-3d), which lists SLS PA11/PA12. The current small sockets and joints must be reviewed/revised for that process; this CAD is not claimed to be interchangeable across SLA and SLS without changes. [Formlabs' design guide](https://formlabs-media.formlabs.com/filer_public/a0/67/a06705a2-8065-4d99-8a5f-409fa01e684c/2401955-wp-enus-0.pdf) illustrates why feature guidance is tied to a particular machine/material/process rather than being a universal printability promise.

## Files / quantities

| File | Quantity | Purpose |
|---|---:|---|
| fit_coupon.stl | 1 initially | Check bores, tappability, thin walls and process bias |
| lower_chassis.stl | 1 after coupon review | Motor/axle support and lower body |
| equipment_carrier.stl | 1 after coupon review | Servo/battery/camera support and upper sidewall |
| lid.stl | 1 after coupon review | Threaded bosses, PCB capture and guide sockets |

STL tessellation tolerance is 0.025 mm for body parts. STEP files are also supplied for inspection and dimension checks. These files contain **no support structures**; supplier determines orientation/supports. Critical seating faces, bores, screw counterbores, guide sockets and battery pocket should be kept free of support scars where practical, with any required finishing agreed in advance.

## Review dimensions before accepting the job

- Envelope Ø44 × 21 mm; 1.2 mm main wall, 0.6 mm floor, 0.8 mm lid. Camera/wheel openings make local edges more delicate.
- Guide sockets: Ø2.5 outside / Ø1.7 bore, about 1 mm bonding length for nominal Ø1.6 steel pins. **0.4 mm radial walls require explicit review.** A metal-bushing redesign may be necessary.
- Axle bores: Ø3.2 nominal for a Ø3 reference axle; this is a printed-fit allowance, not a bearing specification. Roundness/coaxial alignment matter.
- Three Ø1.25 through pilots in the lid bosses, intended for M1.6 tapping; Ø1.8 shaft clearances and open Ø3.7 underside head-access pockets. Screw heads bear at Z=4 mm and nominal thread engagement is 5 mm. Threaded bosses are Ø3.56 mm outside. Ask whether the supplier can tap these holes and test a matching coupon. No heat-set inserts are specified.
- Main body seam: 0.1 mm nominal axial gap. Threaded-boss-to-carrier radial clearance 0.17 mm. Confirm realistic printed clearances before making a full set.
- Battery room includes assumed allowances but only 0.1 mm remaining top clearance. Obtain supplier maximum cell/lead/cycled dimensions first; do not force a cell into a printed part.
- Servo nominal 20 × 16.6 × 7 mm, lateral pocket allowance 0.2 mm. Verify actual X06N sample and lead exit. Shims/compression pads are separate materials, not printed features.
- Interference-free nominal assembly does not prove tolerances. If the proposed process cannot hold the required fits, report that and revise CAD; do not quietly scale the full assembly.

## Coupon map

Base: 42 × 24 × 2 mm. X positions -15,-9,-3,3,9,15 mm at Y=-4 mm have through bores **1.20, 1.25, 1.30, 1.70, 1.80, 3.20 mm**, respectively, in raised bosses. Thin walls at X=-12,-6,0,6,12 mm, Y=5 mm, are **0.4,0.6,0.8,1.0,1.2 mm** thick and 6 mm high. The layout map identifies the features; no dimensions are embossed into the small faces.

Measure after the specified full cure/conditioning. Record material, printer, layer settings, orientation, finishing and measured sizes. Test tapping/assembly on the coupon, then adjust individual CAD fits rather than globally scaling the model.

## Message the user can send (not sent)

Hola, estoy desarrollando un pequeño robot de unos 44 mm de diámetro y 21 mm de alto y quiero revisar la fabricabilidad de una primera carcasa mecánica. Adjunto tres piezas separadas en STEP/STL y una probeta de ajustes. Antes de fabricar la carcasa completa, me gustaría validar la resina, las tolerancias y el mecanizado posterior de tres roscas M1.6.

¿Podéis revisar especialmente los alojamientos de guía con pared de 0,4 mm, los taladros de eje de 3,2 mm, las caras de apoyo y las holguras indicadas en este documento? No necesito una resina decorativa; busco un prototipo de ajuste con comportamiento mecánico documentado. Si alguna zona debe rediseñarse, prefiero saberlo antes de imprimir. Por favor, separad el presupuesto de la probeta y el de las tres piezas, e indicad el material, el poscurado, las tolerancias alcanzables y los acabados necesarios.

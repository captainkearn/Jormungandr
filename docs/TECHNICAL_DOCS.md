 TECHNICAL DOCS – KearnXY-300 (Concept)

 1. Design goals
- Voron-style enclosed CoreXY optimized for high-speed printing
- Very rigid primary structure using 4040 extrusions
- Lightweight, stiff motion system using 2020/3030 where appropriate
- Standardized Voron ecosystem: StealthBurner mount, backpack electronics bay, Klipper-first design
- Serviceability: panels, access, cable routing, strain reliefs
- Safety: mains bed heater, earth bonding, thermal fusing, segregated AC/DC



 2. Build volume & envelope
Target build volume: 300 × 300 × 350 mm.

 Recommended internal “cube” sizing (starting point)
To realistically achieve 300 mm travel while maintaining clearance for:
- toolhead + endstops
- X/Y carriage overtravel
- belt/idler stacks
- bed supports and Z towers

Start with a nominal internal frame cube of:
- Inner XY clear size: ~ 420 × 420 mm (between inner faces)
- Inner Z clear height: ~ 520 mm

This is consistent with Voron-class printers where internal space exceeds build volume significantly.

 3. Frame concept (4040 primary)
 Primary structure
- 4040 extrusions for:
  - bottom perimeter square
  - top perimeter square
  - 4 vertical corner posts
- Corner joining:
  - internal 4040 corner cubes/plates + gussets
  - or 4040 “blind joints” + external plates
- Enclosure:
  - Voron-style paneling (ACM/PC) attached to frame with panel clips
  - door(s) front, removable rear panel for backpack service access

 Example cut list (parametric)
Let:
- `W = frame_outer_x`
- `D = frame_outer_y`
- `H = frame_outer_z`

Then:
- Bottom square: 2× W, 2× D
- Top square: 2× W, 2× D
- Verticals: 4× H

> Actual cut list depends on your corner method (butt joint vs. through joint).



 4. Motion system (CoreXY, 9mm belts)
 Rails
- Y rails (left & right): MGN12H, mounted to the top frame members or dedicated 3030 crossbars
- X rail: MGN12H, mounted to the X extrusion (typically 2020 or 3030), carrying the toolhead carriage

Starting rail lengths (typical for 300-class):
- X rail: 400–450 mm
- Y rails: 450–500 mm

> Choose rail lengths based on carriage width, endstop placement, and belt anchor geometry.

 Gantry extrusions
- X beam: 3030 recommended (stiffer in bending), 2020 acceptable for lighter toolheads
- Y beams/bridges: 2020 or 3030 depending on stiffness needs

 Belt path
- Belt width: 9 mm (both loops)
- Use matched pulleys/idlers:
  - 20T or 16T motor pulleys (9mm) for resolution/torque preference
  - flanged idlers where required
  - consistent stack-up to keep belts parallel (avoid twist)

Voron-style layout:
- Motors on rear top corners (or rear bottom corners) depending on packaging
- Idlers at front corners
- Belt runs along left and right sides to X carriage anchors

 Motor selection & tuning
Given “Super Speedy/Super Power” NEMA17s:
- Run higher acceleration with good cooling
- Keep moving mass low (short, supported wiring, lightweight toolhead where possible)
- Consider 48V XY for higher top speed (requires appropriate drivers and PSU) – optional



 5. Z axis (3-point, Z_TILT)
 Recommended approach (Voron-style, robust)
- 3 lead screws (T8x2 or T8x4) driven by 3 NEMA17 motors
- 3-point kinematic bed support (front-left, front-right, rear-center or rear-left)
- Klipper Z_TILT with 3 independent Z motors
- Z linear guides:
  - 2× MGN12 rails (rear) + 1× MGN12 (front) OR
  - 2× MGN12 (left/right) + 1× additional guide via extrusion/rod
  - If you want simpler: 2× MGN12 (left/right) plus a third constraint via screw positions

 Why 3-point?
- Z_TILT works extremely well
- Fewer components than 4Z while still providing active tramming
- Avoids bed “racking” if guides are properly constrained

Note: 4Z is also possible, but you asked for Z_TILT; 3Z is the cleanest implementation.



 6. Bed system (110V heater)
 Bed stack (typical)
- Cast tooling plate (MIC6/ATP-5) 8–10 mm
- 110V silicone heater sized for plate (usually ~ 300×300 heater slightly smaller)
- Cork/silicone insulation layer under heater
- Thermal fuse bonded to plate underside
- SSR (quality brand) mounted to heatsink
- Mains wiring with:
  - earth/ground bonding to bed frame/plate
  - strain relief
  - proper gauge wire
  - fused inlet + switch
  - separate AC compartment in backpack

Safety requirements
- Always use a thermal fuse on the bed
- Earth bond all exposed metal that can become energized
- Provide an enclosure for mains connections
- Use proper crimped terminals and ferrules
- Follow local electrical codes



 7. Toolhead (StealthBurner mount)
- Use a standard StealthBurner mounting interface
- X carriage should expose the Voron mounting pattern (or adapter plate)
- Cable management:
  - umbilical or drag-chain
  - toolhead PCB optional (SB toolhead PCB is common)


 8. Backpack electronics bay
 Layout goals
- Rear-mounted “backpack” that houses:
  - DC PSU(s)
  - controller + drivers
  - SSR + AC distribution (in segregated compartment)
  - fans + filters
- Cable routing:
  - DC harness to gantry through top rear passthrough
  - AC harness isolated and strain-relieved
- Cooling:
  - intake low, exhaust high (or filtered intake)
  - keep controller/driers in airflow path

 Compartmentalization (recommended)
- Left side: DC (PSU + controller)
- Right side: AC (inlet + fuse + switch + SSR + bed output)
- Divider plate between sides



 9. Printed parts guidance (ABS/ASA/engineering)
- Prefer heat-set inserts for serviceability
- Design with:
  - 4-6 mm wall thickness for structural parts
  - ribs and fillets
  - avoid long, thin cantilevers near motors/rails
- Use annealed parts when possible for highest stability
- Consider CF-ABS/ASA or PC blends for high-load parts (idler mounts, motor mounts)



 10. Firmware (Klipper) high-level plan
- CoreXY kinematics
- Z with 3 drivers/motors (Z, Z1, Z2)
- Enable `z_tilt` with 3 probe points
- Bed heater: controlled via SSR as `heater_bed`
- Safety:
  - `verify_heater` tuned
  - temperature limits
  - thermistor placement validated



 11. Suggested BOM (high level)
Motion
- 2× XY motors (NEMA17 LDO Super Speedy/Power)
- 3× Z motors (NEMA17)
- 1× MGN12H X rail + carriage
- 2× MGN12H Y rails + carriages
- 9mm GT2 belts (2 loops) + 9mm pulleys/idlers
- Idler stacks, spacers, shoulder bolts

Structure
- 4040 extrusions (frame)
- 2020/3030 extrusions (gantry/crossmembers)
- Corner plates/gussets, T-nuts, bolts

Bed
- 300×300 cast plate or CNC cut aluminum plate
- 110V heater + insulation
- SSR + heatsink
- thermal fuse
- wiring + inlet + fuse + switch

Electronics
- Controller (Klipper-compatible)
- Stepper drivers (adequate for your voltage/current)
- DC PSU(s), optionally 24V + 48V for XY
- Fans, filters, wiring, cable glands



 12. Mechanical validation checklist
- Belt planes parallel; no twist
- Idler stack-ups aligned with motor pulley centerlines
- Rail mounting surfaces coplanar
- Z screw alignment and anti-backlash (if used)
- Bed plate flatness + mounting compliance (avoid warping plate)
- Enclosure clearance for toolhead at max Z



 Not included (yet):
- Real idler stacks, pulleys, belt path, carriage plates
- Panel clips, hinges, latches
- Detailed printed parts



# Jormungandr
Project Jormungandr Is a Concept 300x300x350 Core XY Rigid Frame Printer Designed for highspeed, precision printing

A Voron-inspired, high-speed CoreXY 3D printer concept using 4040 for the primary frame, 2020/3030 for gantry/secondary structure, MGN12H linear rails, 9mm belts, a backpack-style side mounted electronics bay, 110V bed heater, and a StealthBurner-compatible toolhead mount.

> Status: Concept + parametric layout + placeholder CAD primitives. This repo is a starting point for a full CAD/DFM cycle.

 Key specs
- Build volume (target): 300 × 300 × 350 mm (X×Y×Z)
- Kinematics: CoreXY, 9mm belts
- Rails: MGN12H (X and Y), MGN12H or MGN9 for Z guides (configurable)
- Motors: LDO “Super Speedy / Super Power High Temp” NEMA17 (XY), NEMA17 (Z)
- Z: 3-point Z with Z_TILT (Klipper) via 3 lead screws (recommended) 
- Bed: 110V silicone heater + SSR + thermal fuse + earth bonding (safety mandatory)
- Electronics: Rear “backpack” bay (Voron style), separated AC / DC compartments

 Files
- `/docs/TECHNICAL_DOCS.md` – design decisions, sizing, cut lists, rails, belt routing, Z system, electronics bay
- 
- Do a belt-path/idler stack-up check with real pulleys
- Validate rail lengths with carriage clearances
- Thermal design of enclosure + electronics bay airflow
- Electrical safety review for mains bed heater

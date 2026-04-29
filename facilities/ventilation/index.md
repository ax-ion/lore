# Industrial Ventilation

The references to cite — and the traps to avoid — when specing exhaust fans, makeup air, and moisture/heat removal for an industrial space. Knowing the right standard turns a vendor pitch into a defensible spec.

---

## Core Standards

**ACGIH — *Industrial Ventilation: A Manual of Recommended Practice for Design***
The bible. Sizing methodologies for steam, dust, fumes, and heat removal. Has actual calculations for latent heat loads, capture velocities, and hood designs. Not free, but every plant engineer needs access to a current edition.

**ASHRAE Handbook — HVAC Applications, Ch. 32 (Industrial Local Exhaust)**
Complementary to ACGIH. Stronger on system-level design — duct sizing, fan curves, pressure balancing. Ch. 30 (Industrial AC) covers makeup air and dehumidification.

**AMCA 210 / AMCA 211**
210 is the test method for fan performance. 211 is the certified-ratings program. If a fan submittal doesn't carry the AMCA seal, the published CFM is marketing — not tested.

**NEC 430.102**
Disconnect within sight of the motor. Required, not optional. Vendors leave it off the quote unless you ask.

**OSHA 29 CFR 1910.94**
General ventilation requirements. Mostly enforces the use of ACGIH/ASHRAE methods — the regulatory teeth behind "you need real ventilation, not a token fan."

---

## What Gets Overlooked

- **ACH alone is the wrong sizing target for steam/heat/fume rooms.** Air-changes-per-hour (volume × ACH ÷ 60) treats the room as a uniform mixing volume. ACGIH sizes based on capture velocity *at the source*. For washrooms or kitchens with continuous steam, industrial norm is 20–30+ ACH, not the 10–15 ACH you'll see quoted for general office space.
- **AMCA-certified ratings matter most when comparing two bids.** Without certification, the higher-CFM-at-lower-price fan often *underperforms* in the field. Require certification on the spec sheet, not just the brochure.
- **Submittals beat datasheets.** A datasheet is what the manufacturer publishes for the catalog; a submittal is what they're committing to deliver for *your* job at *your* static pressure. Always require submittals before approving the order — and read the fan curve at your actual operating point, not the peak.
- **Disconnect language on the PO matters.** "Fused disconnect, NEMA 4X for outdoor / wet locations, mounted within sight of motor per NEC 430.102." Without that, vendors ship NEMA 1 indoor disconnects that rust out in two seasons on a wet rooftop.
- **Makeup air is its own calculation.** Exhaust without enough intake just pulls harder on cracks and doors — fans go off their rated curve, performance falls off, and combustion appliances can backdraft (CO risk). Rule of thumb: keep face velocity through the makeup opening below ~700 fpm.
- **Backdraft prevention is separate from the weather hood.** A "dome" or wind band on an upblast fan keeps rain out; it doesn't necessarily stop reverse airflow when the fan is off. If you don't want warm wet outdoor air drifting back into the room on still days, spec an integral backdraft damper.
- **Fix the source before you size the fan.** A leaking heat exchanger or failing steam trap will out-produce any reasonably sized exhaust system. Service the source first; otherwise the new fans are buying you proportionally less than the math suggests.
- **Corrosion is a material-selection problem, not a fan-sizing problem.** Aluminum housing, sealed motors, stainless fasteners, and coated wheels all cost extra on the PO and pay back in years of service life. Galvanized steel in a steam room is a planned replacement, not a permanent install.

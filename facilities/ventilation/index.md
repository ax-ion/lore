# Industrial Ventilation

The references to cite — and the traps to avoid — when specing exhaust fans, makeup air, and moisture/heat removal for an industrial space. Knowing the right standard turns a vendor pitch into a defensible spec.

---

## Core Standards

**ACGIH — *Industrial Ventilation: A Manual of Recommended Practice for Design***
The bible. Sizing methodologies for steam, dust, fumes, and heat removal. Has actual calculations for latent heat loads, capture velocities, and hood designs. Not free, but every plant engineer needs access to a current edition.

**ASHRAE Handbook — HVAC Applications, Ch. 32 (Industrial Local Exhaust)**
Complementary to ACGIH. Stronger on system-level design — duct sizing, fan curves, pressure balancing. Ch. 30 (Industrial AC) covers makeup air and dehumidification.

**AMCA 210 / AMCA 211 / AMCA 300 / AMCA 311**
210 and 300 are the test methods (air and sound). 211 and 311 are the certified-ratings programs. Spec language: *"Fan(s) shall bear the AMCA Certified Ratings Program seal for air performance per AMCA 211 and sound performance per AMCA 311."* Without the seal, the published CFM and sone numbers are marketing, not tested.

**ASHRAE 62.1, Appendix B**
Sets the math for minimum exhaust-to-intake separation distance and discharge velocity. Discharge velocities in the 1,500–2,000 fpm range with vertical upward discharge get you out of trouble on most rooftops; horizontal or capped discharge tightens the required separation distance significantly.

**NEC 430.102**
Disconnect within sight of the motor. Required, not optional. Vendors leave it off the quote unless you spec it — and on a wet rooftop, spec NEMA 4X enclosure too.

**OSHA — General Duty Clause 5(a)(1), 29 CFR 1910.22, 1910.141**
There is no OSHA standard that prescribes a CFM or ACH for general steam/heat removal. The applicable hooks are: the General Duty Clause (heat stress is a recognized hazard), 1910.22 (slip/fall housekeeping), and 1910.141 ("the floor of every workroom shall be maintained, so far as practicable, in a dry condition"). 1910.94 is *not* the right citation — its scope is abrasive blasting, grinding, and spray finishing only.

---

## Sizing Hierarchy

Three legitimate methods, in order of rigor:

1. **Source capture (ACGIH).** Hood the source, pull 50–100 fpm of capture velocity at the face. Most efficient by far; requires ductwork.
2. **Latent / sensible load (ASHRAE).** Measure or estimate the moisture or heat release rate, then solve psychrometrically for the CFM that holds room humidity ratio (or temperature) under target. The honest answer for whole-room dilution.
3. **Curb-limited or budget-limited maximum.** When 1 and 2 are off the table — no hood, no measured source data — the binding constraint is whatever you *can* install. Pick the largest corrosion-rated fan that mates to the existing curb, select for max CFM at realistic static pressure, and back-check ACH only as a sanity ratio.

ACH-as-a-target ("we need 20 ACH") is a heuristic, not a sizing method. It's fine as a sanity check after the real calc, never as the input.

---

## What Gets Overlooked

- **"CFM at 0.000 in. SP" is the marketing number.** Free-air CFM is what the fan moves with no resistance — never what it moves on a roof curb. Curb height, weather hood, backdraft damper, and bird screen each cost static. Real-world install static is 0.25–0.5 in. w.g., where rated CFM drops 30–50% off the free-air number. Always demand the fan curve at your actual operating point, not the headline figure.
- **AMCA-certified ratings matter most when comparing two bids.** Without certification, the higher-CFM-at-lower-price fan often *underperforms* in the field. Require AMCA 211 (air) **and** AMCA 311 (sound) seals on the published rating, not just the brochure.
- **Submittals beat datasheets.** A datasheet is what the manufacturer publishes for the catalog; a submittal is what they're committing to deliver for *your* job at *your* static pressure. Read the curve at your operating point, not the peak.
- **Disconnect language on the PO matters.** *"Fused disconnect, NEMA 4X for outdoor / wet locations, mounted within sight of motor per NEC 430.102."* Without that, vendors ship NEMA 1 indoor disconnects that rust out in two seasons on a wet rooftop.
- **Makeup air is its own calculation.** Exhaust without enough intake just pulls harder on cracks and doors — fans go off their rated curve, performance falls off, and combustion appliances can backdraft (CO risk). Keep face velocity through the makeup opening below ~700 fpm.
- **Backdraft prevention is separate from the weather hood.** A "dome" or wind band on an upblast fan keeps rain out; it doesn't necessarily stop reverse airflow when the fan is off. If you don't want warm wet outdoor air drifting back into the room on still days, spec an integral backdraft damper.
- **Curb sizing is rarely a stock match.** Most upblast fan curb caps are 19, 22, or 30 inches — odd existing curb dimensions (e.g., 28 × 28) usually need a curb adapter, not a perfect fit. Specify the adapter on the bid or it shows up as a change order.
- **Stage your fans for variable load.** Two fans on a humidistat with a low/high setpoint — one runs in normal conditions, both kick on at peak — gives you turndown without VFDs and aligns running cost with actual demand.
- **Fix the source before you size the fan.** A leaking heat exchanger or failing steam trap will out-produce any reasonably sized exhaust system. Service the source first; otherwise the new fans are buying you proportionally less than the math suggests.
- **Corrosion is a material-selection problem, not a fan-sizing problem.** Aluminum housing, TEFC sealed motor, stainless fasteners, and coated wheels all cost extra on the PO and pay back in years of service life. Galvanized steel in a steam room is a planned replacement, not a permanent install.

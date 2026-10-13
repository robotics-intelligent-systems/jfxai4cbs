# Transferred platform concepts — JFXAI4CBS

Review: 13 October 2026. Proposed requirements; acceptance evidence pending.

The medical patrol boat migrated from JFXHMS and the modular hydrogen-electric helicopter from JFXAI4SCSS. JFXAI4CBS owns these physical concept baselines; JFXHMS retains clinical/EMS coordination, while JFXAI4SCSS retains satellite simulation. These assets support research into supervised cyberphysical systems, telemetry and digital twins; no native integration or validated aircraft/vessel is claimed.

## Medical patrol boat

[CAD illustration](../../MBSE/CAD/medical-patrol-boat-concept.jpg), [editable specification](../../MBSE/CAS/Drawio/OpenTwin_Medical_Patrol_Boat_High_Level_Requirements.drawio), [shared naval requirements](../../MBSE/CAS/Drawio/OpenTwin_Medical_Fleet_Common_High_Level_Requirements.drawio), [SysML requirement views](../../MBSE/CAS/Drawio/JFXAI4CBS_Patrol_Boat_SysML.drawio), [traceability](patrol-boat-requirements-traceability.csv).

Preserve PAT-01–07 and shared MED-C01–12, acceptance criteria and planned evidence IDs. MED-C remains shared with JFXHMS; this is an applicability copy, not 12 new requirements. The illustrated coastal/river boat includes twin outboards, patient/stretcher space, modular deck, PV, navigation/communications and separate water/waste. No helipad, operating theatre or ICU is depicted. Dashboard values do not define acceptance limits. Clinical records remain under separately governed HMS services; CBS receives authorized asset/mission metadata.

## Modular hydrogen-electric helicopter

[CAD illustration](../../MBSE/CAD/modular-hydrogen-electric-helicopter-concept.jpg), [editable requirements/SysML-style views](../../MBSE/CAS/Drawio/JFXAI4CBS_Hydrogen_Electric_Helicopter_Requirements.drawio), [traceability](helicopter-requirements-traceability.csv).

No corresponding helicopter requirements or SysML model were found in JFXAI4SCSS; its satellite-network Drawio stays there. HEL-01–07 are new proposed IDs grounded in the depicted modular cabin, hydrogen storage, fuel cell, buffer battery, electric drive, aerodynamics and mass/CG studies. Quantitative budgets, tank technology, dimensions, endurance and performance remain to be selected and validated. The illustration does not establish amphibious capability or compatibility with the patrol boat.

## Integration and acceptance

Use stable asset identifiers, versioned configuration/model references, timestamps, quality flags, authenticated interfaces and separate observed/simulated states. Record stale data and tolerate duplicate replay. Supervisory AI proposes interpretations; local vessel/flight authority and clinical decisions remain with their responsible operators. No automatic control interface is introduced by this documentation.

Before acceptance, assign owners and dates, approve configurations and measurable budgets, select model/tool versions, and execute the registered inspection, analysis, demonstration and test procedures. All 26 applicable rows (19 patrol/shared + 7 helicopter) remain proposed. The diagrams use editable native Drawio cells and SysML-style stereotypes; they are conceptual views, not compiled SysML models.

[Migration register and source identities](concept-migration-register.json).

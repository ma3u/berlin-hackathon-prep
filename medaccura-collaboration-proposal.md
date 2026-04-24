# Collaboration proposal — MedAccura × EHDS Integration Hub

**Subject:** EHDS rails for MedAccura — 3-min demo if it's a fit

Tim,

Cold email, respect for your time so I'll keep this to the point.

You built MedAccura: an AI that answers clinical guideline questions at the bedside. I built the **EHDS Integration Hub** ([github.com/ma3u/MinimumViableHealthDataspacev2](https://github.com/ma3u/MinimumViableHealthDataspacev2), live at [ehds.mabu.red](https://ehds.mabu.red)): an integration platform and GraphRAG for the European Health Data Space — Eclipse EDC-V, DSP 2025-1, DCP v1.0, FHIR R4, OMOP CDM, HealthDCAT-AP, EEHRxF, full HDAB approval flow, 1490 tests at 94% coverage, massive-scale synthetic cohorts, live cross-border demo running today between a simulated Berlin Clinic, Amsterdam CRO, and German HDAB.

Technically, the Hub is the same retrieval-and-generation pattern as MedAccura — but over a federated 5-layer health knowledge graph instead of guideline PDFs, with natural-language-to-Cypher traversal across multiple participant graph DBs, live EEHRxF compliance checks, and a researcher-facing query surface. Peer system at a different layer of the data stack, not rails underneath it.

Our two projects look adjacent and non-overlapping to me. You own the clinician-facing UX on top of unstructured PDFs. I own the compliant data-exchange layer that EHDS mandates from 2029 onward. Together they become an **EHDS-native clinical decision-support layer** neither of us can credibly build alone. The category exists on slides — it doesn't exist in running software yet. That window is open for maybe 12 months.

## What I see fitting, specifically

1. **MedAccura's RAG → EEHRxF-grounded answers.** Today MedAccura cites guideline PDFs. Via the Integration Hub's EEHRxF alignment layer, the same answer can cite back to the specific HL7 Europe FHIR profile (Patient Summary, Hospital Discharge, Laboratory Results, ePrescription, Medical Imaging, Rare Disease). A clinician asking about a sepsis protocol sees the guideline passage **plus** the patient's actual discharge summary that triggered the question — in one pane, legally compliant.

2. **Guideline-to-patient join over FHIR R4.** Layer 3 of my graph has 127 Synthea patients with full Encounter / Condition / Observation / MedicationRequest / Procedure history. MedAccura's queries land on real clinical context, not hypothetical. SNOMED CT / ICD-10-CM / RxNorm / LOINC concept edges make the join deterministic.

3. **Secondary-use channel under EHDS Art. 50-51.** MedAccura's query logs are themselves valuable anonymised research signal — which guidelines are consulted most, which conditions are missing coverage, where the guidance lags the real case mix. Running that through the HDAB approval flow in my compliance chain turns "we have useful telemetry" into "we have a compliant secondary-use contribution to EU health research." That's a credible fundraising storyline.

4. **Patient-facing mode (EHDS Art. 3-12).** My `patient` persona already exists — dashboard, `/patient/insights`, consent tracking. MedAccura's engine could power the "what does my discharge summary mean in plain German" layer on top of the patient's own EHDS-accessible records. Primary-use, not secondary-use — a different market with the same engine.

5. **Cross-border demo, ready today.** My demo scenario is Berlin Clinic → Amsterdam CRO → German HDAB. Plug MedAccura in and it becomes a cross-border clinical-AI demo under live EHDS rails. Nobody else in the EU has that running end-to-end.

## Three shapes, ascending commitment

**Shape 1 — Joint demo (low effort, high signal).**
I integrate MedAccura against the `/patient` and `/catalog` endpoints on the live stack at ehds.mabu.red. One recorded 3-minute demo shows a clinician asking a guideline question and getting a cited answer grounded in a real synthetic patient. We both publish it. ~2 weeks of integration work from my side; your side is a read-only API key against my demo data.

**Shape 2 — Co-authored reference (medium commitment).**
Joint article — "MedAccura × EHDS Integration Hub: the first EHDS-native clinical AI reference." Technical deep-dive, your clinical framing, my infrastructure framing. Target publications: HIMSS Europe, Bitkom Digital Health, HL7 Europe. Sets the category definition before anyone else does.

**Shape 3 — Pilot pursuit (high commitment).**
We propose a joint pilot to a Berlin hospital (Charité, Vivantes, or DRK group) or the gematik. MedAccura brings the clinician UX and the doctor-founder credibility. I bring the EHDS-compliant data rails and the infrastructure, plus access to systems-integrator delivery capacity and an EHDS Readiness Advisory offering on the implementation-partner side — which means we can walk in with a credible "pilot → production" story, not just a demo. Pilot scope: one EHDS priority category (I'd suggest Hospital Discharge first — narrowest, highest ROI, maps cleanly to your PDF guideline strength). 90-day MVP, jointly branded.

## What I'm not asking for

- Not asking you to merge code or share IP.
- Not asking you to change the MedAccura roadmap.
- Not pitching you at the Big Berlin Hack this weekend — the rules require brand-new projects, and I respect that.

## Next step

I'm at Delta Campus 25–26 April for the Big Berlin Hack (different project, Wildcard track). Happy to grab 20 minutes of coffee if you're around, otherwise a 30-min call anytime in the next two weeks works.

Either way, the fastest path to "is this real or am I over-fitting a pattern" is 10 minutes on [ehds.mabu.red](https://ehds.mabu.red) with the `clinicuser` and `researcher` personas logged in live.

Matthias Buchhorn-Roth
[github.com/ma3u](https://github.com/ma3u) · matthias.buchhorn@web.de

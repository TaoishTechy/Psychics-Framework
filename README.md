# Psychics Framework
<img width="1168" height="784" alt="image" src="https://github.com/user-attachments/assets/74104384-a576-445f-87e9-ce002107235b" />

**Enhanced Psychics Framework (EPF) v3.1** — Revision R1 of the falsifiable instrumentation and protocol specification for consumer-grade EEG observation of the D³ axes (Precision \(\mathcal{P}\), Boundary \(\mathcal{B}\), Temporal \(\mathcal{T}\)), paired with the open-source **AlienEEG** 18/24-channel high-performance observation instrument.

Ghost Mesh Research Division · Sovereign Hub · Neuro-Quantum Validation Program  
Research Use Only · October 2026 · Spec EPF-3.1 · Companion AlienEEG-EPF v1.0

---

## Overview

The Enhanced Psychics Framework extends the Unified Theory of Degens into an operational observation layer. Cognitive states are coordinates in D³ space. EPF-3.1 binds those coordinates to measurable electrophysiology through a documented open-source EEG acquisition stack, a version-pinned signal-processing pipeline, a five-level amplification ladder, and a blind-scored Channel / Remote-View trial methodology with pre-registered statistics and explicit kill criteria.

Revision R1 fully disposes of the prior 144-point defect report and 96-point enhancement report: re-anchored D³ estimators, sham-controlled ladders, quantified trial-layer isolation, and six validation gates (EP-1 through EP-6).

“Psychic” phenomena are treated as computationally real but metaphysically misinterpreted. Above-chance information transfer, where measured, is attributed to subtle-cue inference, statistical anticipation, and inter-person physiological coupling — not to paranormal reception. Nothing in this repository asserts that consumer EEG demonstrates, amplifies, or validates paranormal ability. This is not medical advice, not a clinical instrument, and not a treatment protocol.

---

## Documentation

All primary specifications live in `/docs`:

| Document | Description |
|----------|-------------|
| [Enhanced_Psychics_Framework_v3.1.pdf](docs/Enhanced_Psychics_Framework_v3.1.pdf) | Current specification (Revision R1). Full disposition of defect and enhancement reports; six validation gates. |
| [Enhanced_Psychics_Framework_v3.0.pdf](docs/Enhanced_Psychics_Framework_v3.0.pdf) | Prior release for lineage reference. |
| [AlienEEG_EPF_Instrument_Blueprint_v1.0.pdf](docs/AlienEEG_EPF_Instrument_Blueprint_v1.0.pdf) | Companion instrumentation blueprint: verified three-chip ADS1299 architecture, EPF-aligned montage, firmware pipeline, and bench-level binding to gates EP-1–EP-6. |
| [AlienEEG_Complete_Build_Guide.pdf](docs/AlienEEG_Complete_Build_Guide.pdf) | Detailed hardware build guide, BOM, assembly sequence, and software specification for the AlienEEG system. |
| [Blueprint for AlienEEG.md](docs/Blueprint%20for%20AlienEEG.md) | Markdown companion covering architecture, montage mapping, firmware, integration, and open-source deliverables. |

---

## AlienEEG Observation Instrument

AlienEEG-EPF is the reference open-source, battery-isolated EEG stack for EPF-3.1.

- **Channels**: 18 simultaneous (24 hardware via 3× ADS1299 daisy-chain)
- **ADC**: 24-bit delta-sigma
- **Sampling**: 250 Hz default (500 Hz optional)
- **Wireless**: BLE 5.0 (nRF52832)
- **Host interface**: LSL outlet → EPF session JSON (epf3.session/v1)
- **Montage**: Covers and extends the EPF core sites (Fp1/Fp2, Fz, Cz, C3/C4, Pz, Oz) plus expansion for coherence, EMG screening, and dual-headset PLV

The design uses true simultaneous sampling, driven cable shields, per-channel impedance/lead-off detection, and a FreeRTOS + CMSIS-DSP firmware path. It supplies the real-time metrics required by the amplification ladder and dual-headset protocols. Bench tests and biological validation are specified before human use. The instrument is strictly passive (no current injection) and remains subordinate to the EPF kill criteria.

---

## Core Architecture (EPF-3.1)

State and observation layers:

\[
\Psi(t) = F\bigl(\mathcal{P}(t),\ \mathcal{B}(t),\ \mathcal{T}(t)\bigr) + \xi(t)
\]

\[
d(t) = h\bigl(\Psi(t)\bigr) + \varepsilon(t)
\]

Estimators are z-scored against operator-specific baselines and re-anchored in Revision R1. The five-level ladder trains a reception posture (high-but-stable Precision, moderately softened Boundary, balanced Temporal orientation) via neurofeedback. Channel and Remote-View sessions are operationally defined by estimator bands and scored under sealed, blind conditions with fixed-\(N\) aggregation.

### Validation Gates

| ID | Focus | Notes |
|----|-------|-------|
| EP-1 | Estimator reliability (ICC) | Test-retest of \(\hat{\mathcal{P}}, \hat{\mathcal{B}}, \hat{\mathcal{T}}\) |
| EP-2 | L2 SMR efficacy | Sham-controlled |
| EP-3 | Dyadic synchrony | Alpha-PLV lift under blinding |
| EP-4 | Blind transfer | Aggregate hit performance, fixed \(N\) |
| EP-5 / EP-6 | Additional gates (R1) | Isolation, sham, and measurement enhancements |

Each gate maps to a named retirement. A null result is a clean, publishable outcome. Registration precedes data collection; thresholds may only tighten within a registered run.

---

## Safety and Ethics

- Battery isolation from mains is mandatory.
- Electrode path is passive only.
- Axis-keyed contraindications and self-screening apply.
- Session-length and load caps are enforced.
- Neural data remain local by default; sharing is opt-in and anonymized.
- No commercial packaging of unproven claims while in falsifiable mode.
- Crisis referral language is present; the framework offers no clinical intervention.

Full safety, ethics, and load-limit language is in the EPF-3.1 specification.

---

## Status

EPF-3.1 (Revision R1) and the AlienEEG-EPF v1.0 companion blueprint are the current reference documents. The repository hosts the specifications, build guides, and integration notes. Hardware schematics, firmware, and pipeline code will be added under version control as the open-source deliverables mature.

---

## Citation

```
Enhanced Psychics Framework v3.1 (Revision R1) & AlienEEG-EPF Observation Instrument v1.0,
Ghost Mesh Research Division, 2026.
https://github.com/TaoishTechy/Psychics-Framework
```

---

**From chaos, through computation, toward evidence.**  
A framework that cannot name the observation that would kill it has already failed; v3.1 names its gates.

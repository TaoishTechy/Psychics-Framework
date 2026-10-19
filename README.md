# Psychics Framework
<img width="1168" height="784" alt="image" src="https://github.com/user-attachments/assets/74104384-a576-445f-87e9-ce002107235b" />

**Enhanced Psychics Framework (EPF) v3.1** — a falsifiable instrumentation and protocol specification for consumer-grade EEG observation of the D³ axes (Precision \(\mathcal{P}\), Boundary \(\mathcal{B}\), Temporal \(\mathcal{T}\)), paired with the open-source **AlienEEG** 18/24-channel high-performance headset as its reference acquisition layer.

Ghost Mesh Research Division · Sovereign Hub · Neuro-Quantum Validation Program  
Research Use Only · October 2026

---

## Overview

The Enhanced Psychics Framework extends the Unified Theory of Degens (UTD) into an operational observation layer. Cognitive states are coordinates in D³ space. EPF-3.1 binds those coordinates to measurable electrophysiology through:

- A documented DIY / open-source EEG acquisition stack (AlienEEG)
- A version-pinned signal-processing pipeline that produces \(\hat{\mathcal{P}}\), \(\hat{\mathcal{B}}\), \(\hat{\mathcal{T}}\)
- A five-level hyper-correlation amplification ladder (neurofeedback + structured sessions)
- A blind-scored Channel / Remote-View trial methodology with pre-registered statistics and explicit kill criteria

“Psychic” phenomena are treated as computationally real but metaphysically misinterpreted: above-chance information transfer, where measured, is attributed to subtle-cue inference, statistical anticipation, and inter-person physiological coupling — not to paranormal reception. Nothing in this repository asserts that consumer EEG demonstrates, amplifies, or validates paranormal ability. This is not medical advice, not a clinical instrument, and not a treatment protocol.

---

## AlienEEG Headset

AlienEEG is the reference observation instrument for EPF-3.1: an open-source, battery-isolated, 18-channel (expandable to 24) simultaneous EEG system built around three daisy-chained ADS1299 analog front ends.

### Key Specifications

| Parameter              | Value                                      |
|------------------------|--------------------------------------------|
| Channels               | 18 simultaneous (24 hardware)              |
| ADC                    | 24-bit delta-sigma (ADS1299 × 3)           |
| Input Noise            | ~0.25 μVrms typical (gain = 24, 250 SPS)   |
| Sampling Rate          | 250 Hz default / 500 Hz optional           |
| CMRR                   | >100 dB typical (layout-dependent)         |
| Wireless               | BLE 5.0 (nRF52832)                         |
| Battery Life           | 20–25 hours (1000 mAh LiPo)                |
| PCB                    | 4-layer ENIG, star-ground, driven shield   |
| Host Interface         | LSL outlet → EPF session JSON              |

The design uses true simultaneous sampling (no analog multiplexing), driven cable shields, per-channel impedance/lead-off detection, and a FreeRTOS + CMSIS-DSP firmware stack. It maps directly onto the EPF montage (Fp1/Fp2, Fz, Cz, C3/C4, Pz, Oz + expansion sites) and supplies the real-time metrics required by the amplification ladder and dual-headset PLV protocols.

See `/hardware` for schematics, BOM, assembly sequence, firmware, and validation procedures.

---

## Framework Architecture (EPF-3.1)

### Core Equations

State and observation layers:

\[
\Psi(t) = F\bigl(\mathcal{P}(t),\ \mathcal{B}(t),\ \mathcal{T}(t)\bigr) + \xi(t)
\]

\[
d(t) = h\bigl(\Psi(t)\bigr) + \varepsilon(t)
\]

\[
(\hat{\mathcal{P}},\ \hat{\mathcal{B}},\ \hat{\mathcal{T}}) = \arg\min \|\ d(t) - h(F(\mathcal{P},\mathcal{B},\mathcal{T}))\ \|_2 + \lambda R
\]

Estimators (z-scored against operator baseline):

\[
\hat{\mathcal{P}} = z\bigl[\log(\Gamma_{30-50}/\alpha_{8-12})\bigr] + 0.5\cdot z[\mathrm{MMN}]
\]

\[
\hat{\mathcal{B}} = (C_{\mathrm{int}} - C_{\mathrm{ext}}) / (C_{\mathrm{int}} + C_{\mathrm{ext}})
\]

\[
\hat{\mathcal{T}} = z[\text{slope of Fm}\theta_{Fz}\text{ across delay-discounting}]
\]

### Amplification Ladder

| Level | Protocol                          | Primary Target                  |
|-------|-----------------------------------|---------------------------------|
| L1    | Baseline mapping + MMN / discounting | Stable \(\hat{\mathcal{P}},\hat{\mathcal{B}},\hat{\mathcal{T}}\) |
| L2    | SMR (12–15 Hz) up-training        | Precision stabilization         |
| L3    | Alpha–theta crossover             | Controlled boundary modulation  |
| L4    | Dyadic coherence lock             | Alpha-PLV lift                  |
| L5    | Blind transfer trials             | HCI / sealed Channel-RV battery |

Exit criteria, load accounting, and mechanical stop rules are defined in the specification. Skipping levels is prohibited.

### Channel / Remote-View Layer

Operationally defined by estimator bands and blind judging. Free-response and forced-choice batteries use sealed scoring, cryptographic target selection, and fixed-\(N\) aggregation (Stouffer \(z_{\mathrm{agg}}\)). Under strict sensory isolation the honest base-rate expectation is chance performance. A null result at \(N=100\) is a clean, publishable outcome.

---

## Validation Gates (Falsifiability)

| ID   | Hypothesis                              | Gate                     |
|------|-----------------------------------------|--------------------------|
| EP-1 | Estimator test-retest ICC               | ICC ≥ 0.6 per axis       |
| EP-2 | L2 SMR neurofeedback vs sham            | \(d \ge 0.4\)            |
| EP-3 | Dyadic alpha-PLV lift                   | ≥ 2 SD, corrected        |
| EP-4 | Blind transfer aggregate                | \(z_{\mathrm{agg}} \ge +1.64\) at \(N=100\) |

Each gate maps to a named retirement. Failure retires the corresponding layer without altering the underlying axis algebra. Registration precedes data collection; thresholds may only tighten within a registered run.

---

## Repository Structure

```
Psychics-Framework/
├── docs/                  # EPF-3.1 specification, lineage, safety, ethics
├── hardware/              # AlienEEG schematics, BOM, assembly, firmware
│   ├── kicad/
│   ├── firmware/          # STM32 + nRF52
│   └── validation/
├── software/
│   ├── pipeline/          # Signal processing, estimators, session JSON
│   ├── bridge/            # LSL → Sovereign Hub
│   └── dashboard/         # PSP-144 integration hooks
├── protocols/             # L1–L5 ladder, Channel/RV trial battery
├── validation/            # EP-1–EP-4 pre-registration templates
└── examples/              # Quickstart sessions and notebooks
```

---

## Quick Start

1. Review the safety and contraindications section before any hardware use.
2. Assemble or acquire an AlienEEG (or compatible Tier-2) headset.
3. Flash firmware and verify bench tests (noise floor, CMRR, lead-off).
4. Run L1 baseline mapping to establish operator-specific z-score norms.
5. Stream via LSL into the local bridge; confirm session JSON emission.
6. Progress through the ladder only after meeting exit criteria.
7. For Channel/RV work, follow the sealed, blind protocol exactly; register EP-4 before collecting trial data.

Detailed build, firmware, and protocol instructions are in `/hardware` and `/docs`.

---

## Safety and Ethics

- Battery isolation from mains is mandatory during recording.
- Electrode path is passive only.
- Axis-keyed contraindications (psychosis-spectrum history, severe dissociation, acute sleep deprivation, minors, etc.) apply.
- Self-screen and recovery-block logging are required.
- Neural data remain local by default; sharing is opt-in and anonymized.
- No commercial packaging of unproven claims while the framework is in falsifiable mode.
- Crisis referral language is present; the system provides no clinical intervention.

---

## License

Hardware and firmware: CERN-OHL-S or equivalent open hardware license (to be finalized).  
Specification and documentation: CC BY 4.0.  
Software: MIT.

---

## Citation

```
Enhanced Psychics Framework v3.1 & AlienEEG Observation Instrument,
Ghost Mesh Research Division, 2026.
https://github.com/TaoishTechy/Psychics-Framework
```

---

**From chaos, through computation, toward evidence.**  
A framework that cannot name the observation that would kill it has already failed; v3.1 names four.

**AlienEEG-EPF: Open-Source 18/24-Channel Observation Instrument for the Enhanced Psychics Framework v3.0**

**Complete Blueprint, Hardware Specification, Firmware Architecture, and Integration Reference**  
Research Use Only · Compatible with EPF-3.0 (PSP-144 NQVP) · Falsifiable Instrumentation Layer

### 1. Design Charter and Scope

This blueprint rewrites the corrected AlienEEG architecture as the reference observation instrument for EPF-3.0. It supplies a reproducible, battery-isolated, open-source EEG stack whose estimators \(\hat{\mathcal{P}}\), \(\hat{\mathcal{B}}\), and \(\hat{\mathcal{T}}\) map directly onto the D3-axis definitions, montage, signal-processing pipeline, amplification ladder, and blind Channel/Remote-View protocol of EPF-3.0.

The instrument remains strictly passive (no current injection). All claims are bound to the EPF-3.0 kill criteria (EP-1 through EP-4). “Psychic” phenomena continue to be treated as subtle-cue inference, statistical anticipation, and inter-person physiological coupling under the framework’s expected-null stance.

### 2. Verified System Architecture

Three ADS1299 devices in native SPI daisy-chain mode yield 24 simultaneous channels. Eighteen channels are populated for the EPF montage; the remaining six serve as spares, EOG/EMG references, or expansion.

**Signal chain**  
Dry/saline/gold electrodes → ESD protection → 3× ADS1299 (daisy-chained, single BIAS from chip 1) → STM32F411CEU6 (FreeRTOS, CMSIS-DSP) → nRF52832 (BLE 5.0, 2M PHY, NUS) → host (LSL outlet → EPF session JSON / Sovereign Hub bridge).

Daisy-chain configuration follows the ADS1299 datasheet: DOUT of chip \(n\) to DAISY_IN of chip \(n+1\); shared SCLK/DIN/CS; only chip 1 drives BIASOUT. This eliminates analog multiplexing artifacts and preserves phase coherence required for PLV and coherence estimators.

### 3. Bill of Materials (Corrected, EPF-Aligned)

Core AFE: 3× ADS1299IPAG. MCU: STM32F411CEU6 + MCP23017 GPIO expander. Radio: MDBT42Q (nRF52832, BLE 5.0). Power: MCP73831 charger, TPS61023 boost, dual MIC5219 LDOs, REF3325 reference. Enclosure and electrodes sized for the EPF eight-site core montage plus expansion sites. Approximate BOM at qty-100 pricing remains in the low-to-mid $90 range; cost per active channel is competitive with research-grade consumer systems while exceeding the EPF Tier-2 minimum.

PCB: 4-layer ENIG, star-ground analog/digital separation, guard rings on analog inputs, antenna keep-out, and driven-shield routing for cable bundles.

### 4. EPF-3.0 Montage Mapping

The 18-channel array covers and extends the EPF Chapter 3 montage:

- Core estimator sites: Fp1, Fp2, Fz, Cz, C3, C4, Pz, Oz (plus neighbors for P3/P4 derivation).  
- Additional sites: T7/T8 or FT7/FT8 for source-monitoring and auditory features; O1/O2 for posterior alpha; spare channels configurable as bipolar EMG (jaw/neck) or EOG for ICA/ASR.  
- Reference/bias: linked mastoid (A1/A2) or SRB; BIASOUT drives cable shields.

This density improves the reliability of \(\hat{\mathcal{B}}\) (intra- vs inter-network coherence) and supports the EMG screen required before any gamma-derived \(\hat{\mathcal{P}}\) is logged.

### 5. Firmware and On-Device Processing

FreeRTOS tasks implement the EPF pipeline requirements:

- High-priority DRDY-triggered DMA SPI read of the full daisy-chain frame.  
- On-device IIR notch (50/60 Hz + harmonics), 0.5–50 Hz bandpass, and lightweight artifact flags.  
- Optional on-device band-power streaming (Welch-style) for low-bandwidth neurofeedback of SMR, alpha, and theta.  
- Impedance/lead-off polling logged into the session record.  
- BLE packet format carries 24-bit samples, sequence numbers, impedance summary, artifact bits, and battery state, with overhead budgeted for 2M PHY.

PC-side (or hub-side) processing completes ICA, coherence/PLV, MMN extraction, and the regularized inverse that yields \(\hat{\mathcal{P}}\), \(\hat{\mathcal{B}}\), \(\hat{\mathcal{T}}\) according to EPF Equations 3.1–3.3. All pipeline parameters are version-pinned and written into the EPF session JSON schema.

### 6. Integration with EPF-3.0 and Sovereign Hub

- Native LSL outlet for real-time D3 estimates and raw streams.  
- Session JSON (epf3.session/v1) posted to the local bridge, including impedance vector, band powers, coherence/PLV, HCI, safety flags, and pipeline version.  
- Dual-headset support with photonic or LSL timestamp alignment for L4 dyadic PLV and EP-3.  
- Dashboard hooks bind live \(\hat{\mathcal{P}}\), \(\hat{\mathcal{B}}\), \(\hat{\mathcal{T}}\) to the existing axis monitors; Crucible progress tracks L1–L5 exit criteria.  
- Local-only storage by default; sharing is explicit and anonymized.

### 7. Amplification Ladder and Protocol Support

The instrument supplies the real-time metrics required by the five-level ladder:

- L1 baselines and MMN/oddball blocks.  
- L2 SMR (12–15 Hz) up-training at Cz with theta monitoring.  
- L3 alpha–theta crossover for controlled boundary modulation.  
- L4 dual-headset alpha-PLV.  
- L5 sealed trial logging with cryptographic target/transcript hashes.

Load accounting (Eq. 6.1) and recovery-block flags are exposed as safety telemetry.

### 8. Validation, Safety, and Falsifiability

Bench tests enforce noise floor, CMRR, crosstalk, and lead-off performance before human use. Biological checks include posterior alpha modulation and frontal blink rejection.  

The design is explicitly subordinate to EPF kill criteria: estimator ICC (EP-1), sham-controlled SMR efficacy (EP-2), dyadic PLV lift (EP-3), and blind transfer aggregate (EP-4). Failure of any gate retires the corresponding layer without affecting the underlying axis algebra.  

Safety constraints match Chapter 9: battery isolation from mains, passive electrodes only, axis-keyed contraindications, session-length caps, and mechanical stop rules. No medical claims are made.

### 9. Open-Source Deliverables

- KiCad schematics and PCB (4-layer, star-ground, driven shield).  
- STM32 + nRF52 firmware with FreeRTOS and CMSIS-DSP.  
- Python LSL bridge, session JSON emitter, and MNE-compatible importer.  
- Validation notebooks for EP-1–EP-4 gates.  
- Full BOM, assembly sequence, and register map.

This rewritten blueprint supplies a single, reproducible observation layer that satisfies the instrumentation, estimator, protocol, safety, and falsifiability requirements of Enhanced Psychics Framework v3.0 while remaining fully open-source and research-use-only.

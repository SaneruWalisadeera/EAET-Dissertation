# Entanglement-Anchored Evidence Timestamping (EAET)
### A Post-Quantum Prototype for Real-Time Digital Forensics Integrity Verification

**Author:** Saneru Walisadeera (w032674o)  
**Institution:** Staffordshire University, Department of Computer Science  
**Email:** w032674o@student.staffs.ac.uk  
**Submission:** Final Dissertation, 2026

---

## Overview

EAET is a hybrid quantum-classical prototype that addresses a critical gap in post-quantum digital forensics. Existing blockchain-based forensic systems detect tampering only through post-hoc hash comparison and depend on classical cryptographic mechanisms that quantum computing threatens to break. EAET replaces this reactive model with a physically grounded verification signal derived from entangled photon correlations.

The SHA-256 hash of a digital evidence file is converted into a deterministic measurement recipe. Pairs of entangled photons are distributed to two measurement nodes that both follow this recipe. Their paired outcomes produce a correlation score C. Under authentic conditions C stays at or above the acceptance threshold of 0.9. Any interference collapses the entanglement and causes a measurable drop in C, generating a real-time tamper signal. Every verification event is anchored to a proof-of-work blockchain audit ledger for chain-of-custody reporting.

---

## Simulation Results Summary

| Scenario | Finding |
|----------|---------|
| S0: Integration test | Pipeline works end-to-end; chain validates |
| S1: Real-time detection | 100% detection rate across 4 attack onsets |
| S2: Photon loss robustness | Discriminative window preserved up to 50% loss |
| S3: Combined stress | 100% tampered rejection across full noise/loss grid |
| S4: Latency comparison | EAET fastest at 66ms (tampered, deployment-projected) |
| S5: ROC analysis | AUC = 1.0000; robust threshold range 0.34–0.95 |
| S6: Multi-attack modes | 100% detection for Y/X/Z attacks; 25% for partial 25% |

---

## How to Run

### Google Colab (recommended)

1. Open [Google Colab](https://colab.research.google.com)
2. Click **File → Upload notebook** and upload `EAET_Dissertation.ipynb`
3. Run the first cell to install dependencies
4. Restart the runtime when prompted, then run all remaining cells
5. When prompted, upload any evidence file (PDF, image, text — any file works)

### Local Python environment

```bash
pip install qiskit qiskit-aer matplotlib numpy
jupyter notebook EAET_Dissertation.ipynb
```

For local runs, the notebook automatically uses a synthetic test file instead of requiring an upload.

---

## What the Notebook Produces

**Figures (saved to `/figures/`):**

| Figure | Description |
|--------|-------------|
| Figure 05 | Cumulative correlation trajectories (authentic vs 4 tamper onsets) |
| Figure 06 | Step-wise correlation — immediate collapse at attack onset |
| Figure 07 | Distribution of first detection step across 30 trials |
| Figure 08 | Detection latency by attack onset |
| Figure 09 | Photon loss robustness (dual panel: correlation + decision rates) |
| Figure 10 | Discriminative window across multiple threshold values |
| Figure 11 | Combined noise/loss heatmap (correlation) |
| Figure 12 | Discriminative gap heatmap |
| Figure 13 | Decision rate heatmap (clean accept / tampered reject) |
| Figure 14 | Verification latency comparison (simulation + deployment-projected) |
| Figure 15 | Detection step comparison across methods |
| Figure 16 | ROC curve with AUC annotation |
| Figure 17 | Correlation distributions (authentic vs tampered, no overlap) |
| Figure 18 | Decision rate sensitivity across threshold sweep |
| Figure 19 | Detection rate by attack mode |
| Figure 20 | Cumulative trajectories across 7 attack modes |
| Figure 21 | Partial attack sensitivity envelope |

**Results (saved to `/results/`):**
- `s1_realtime_detection.json`
- `s2_photon_loss.json`
- `s6_attack_modes.json`
- `eaet_final_audit_chain.json` — full blockchain audit ledger

---

## Technical Stack

| Component | Tool / Library |
|-----------|---------------|
| Quantum simulation | IBM Qiskit + Qiskit Aer |
| Quantum circuits | Bell state (Hadamard + CNOT) |
| Noise modelling | Depolarising error + readout error |
| Photon loss | Coincidence-count reduction model |
| Blockchain ledger | Custom proof-of-work (difficulty 4) |
| Evidence hashing | SHA-256 (streaming, 4096-byte chunks) |
| Language | Python 3.10+ |
| Visualisation | Matplotlib |

---

## Repository Structure

```
EAET_Project/
├── EAET_Dissertation.ipynb    # Main Google Colab notebook (all experiments)
├── README.md                  # This file
├── figures/                   # Generated graphs (created on run)
└── results/                   # JSON audit records (created on run)
```

---

## Important Notes

1. **Simulation only:** All results are simulated behavioural indicators produced by IBM Qiskit Aer. Physical quantum hardware would eliminate the simulator overhead visible in wall-clock latency figures. Deployment-projected latency uses 2ms per measurement step, consistent with entanglement distribution rates demonstrated by Tang et al. (2023) and Han et al. (2025).

2. **Synthetic test data:** When running locally (outside Colab), the notebook uses a synthetic byte sequence as the evidence file. This is valid because EAET operates on the SHA-256 hash of the artefact; the verification pipeline is agnostic to file format or content.

3. **Reproducibility:** A fixed random seed (42) is used throughout. Every trial uses a deterministic seed derived from the trial number, ensuring all results are fully reproducible.

4. **Threshold calibration:** The default acceptance threshold of 0.9 was selected based on simulation conditions at zero photon loss. Deployment in environments with higher noise or loss requires recalibration. Scenario S2 maps the operational envelope for different threshold values.

---

## References (Key)

- Parida et al. (2023). Post-quantum distributed ledger technology. *Scientific Reports*, 13(1).
- Tang et al. (2023). 75 km-fiber quantum clock synchronization. *EPJ Quantum Technology*, 10(1).
- Han et al. (2025). Quantum clock synchronization with silicon-chip entangled photon source. *EPJ Quantum Technology*, 12(1).
- Li et al. (2025). High-dimensional entanglement witnessed by correlations. *npj Quantum Information*, 11(1).
- Kebande, V.R. (2025). Quantum computing as a transformative force for IIoT forensics. *WIREs Forensic Science*. DOI: 10.1002/wfs2.70013

---

*Staffordshire University — Department of Computer Science — 2026*

# Low-Voltage FGMOS Synthetic Inductor — LTspice Simulation (180 nm CMOS)

Design and simulation of a tunable synthetic inductor using Floating-Gate MOS (FGMOS) transistors in a MOS-C topology. Operates at ±0.5V supply — well below conventional analog circuit supply requirements. Simulated in LTspice using a 180 nm CMOS process design kit.

---

## Motivation

Physical inductors are bulky, lossy, and incompatible with on-chip integration at low frequencies. Synthetic (active) inductors replace them with transistor-based circuits that emulate inductive behaviour — enabling compact, tunable, fully-integrated analog designs.

Conventional synthetic inductors use standard MOSFET topologies, but suffer from limited tunability and poor performance at low supply voltages. This project replaces conventional MOSFETs with **Floating-Gate MOS (FGMOS)** transistors, which offer:

- Electronically programmable threshold voltage via control voltage Vc
- Enhanced transconductance efficiency at low supply voltages
- Tunable inductance and quality factor without additional circuitry

**Target applications:** RF front-ends, on-chip LNA matching networks, energy-efficient biosignal acquisition front-ends, band-pass filter implementations.

---

## Circuit Topology

**Base topology:** MOS-C grounded active inductor  
**Reference:** A. Yesil, E. Yuce, and S. Minaei, "MOSFET-C-Based Grounded Active Inductors with Electronically Tunable Properties," *International Journal of RF and Microwave Computer-Aided Engineering*, vol. 30, no. 8, p. e22274, 2020.

**Key modification:** Standard MOSFETs replaced with FGMOS transistors, enabling threshold voltage tuning via a programmable control voltage Vc — making both inductance value and quality factor electronically adjustable.

---

## Simulation Setup

| Parameter | Value |
|-----------|-------|
| Simulation tool | LTspice |
| CMOS process | 180 nm PDK |
| Supply voltage | VDD = \|VSS\| = 0.5V |
| Control voltage (baseline) | Vc = 0.5V |
| Grounded capacitor | C = 10 pF |
| Analysis type | AC sweep (10kHz – 1GHz) |

---

## Results

### 1. Inductance vs Frequency

![Inductance](screenshots/inductance.png)

- Flat inductive behaviour observed from **10kHz up to ~10MHz**
- Self-resonance occurs around **15–20MHz** — characteristic of active inductor topologies
- Stable inductance plateau confirms correct synthetic inductor operation in the target frequency band

---

### 2. Impedance vs Frequency

![Impedance](screenshots/impedance.png)

- Impedance rises with frequency in the inductive region — consistent with Z = jωL behaviour
- Peak impedance at self-resonant frequency (~20MHz) reaches ~100dB
- Confirms the circuit presents inductive impedance across the RF analog band

---

### 3. Band-Pass Filter — Gain Response

![BPF Gain](screenshots/bpf_gain.png)

The synthetic inductor was used to implement a **band-pass filter** by combining it with a load capacitor. Results:

- Centre frequency: **~3MHz**
- Peak gain: **~0dB**
- Selectivity: clean roll-off on both sides confirming BPF behaviour
- Demonstrates a direct application of the synthetic inductor in a functional analog filter

---

## Key Advantages of FGMOS Implementation

| Feature | Conventional MOSFET | FGMOS |
|---------|-------------------|-------|
| Tunability | Fixed (requires external bias circuit) | Electronic — via control voltage Vc |
| Supply voltage | Typically >1V | ±0.5V demonstrated |
| Transconductance efficiency | Standard | Enhanced |
| Device count | Higher | Reduced |

---

## What I Learned

- How floating-gate transistors enable threshold voltage programmability and why this matters for low-voltage analog design
- The relationship between transconductance (gm) and synthetic inductance value: L = C/gm²
- Why active inductors have a self-resonant frequency and how it limits usable bandwidth
- How to characterise an active inductor — impedance sweep, inductance extraction, Q factor analysis
- Practical application of a synthetic inductor in a band-pass filter topology

---

## Files

| File | Description |
|------|-------------|
| `*.asc` | LTspice schematic files |
| `screenshots/inductance.png` | Inductance vs frequency plot |
| `screenshots/impedance.png` | Impedance vs frequency plot |
| `screenshots/bpf_gain.png` | Band-pass filter gain response |
| `report.pdf` | Full project report (unpublished) |
| `README.md` | This file |

---

## References

- A. Yesil, E. Yuce, and S. Minaei, "MOSFET-C-Based Grounded Active Inductors with Electronically Tunable Properties," *Int. J. RF Microw. Comput. Aided Eng.*, vol. 30, no. 8, p. e22274, 2020.
- 180 nm CMOS Process Design Kit — LTspice

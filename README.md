# CO-VLFF: Power-Delay Optimization of Low-Power Flip-Flops Using Transistor Sizing for Data-Aware IoT Shift Registers

**VConnecTech Engineering Marathon 2026** | **Team Name:** NanoWatt | **Team ID:** `M2026-124`  
**Institution:** Department of Electronics & Communication Engineering, Chennai Institute of Technology, Chennai, India

---

## Overview

`CO-VLFF (V3)` is a topology-preserving, contention-optimized transistor sizing methodology applied to the 19-transistor Voltage-Latched Flip-Flop (VLFF) in **180 nm CMOS (`gpdk180`)** at **1.8 V, 125 MHz**, targeting battery-constrained **8-bit Edge IoT SIPO shift register buffers**.

Without adding any extra transistors, feedback diodes, or multi-phase clocks, targeted transistor skewing suppresses internal node `L2` pull-down contention, cuts total active gate width by **48.2%**, and reduces 8-bit SIPO system power by **53.7%** and simultaneous peak supply current by **40.0%**.

## Key Round 1 Verified Results (`gpdk180`, 1.8 V, 125 MHz, TT, 27 °C)

### Single-Cell Benchmark (`19T`, `C_L = 10 fF`)
| Metric | VLFF (`V0` Baseline) | `V1` Diagnostic | `CO-VLFF (V3)` | Improvement (`V0 → V3`) |
| :--- | :---: | :---: | :---: | :---: |
| **Power @ 80% DA** | 28.66 µW | 25.03 µW | **13.92 µW** | **−51.4%** |
| **Power @ 50% DA** | 20.17 µW | — | **9.872 µW** | **−51.1%** |
| **Power @ 20% DA** | 8.14 µW | — | **3.972 µW** | **−51.2%** |
| **Idle Rail Power @ 0% DA** | 135.1 nW | — | **77.80 nW** | **−42.4%** |
| **Peak Supply Current (`I_peak`)** | 681.0 µA | 764.2 µA (+12.2%) | **517.6 µA** | **−24.0%** |
| **Avg Clock-to-Q (`t_CQ,avg`)** | 197.4 ps | 156.0 ps | **147.1 ps** | **−25.5%** |
| **`PDP_avg` @ 80% DA** | 5.66 fJ | 3.90 fJ | **2.05 fJ** | **−63.8%** |
| **Active Gate Width (`ΣW`)** | 38.0 µm | >39.5 µm | **19.7 µm** | **−48.2%** |

### Four-Corner Timing & Retention Sign-Off (`CO-VLFF V3`, 10% `t_CQ` Rule, 25 ps Step)
* **Nominal `t_CQ,LH` / `t_CQ,HL`:** `129.6 ps` / `164.6 ps`
* **Setup Time (`0 → 1` / `1 → 0`):** `~203 ps` (`225 ps` grid) / `~351 ps` (`375 ps` grid)
* **Hold Time (`D = 1` / `D = 0`):** `< −300 ps` / `+25 ps` (`t_CQ,min > t_hold` by `> 100 ps` — race-free)
* **State Retention (`pw_setup = 13 ns`):** Flat `1.8 V` on consecutive `'1'` bits with zero glitch or false reset

### 8-Bit SIPO Shift Register Benchmark (`152T`, 50% DA `'1100'`, 160 ns, `C_L = 10 fF` on `Q7`)
| System Metric | `SIPO_8bit_VLFF (V0)` | `SIPO_8bit_CO_VLFF (V3)` | Improvement |
| :--- | :---: | :---: | :---: |
| **Total Average Power (`P_avg`)** | 136.2 µW | **63.05 µW** (`7.88 µW/bit`) | **−53.7%** |
| **Energy per Clock Cycle** | 1.09 pJ/cycle | **0.50 pJ/cycle** | **−53.7%** |
| **Peak Supply Current (`I_peak`)** | 2.823 mA | **1.693 mA** | **−40.0%** |
| **Total Active Gate Width (`ΣW`)** | 304.0 µm | **157.6 µm** | **−48.2%** |

---

## Repository Structure

```text
├── README.md
├── cadence/
│   ├── transistor_sizing.csv      # Complete 19T widths (V0 vs. V3, L = 180 nm)
│   └── viva_expressions.txt       # ADE L stimuli & ViVA Calculator expressions
├── docs/
│   ├── M2026-124_NanoWatt_DPR.pdf # IEEE Detailed Project Report
│   └── Team_NanoWatt_Slides.pdf   # VConnecTech Submission Deck
├── figures/                       # Virtuoso schematics, ViVA proofs & 300-DPI charts
└── notebooks/
    └── CO_VLFF.ipynb              # Lab log & benchmark notebook

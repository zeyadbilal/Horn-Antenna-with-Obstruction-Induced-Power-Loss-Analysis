# 📡 Horn Antenna Design & Obstruction-Induced Power Loss Analysis

> **Course:** Electromagnetic Waves — 3rd Year Communications Engineering (2025–2026)  
> **Institution:** Benha University, Shoubra Faculty of Engineering  
> **Supervised by:** Dr. Gehan Sami  
> **Team:** Zeyad Bilal (B.N:17) · Kerolos Hani (B.N:23) · Jana Ahmed (B.N:9) · Jehad Amrou (B.N:10)

---

## 📌 Project Overview

This project involves the full design, simulation, and power loss analysis of a **rectangular pyramidal horn antenna** using **Ansys HFSS**. The simulation examines how the antenna radiates electromagnetic energy and how introducing material obstacles in front of the aperture affects power distribution and efficiency.

Two main scenarios are studied:
1. **Free-space radiation** — antenna gain, S11 return loss, radiation pattern
2. **Obstruction-induced power loss** — power absorbed by a lossy dielectric (FR4_epoxy) and surface loss on the metallic horn walls

---

## 🛠️ Tools & Software

| Tool | Purpose |
|------|---------|
| Ansys HFSS | Full-wave 3D EM simulation |
| Fields Calculator | Power loss integration |
| Far-Field Radiation Setup | Radiation pattern & gain |

---

## 📐 Antenna Geometry

| Parameter | Value |
|-----------|-------|
| Waveguide dimensions | 1.59 in × 0.795 in × 1 in |
| Aperture size | 7.95 in × 3.975 in |
| Radiation box | 8.8 in × 4.4 in × 15 in |
| Operating frequency | 5 GHz |
| Excitation | Wave Port (TE10 mode) |
| Boundary | Perfect E (PEC walls) |
| Max solver passes | 25 |

---

## 🧪 Part 1 — Horn Antenna HFSS Simulation

### Steps Summary
1. Draw waveguide box and aperture rectangle in HFSS (units: inches)
2. Connect faces using `Modeler → Surface → Connect`
3. Uncover top/waveguide faces to form the open-flared horn
4. Unite geometry with `Modeler → Boolean → Unite`
5. Assign **Wave Port** excitation at the waveguide input face with integration line
6. Assign **Perfect E** boundary to the horn body
7. Add **Radiation Box** with radiation boundary
8. Set up solution (5 GHz, 25 passes) and frequency sweep (4–8 GHz)
9. Insert **Infinite Sphere** far-field setup (φ: 0°→180°, θ: -180°→180°, step: 1°)
10. Run simulation and extract results

### Results Obtained
- `dB(S(1,1))` — Return loss vs. frequency (rectangular plot)
- `re(Z(1,1))` — Real part of input impedance
- **3D Polar Plot** — Far-field gain pattern
- **Antenna Parameters** via `HFSS → Radiation → Compute Antenna/Max Parameters`

| Parameter | Simulated Value |
|-----------|----------------|
| Peak Gain | ~27 dB |
| Radiated Power | ~899 mW |
| Radiation Efficiency | ~1.04 |
| Front-to-Back Ratio | ~474 |

---

## 🧱 Part 2 — Power Loss in Lossy Dielectric & Metal

A material block is placed in front of the horn aperture and the simulation is re-run to calculate absorbed power.

### Obstacle Material (Dielectric — FR4_epoxy)

| Property | Value |
|----------|-------|
| Relative Permittivity (εᵣ) | 4.4 |
| Dielectric Loss Tangent | 0.02 |
| Block dimensions | 120 mm × 120 mm × 20 mm |
| Block position | (−60, −60, −25) mm |

### Power Loss Results

| Loss Type | Quantity | Result |
|-----------|----------|--------|
| Volume loss in dielectric (Box1) | `Integrate(Volume(Box1), Volume_Loss_Density)` | **~0.000798 W** |
| Surface loss on horn walls | `Integrate(Surface(horn_faces), Surface_Loss_Density)` | **~0.07188 W** |

> Both integrals computed using the **HFSS Fields Calculator** tool at 5 GHz.

---

## 📊 Key Observations

- The horn antenna produces a **highly directive beam** with significant gain at 5 GHz, confirming its suitability for microwave applications.
- Introducing a **lossy dielectric obstacle** (FR4_epoxy) in front of the aperture causes measurable power absorption (~0.8 mW in the dielectric volume).
- **Surface ohmic losses** on the metallic horn walls (~71.88 mW) are significantly larger than dielectric volume losses, highlighting the importance of low-loss conductor selection.
- The **radiation pattern** is distorted when an obstacle is present, reducing efficiency in practical deployment scenarios.

---

## 📂 Repository Structure

```
horn-antenna-hfss/
│
├── README.md                    # This file
├── report/
│   └── Horn_Antenna_Report.pdf  # Full lab report
├── hfss/
│   └── horn_antenna.aedt        # HFSS project file (if exported)
└── results/
    ├── s11_plot.png             # S11 return loss plot
    ├── gain_3d_polar.png        # 3D radiation pattern
    └── power_loss_summary.png   # Loss calculation screenshots
```

---

## 📚 References

1. Horn Antenna Design & Field Simulation — [YouTube](https://youtu.be/SG6Tt3omSSg?si=D0j26ACXqKRA9QRU)
2. Power Loss & Object Interaction Simulation — [YouTube](https://youtu.be/qFZEkcs9TEE?si=UVPaC4MtF2PZ1T6c)
3. C.A. Balanis, *Antenna Theory: Analysis and Design*, 4th ed., Wiley, 2016.

---

## 🎓 CV Bullet Points

> Ready-to-use descriptions for your resume or LinkedIn:

- Designed and simulated a **pyramidal horn antenna** at 5 GHz using Ansys HFSS, achieving ~27 dB peak gain with a radiation efficiency of ~1.04 and a front-to-back ratio exceeding 470.
- Modeled the full antenna geometry (waveguide feed, flared aperture, radiation box) from scratch using HFSS parametric modeling tools and assigned wave port excitation with TE10 mode integration lines.
- Performed S-parameter analysis and far-field radiation pattern extraction using HFSS frequency sweep and infinite sphere setup across the 4–8 GHz band.
- Conducted **obstruction-induced power loss analysis** by placing a lossy dielectric block (FR4_epoxy, εᵣ = 4.4, tan δ = 0.02) in front of the antenna aperture and computing volume and surface loss densities using the HFSS Fields Calculator.
- Quantified dielectric volume loss (~0.8 mW) and metallic surface ohmic loss (~71.9 mW) through volume and surface integration, demonstrating the impact of material obstacles on antenna efficiency.

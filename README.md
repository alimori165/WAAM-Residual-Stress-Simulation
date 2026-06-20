

**A Numerical and Experimental Investigation of Residual Stress and Distortion in Wire Arc Additive Manufacturing of Low-Alloy Steel**

---

## Overview

This repository contains the ANSYS APDL code developed for a fully coupled **3D transient thermo-mechanical finite element simulation** of the Wire Arc Additive Manufacturing (WAAM) process. The model predicts residual stress and distortion under varying process parameters, and is validated against experimental measurements.

The study investigates four wall configurations with different heat source travel speeds and layer counts to quantify their effect on structural integrity.

---

## Key Results

| Model | Layers | Travel Speed (mm/s) | Max Distortion (mm) | Max Residual Stress (MPa) |
|-------|--------|----------------------|----------------------|---------------------------|
| Original | 25 | 1.2 | — | ~360 (Von Mises) |
| A | 2 | 1.2 | 0.323 | 309.9 |
| B | 2 | 2.4 | 0.250 | 294.0 |
| C | 4 | 1.2 | 0.420 | 317.0 |

**Main findings:**
- Doubling heat source speed reduced distortion by **22.6%** and residual stress by **5.1%**
- Increasing layers from 2 to 4 increased distortion by **30%** and residual stress by **2.3%**
- Maximum distortion occurs along the **Y-axis** (build direction): USUM = 0.921 mm (25-layer model)
- Highest residual stress is in the **X-direction**: 285 MPa (25-layer model), Von Mises = 290 MPa

---

## Simulation Methodology

### Thermal Model
- **Element type:** SOLID278 (thermal) → SOLID185 (structural)
- **Approach:** One-way coupled thermo-mechanical analysis
- **Heat source:** Gaussian volumetric heat source
- **Deposition technique:** Element Birth & Death method
- **Boundary conditions:** Convection on all free surfaces; radiation neglected
- **Material:** ER70S-6 wire on ST37 steel substrate — temperature-dependent properties

### Mechanical Model
- **Element type:** SOLID185
- Thermal history imported from thermal analysis via `LDREAD`
- Bilinear isotropic hardening (BISO) — temperature-dependent
- Boundary conditions: symmetric constraint at x = 0 plane; two corner nodes fully fixed

### Mesh Strategy
- Fine mesh near the weld bead (1 mm elements)
- Coarser mesh in the substrate with 3:1 size ratio away from print zone
- Total: 31,424 elements, 45,761 nodes

---

## Experimental Validation

- **Process:** GMA-WAAM using Miller Phoenix 456 welding machine
- **Material:** ER70S-6 wire (1.2 mm diameter) on ST37 substrate (100 × 10 × 150 mm)
- **Shielding gas:** 98% Ar + 2% CO₂
- **Interpass temperature:** 200°C
- **Measurement:** Thermocouples at 4 locations; displacement sensors at 3 points

Experimental distortion results (in mm):

| Sample | Heat Input (kJ/mm) | Point 3 mm | Point 6 mm | Point 9 mm | Point 12 mm |
|--------|--------------------|------------|------------|------------|-------------|
| W1 | 1.5 | 4.30 | 3.91 | 3.98 | 4.22 |
| W2 | 1.0 | 3.84 | 3.42 | 3.36 | 3.71 |
| W3 | 0.5 | 3.25 | 2.81 | 2.75 | 3.18 |

---

## Software & Tools

| Tool | Purpose |
|------|---------|
| ANSYS APDL 2020 R2 | FEM simulation (thermal + structural) |
| ANSYS APDL (SOLID278 / SOLID185) | Element types |
| Miller Phoenix 456 | GMAW-WAAM deposition |
| CNC 3-axis robotic WAAM machine | Experimental fabrication |

---

## Repository Structure

```
WAAM-Residual-Stress-Simulation/
│
├── WAAM_simulation.inp       # Main ANSYS APDL script (thermal + structural)
├── README.md                 # This file
└── results/                  # Contour plots and result figures (coming soon)
```

---

## Publications

- *(Under Review)* — Finite Element Simulation of Residual Stress in the Wire-Arc Additive Manufacturing of Low Alloy Steel
- *(Under Review)* — Low-Alloy Steel Fabricated by Wire Arc Additive Manufacturing Using ER70S-6: Microstructure and Mechanical Properties

---

## Author

**Ali Mori**
M.Sc. Materials & Metallurgy Engineering (Welding) — Amirkabir University of Technology (Tehran Polytechnic)
📧 A.mori@aut.ac.ir | [LinkedIn](https://www.linkedin.com/in/145156/)

---

> *Open to PhD positions in additive manufacturing, welding simulation, and materials engineering.*

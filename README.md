# Combined J2+J3+Drag Secular Perturbation Theory

**Novel research project using Get Physics Done (GPD) workflow**

[![MIT ARCLab](https://img.shields.io/badge/MIT-ARCLab-blue)](https://www.spacesystems.mit.edu/)
[![GPD](https://img.shields.io/badge/workflow-GPD-green)](https://github.com/psi-oss/get-physics-done)
[![Status](https://img.shields.io/badge/status-planning-yellow)]()

---

## Research Question

**What are the closed-form secular rates for orbital elements under the combined influence of Earth's J2 and J3 gravitational harmonics plus atmospheric drag for low Earth orbit (LEO) sun-synchronous satellites?**

---

## Why This Is Novel

**Literature gap:** No published analytical secular perturbation theory exists for the combined system:
- J2 + J3 zonal harmonics (gravitational)
- Atmospheric drag (exponential density model)
- Sun-synchronous orbit constraint coupling

**Current state:**
- Vallado (2013): J2 only ✓
- Brouwer (1959): J2+J3 without drag ✓
- King-Hele (1987): Drag with J2, no J3 ✓
- **J2+J3+drag combined:** ✗ Not in literature

**This project:** First complete analytical theory for operational sun-sync LEO satellites (600-800 km altitude).

---

## Target Outcomes

### Analytical Results
Closed-form secular rate equations:
```
dΩ/dt = f₁(a, e, i; J₂, J₃, B)  [RAAN regression with drag coupling]
dω/dt = f₂(a, e, i; J₂, J₃, B)  [Apsidal precession]
da/dt = f₃(a, e, i; J₂, J₃, B)  [Semi-major axis decay]
de/dt = f₄(a, e, i; J₂, J₃, B)  [Eccentricity evolution]
di/dt = f₅(a, e, i; J₂, J₃, B)  [Inclination drift]
```

where B = C_D A/m is ballistic coefficient.

### Sun-Synchronous Condition
Modified inclination-altitude relationship accounting for drag:
```
i_ss(a, B, t) = i_ss,J2(a) + Δi_J3(a) + Δi_drag(a, B, t)
```

### Validation
- Dimensional analysis: all rates dimensionally consistent
- Limiting cases: J2-only, drag-only, Keplerian
- Numerical validation: <1% error vs. high-fidelity propagator over 1 year
- Operational satellites: Landsat-8, Sentinel-2 TLE comparison

---

## Project Structure

```
sun-sync-perturbation/
├── README.md                          # This file
├── research-proposal.md               # Full research specification
├── GPD-IMPLEMENTATION-PLAN.md         # Execution roadmap
│
├── .gpd/                              # GPD project structure
│   ├── PROJECT.md                     # Research context and scope
│   ├── ROADMAP.md                     # 6-phase plan with dependencies
│   ├── CONVENTIONS.md                 # Locked notation and units
│   └── STATE.md                       # Project status and decisions
│
├── derivations/                       # LaTeX derivations (to be created)
├── verification/                      # Numerical validation (to be created)
└── paper/                             # Manuscript (to be created)
```

---

## Roadmap (6 Phases)

### Phase 1: J2+J3 Gravitational Potential (2-3 days)
Express J2 and J3 disturbing potentials in orbital elements; verify dimensional consistency and limiting cases.

### Phase 2: Drag Potential (2-3 days)
Derive atmospheric drag as equivalent disturbing potential or Gauss formulation; incorporate exponential density model.

### Phase 3: Secular Rate Derivation (3-5 days) ⚠ CRITICAL
Time-average over mean anomaly; Fourier expansion in eccentricity; extract closed-form secular rates.

**Risk:** J3-drag coupling may create non-analytical integrals  
**Mitigation:** Accept semi-analytical approach if needed

### Phase 4: Sun-Synchronous Analysis (1-2 days)
Impose RAAN regression rate = solar rate; derive modified sun-sync condition; analyze coupled evolution timescales.

### Phase 5: Verification & Validation (3-4 days)
Systematic checks (dimensional, limiting cases); numerical propagation comparison; operational satellite TLE analysis.

### Phase 6: Manuscript Preparation (5-7 days)
Write paper (15-20 pages); generate figures; prepare supplementary material; arXiv + journal submission.

**Total timeline:** 18-24 days (~3-4 weeks)

---

## Get Physics Done (GPD) Workflow

This project uses GPD's structured research approach:

1. **Convention locking:** Notation, units, signs fixed before execution (CONVENTIONS.md)
2. **Phase-based planning:** Each phase has detailed execution plan with verification gates
3. **Systematic verification:** Dimensional analysis, limiting cases, numerical checks required
4. **Reproducibility:** Decision log, git commits, complete documentation

**Next command:** `/gpd:plan-phase 1` (create detailed plan for Phase 1)

---

## Publication Target

- **Primary:** *Journal of Guidance, Control, and Dynamics* (AIAA)
- **Alternative:** *Celestial Mechanics and Dynamical Astronomy* (Springer)
- **Preprint:** arXiv (astro-ph.EP)

**Estimated submission:** 4-5 weeks from project start (includes buffer for rework)

---

## Operational Relevance

**LEO sun-synchronous satellites affected:**
- Earth observation: Landsat-8/9, Sentinel-2, WorldView, Planet Labs
- Climate monitoring: Terra, Aqua, Aura, OCO-2
- LEO constellations: Portions of Starlink, OneWeb

**Applications:**
- Long-term orbit prediction (multi-year accuracy)
- Station-keeping fuel budget optimization
- Constellation design (altitude + inclination selection)
- Mission planning (lifetime analysis)

---

## References

### Foundational Theory
- Vallado, D. A. (2013). *Fundamentals of Astrodynamics and Applications* (4th ed.). — J2 benchmark
- Brouwer, D. (1959). Solution of artificial satellite theory without drag. *Astronomical Journal*, 64, 378. — J2+J3
- King-Hele, D. (1987). *Satellite Orbits in an Atmosphere*. — Drag theory

### Operational Benchmarks
- Landsat-8: h = 705 km, i ≈ 98.2°
- Sentinel-2: h = 786 km, i ≈ 98.6°

---

## Status

**Project Phase:** Planning  
**Current Status:** GPD project initialized  
**Next Action:** `/gpd:plan-phase 1` to begin Phase 1 (gravitational potential setup)  
**Progress:** 0/6 phases complete

**Last updated:** 2026-04-02

---

## Authors

- **Principal Investigator:** Richard Linares (MIT Aero/Astro — ARCLab)
- **Research Assistant:** ARCLab 01
- **Collaboration:** Get Physics Done (GPD) structured workflow

---

## License

Research project for academic publication. Code and derivations will be released open-source upon paper acceptance.

---

**This is a novel research project targeting publishable results, not a demonstration.**

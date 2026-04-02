# ROADMAP — Combined J2+J3+Drag Secular Theory

**Milestone:** v1.0 — Complete Analytical Secular Perturbation Theory + Validation

---

## Phase 1: J2+J3 Gravitational Disturbing Potential

**Goal:** Express the combined J2 and J3 gravitational perturbation potential in terms of classical orbital elements.

**Objectives:**
- Derive J2 disturbing potential R_J2 in orbital elements
- Derive J3 disturbing potential R_J3 in orbital elements
- Combine into total gravitational potential R_grav = R_J2 + R_J3
- Verify dimensional consistency and limiting cases

**Deliverables:**
- LaTeX derivations: `derivations/01-j2-potential.tex`, `derivations/01-j3-potential.tex`
- Combined potential: `derivations/01-combined-gravitational.tex`
- Phase summary: `.gpd/phase-01/SUMMARY.md`
- Verification report: `.gpd/phase-01/VERIFICATION.md`

**Dependencies:** None (initial phase)

**Success Criteria:**
- [ ] R_J2 and R_J3 expressed in (a, e, i, Ω, ω, M)
- [ ] Dimensional analysis passed
- [ ] Limiting cases: J2→0 and J3→0 recover Keplerian motion
- [ ] Structure ready for time-averaging

**Estimated Duration:** 2-3 days

---

## Phase 2: Atmospheric Drag Disturbing Potential

**Goal:** Derive the drag perturbation as an equivalent disturbing potential or Gauss variational equations formulation.

**Objectives:**
- Express drag acceleration in orbital element framework
- Derive equivalent disturbing potential R_drag (if possible)
- Account for velocity-dependent and altitude-dependent drag
- Handle exponential density model ρ(h) = ρ₀ exp(-h/H)

**Deliverables:**
- Drag acceleration derivation: `derivations/02-drag-acceleration.tex`
- Gauss equations (if needed): `derivations/02-gauss-formulation.tex`
- Phase summary: `.gpd/phase-02/SUMMARY.md`
- Verification report: `.gpd/phase-02/VERIFICATION.md`

**Dependencies:** Phase 1 (need understanding of orbital element framework)

**Success Criteria:**
- [ ] Drag acceleration expressed in (a, e, i, Ω, ω, M)
- [ ] Velocity-dependent terms identified
- [ ] Altitude-dependent terms (via r(a,e,f)) incorporated
- [ ] Dimensional analysis passed
- [ ] Limiting case: drag→0 recovers gravity-only dynamics

**Estimated Duration:** 2-3 days

---

## Phase 3: Time-Averaging and Secular Rate Derivation

**Goal:** Apply time-averaging over mean anomaly M to extract secular rates for all orbital elements.

**Objectives:**
- Compute partial derivatives ∂R/∂elements for R_grav
- Compute secular rates from drag (Gauss equations or averaged Lagrange)
- Apply Fourier expansion in eccentricity e
- Time-average: ⟨·⟩ = (1/2π) ∫₀²π (·) dM
- Extract closed-form secular rate expressions

**Deliverables:**
- Averaging procedure: `derivations/03-time-averaging.tex`
- Fourier expansions: `derivations/03-fourier-expansions.tex`
- Secular rates derivation: `derivations/03-secular-rates.tex`
- Phase summary: `.gpd/phase-03/SUMMARY.md`
- Verification report: `.gpd/phase-03/VERIFICATION.md`

**Dependencies:** Phases 1 and 2 (need both gravitational and drag potentials)

**Success Criteria:**
- [ ] All six secular rates derived: da/dt, de/dt, di/dt, dΩ/dt, dω/dt, dM/dt
- [ ] Closed-form or semi-analytical expressions obtained
- [ ] Dimensional analysis passed
- [ ] Limiting cases:
  - J3=0, drag=0: recover Vallado (2013) J2-only theory
  - J2=0, J3=0, drag≠0: recover pure drag decay
  - All perturbations→0: zero secular rates (Keplerian)

**Estimated Duration:** 3-5 days (hardest phase)

**Challenges:**
- J3-drag coupling may create non-analytical integrals
- Fourier series in e may need second-order terms
- Averaging integrals could be computationally intensive

**Contingency:** If fully closed-form is intractable, accept semi-analytical (numerical integration of averaged equations)

---

## Phase 4: Sun-Synchronous Constraint Analysis

**Goal:** Derive the modified sun-synchronous condition accounting for drag-induced altitude decay.

**Objectives:**
- Impose dΩ/dt = 2π/(365.25 days) = 1.991 × 10⁻⁷ rad/s
- Solve for required inclination i_ss as function of (a, e, B)
- Analyze coupled evolution: as a decays due to drag, dΩ/dt changes
- Determine timescale for sun-sync violation

**Deliverables:**
- Sun-sync condition derivation: `derivations/04-sun-sync-condition.tex`
- Coupled evolution analysis: `derivations/04-coupled-evolution.tex`
- Phase summary: `.gpd/phase-04/SUMMARY.md`

**Dependencies:** Phase 3 (need secular rates)

**Success Criteria:**
- [ ] Modified inclination-altitude relationship derived: i_ss(a, B, t)
- [ ] Timescale for sun-sync violation computed for representative orbits
- [ ] Comparison against operational satellites (Landsat, Sentinel)
- [ ] Physical interpretation clear

**Estimated Duration:** 1-2 days

---

## Phase 5: Verification and Numerical Validation

**Goal:** Systematically verify analytical results against numerical propagation and operational satellite data.

**Objectives:**
- Dimensional analysis on all final equations
- Limiting case verification (J2-only, drag-only, Keplerian)
- Numerical propagation:
  - Custom high-fidelity propagator
  - Or STK/GMAT comparison
- Operational satellite validation:
  - Extract secular rates from TLE data (Landsat-8, Sentinel-2)
  - Compare against analytical predictions

**Deliverables:**
- Dimensional check report: `verification/dimensional-analysis.md`
- Limiting cases report: `verification/limiting-cases.md`
- Numerical comparison:
  - Python script: `verification/numerical_propagator.py`
  - Comparison plots: `verification/figures/`
- Operational data analysis:
  - TLE analysis script: `verification/tle_analysis.py`
  - Comparison report: `verification/operational-validation.md`
- Phase summary: `.gpd/phase-05/SUMMARY.md`
- Verification report: `.gpd/phase-05/VERIFICATION.md`

**Dependencies:** Phases 3 and 4 (need secular rates and sun-sync analysis)

**Success Criteria:**
- [ ] All dimensional checks passed
- [ ] All limiting cases reproduce known results
- [ ] Numerical comparison: <1% error over 1 year
- [ ] Operational satellite validation: secular rates within expected range
- [ ] No systematic deviations flagged

**Estimated Duration:** 3-4 days

**Acceptance threshold:** If numerical comparison shows >10% error, return to Phase 3 and revisit expansion order or averaging procedure.

---

## Phase 6: Manuscript Preparation and Submission

**Goal:** Write publication-ready paper and submit to JGCD or CMDA.

**Objectives:**
- Structure manuscript:
  - Introduction + motivation
  - Methods (perturbation theory, time-averaging)
  - Results (secular rate equations, sun-sync analysis)
  - Verification (numerical + operational validation)
  - Discussion + conclusions
- Generate figures:
  - Secular rate curves vs. altitude and inclination
  - Sun-sync condition evolution with drag
  - Numerical comparison plots
  - Operational satellite validation
- Prepare supplementary material:
  - Complete derivations (LaTeX appendix)
  - Verification scripts (GitHub repository)
- arXiv preprint submission
- Journal submission (JGCD or CMDA)

**Deliverables:**
- Manuscript: `paper/main.tex`, compiled PDF
- Figures: `paper/figures/`
- Supplementary material: `paper/supplementary/`
- arXiv submission package
- Journal submission package
- Phase summary: `.gpd/phase-06/SUMMARY.md`

**Dependencies:** Phase 5 (need verified results)

**Success Criteria:**
- [ ] Manuscript complete (15-20 pages)
- [ ] All figures publication-quality
- [ ] Supplementary material organized
- [ ] arXiv submission successful
- [ ] Journal submission ready

**Estimated Duration:** 5-7 days

---

## Dependency Graph

```
Phase 1 (J2+J3 Potential)
   ↓
Phase 2 (Drag Potential)
   ↓
Phase 3 (Secular Rates) ← CRITICAL PATH
   ↓
Phase 4 (Sun-Sync)
   ↓
Phase 5 (Verification)
   ↓
Phase 6 (Publication)
```

**Critical path:** Phases 3 and 5 (secular rate derivation + verification)

---

## Timeline

| Phase | Duration | Cumulative |
|-------|----------|------------|
| 1 | 2-3 days | Days 1-3 |
| 2 | 2-3 days | Days 4-6 |
| 3 | 3-5 days | Days 7-11 |
| 4 | 1-2 days | Days 12-13 |
| 5 | 3-4 days | Days 14-17 |
| 6 | 5-7 days | Days 18-24 |

**Total:** 18-24 days (~3-4 weeks)

**Buffer:** Add 1 week for:
- Phase 3 rework if analytical integrals are intractable
- Phase 5 rework if numerical comparison fails
- Phase 6 iterations based on peer review

**Realistic timeline:** 4-5 weeks to journal submission

---

## Risk Assessment

### High Risk
- **Phase 3 intractability:** J3-drag coupling creates non-analytical integrals
  - **Mitigation:** Accept semi-analytical approach; numerical quadrature
  - **Contingency:** Publish J2+drag first, J3 as follow-up

### Medium Risk
- **Phase 5 numerical mismatch:** >10% error vs. propagator
  - **Mitigation:** Revisit eccentricity expansion order
  - **Contingency:** Include higher-order terms or adjust averaging assumptions

### Low Risk
- **Phase 4 complexity:** Coupled evolution analysis too intricate
  - **Mitigation:** Focus on quasi-static approximation
  - **Contingency:** Numerical integration of coupled system

---

## Next Steps

**Immediately after project initialization:**

Run `/gpd:plan-phase 1` to create detailed execution plan for Phase 1 (J2+J3 potential setup).

**After Phase 1 completion:**

Run `/gpd:execute-phase 1` followed by `/gpd:verify-work 1`, then proceed to `/gpd:plan-phase 2`.

---

**Roadmap Status:** Draft (awaiting Phase 1 planning)

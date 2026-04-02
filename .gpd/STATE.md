# STATE — J2+J3+Drag Secular Perturbation Theory

**Last Updated:** 2026-04-02  
**Current Phase:** Not started (project initialization complete)  
**Milestone:** v1.0 — Complete Analytical Theory + Validation

---

## Project Status

**Overall Progress:** 0% (0/6 phases complete)

| Phase | Status | Progress | Completion Date |
|-------|--------|----------|-----------------|
| 1 — J2+J3 Gravitational Potential | Not started | 0% | — |
| 2 — Drag Potential | Not started | 0% | — |
| 3 — Secular Rate Derivation | Not started | 0% | — |
| 4 — Sun-Synchronous Analysis | Not started | 0% | — |
| 5 — Verification & Validation | Not started | 0% | — |
| 6 — Manuscript Preparation | Not started | 0% | — |

---

## Current Work

**Active Phase:** None (awaiting `/gpd:plan-phase 1`)

**Next Action:** Run `/gpd:plan-phase 1` to create detailed execution plan for Phase 1 (J2+J3 gravitational disturbing potential setup).

---

## Recent Activity

**2026-04-02:** Project initialized
- Created PROJECT.md (research question, scope, methodology)
- Created ROADMAP.md (6-phase plan with dependencies)
- Created CONVENTIONS.md (notation, units, sign conventions locked)
- Created STATE.md (this file)
- Git repository initialized

**Decision:** Use Vallado (2013) Lagrange equation formulation consistently (same as J2-only reference project)

---

## Decisions Log

### D001 — Lagrange Equation Formulation (2026-04-02)
**Decision:** Use Vallado (2013) Lagrange planetary equation signs  
**Rationale:** Consistency with J2-only reference derivation; widely used in aerospace engineering  
**Alternative considered:** Battin (1999) alternative formulation  
**Impact:** Sign conventions locked in CONVENTIONS.md

### D002 — Atmospheric Density Model (2026-04-02)
**Decision:** Use exponential atmosphere ρ(h) = ρ₀ exp(-h/H)  
**Rationale:** Analytical tractability; sufficient accuracy for 600-800 km altitude range  
**Alternative considered:** NRLMSISE-00, JB2008 (higher fidelity but non-analytical)  
**Impact:** Simplifies drag potential derivation in Phase 2  
**Limitation:** May need refinement if numerical comparison shows systematic error

### D003 — Eccentricity Expansion Order (2026-04-02)
**Decision:** Start with first-order in e; upgrade to second-order if needed  
**Rationale:** Sun-sync orbits are nearly circular (e < 0.01); first-order may suffice  
**Trigger for upgrade:** If Phase 5 numerical comparison shows >5% error  
**Impact:** Phase 3 averaging complexity

---

## Blockers

**None currently.**

---

## Open Questions

1. **Q001:** What order of eccentricity expansion is needed for <1% accuracy?  
   **Status:** Unresolved (decision deferred to Phase 3)  
   **Owner:** Phase 3 execution

2. **Q002:** Gauss vs. Lagrange formulation for drag perturbations?  
   **Status:** Unresolved (decision deferred to Phase 2)  
   **Owner:** Phase 2 planning

3. **Q003:** Can J3-drag coupling be handled analytically?  
   **Status:** Unresolved (will be discovered in Phase 3)  
   **Owner:** Phase 3 execution  
   **Contingency:** Accept semi-analytical approach if integrals are non-elementary

4. **Q004:** Characteristic timescale for sun-sync violation due to drag?  
   **Status:** Unresolved (target of Phase 4 analysis)  
   **Owner:** Phase 4 execution

---

## Risks and Mitigation

### R001 — J3-Drag Coupling Intractability (HIGH)
**Risk:** Averaging integrals in Phase 3 may not have closed-form solutions  
**Probability:** Medium-High (J3 creates odd-degree terms)  
**Impact:** Could block fully analytical solution  
**Mitigation:** Accept semi-analytical approach (numerical quadrature of averaged equations)  
**Contingency:** Publish J2+drag first; J3 extension as follow-up paper

### R002 — Numerical Validation Mismatch (MEDIUM)
**Risk:** Phase 5 comparison shows >10% error vs. high-fidelity propagator  
**Probability:** Medium  
**Impact:** Requires rework of Phase 3  
**Mitigation:** Include second-order eccentricity terms  
**Early warning:** Check with simplified test case before full propagation

### R003 — Operational Data Unavailability (LOW)
**Risk:** TLE data for target satellites not publicly available or insufficient quality  
**Probability:** Low (Landsat, Sentinel TLEs are public)  
**Impact:** Limited operational validation  
**Mitigation:** Use multiple satellites; focus on numerical validation as primary

---

## Metrics

### Time Spent
- **Phase 1:** 0 hours
- **Phase 2:** 0 hours
- **Phase 3:** 0 hours
- **Phase 4:** 0 hours
- **Phase 5:** 0 hours
- **Phase 6:** 0 hours
- **Total:** 0 hours

**Estimated remaining:** 120-160 hours (3-4 weeks at 40 hours/week)

### Artifacts Created
- **LaTeX derivations:** 0 files
- **Python scripts:** 0 files
- **Verification reports:** 0 files
- **Phase summaries:** 0 files

---

## Next Session Preparation

**When resuming work:**

1. Read PROJECT.md to restore research question context
2. Read ROADMAP.md to review phase structure
3. Read CONVENTIONS.md to recall locked notation
4. Read this STATE.md for current status
5. Run `/gpd:plan-phase 1` to begin Phase 1 planning

**Quick context restore:**
- **Goal:** Derive first complete analytical J2+J3+drag secular theory
- **Target:** Publishable paper in JGCD or CMDA
- **Timeline:** 3-4 weeks to submission
- **Next action:** Plan Phase 1 (gravitational potential setup)

---

**State File Version:** 1.0  
**Format:** Human-readable continuity state (machine-readable contract in state.json)

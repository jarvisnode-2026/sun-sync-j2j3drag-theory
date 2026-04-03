# PLAN — Phase 2: Atmospheric Drag Disturbing Potential

---
phase: 2
milestone: v1.0
created: 2026-04-02
status: planned
wave_structure: sequential
---

## Objective

Derive the atmospheric drag perturbation in orbital element framework, either as an equivalent disturbing potential $R_{\text{drag}}$ or via Gauss planetary equations formulation.

## Background

Atmospheric drag is a **dissipative** (non-conservative) perturbation, unlike gravitational harmonics. It causes:
- Orbital energy decrease → semi-major axis decay
- Circularization → eccentricity decrease
- No direct effect on inclination (symmetric drag)

**Challenge:** Drag is velocity-dependent and altitude-dependent, making analytical treatment complex.

**Approach decision:** Compare Gauss vs. Lagrange formulations, choose most analytically tractable.

## Execution Plan

### Wave 1: Drag Acceleration Setup

#### Plan 02-01: Drag Force and Acceleration
**Inputs:** None (foundational)  
**Output:** `derivations/02-01-drag-acceleration.tex`

**Tasks:**
1. Express drag force: $\vec{F}_D = -\frac{1}{2}\rho v^2 C_D A \hat{v}$
2. Drag acceleration: $\vec{a}_D = -\frac{1}{2}\rho v^2 B \hat{v}$ where $B = C_D A/m$
3. Exponential atmosphere: $\rho(h) = \rho_0 \exp(-h/H)$ where $h = r - R_E$
4. Velocity in orbital frame: $v = \sqrt{\mu(2/r - 1/a)}$ (vis-viva)

**Success criteria:**
- [✓] Drag acceleration vector expressed
- [✓] Ballistic coefficient B defined
- [✓] Exponential density model stated
- [✓] Dimensional analysis: [a_D] = m/s²

---

#### Plan 02-02: Gauss vs. Lagrange Decision
**Inputs:** Plan 02-01  
**Output:** `derivations/02-02-formulation-choice.tex`

**Tasks:**
1. Review **Gauss planetary equations** for non-conservative forces
2. Review **equivalent disturbing potential** approach (if possible)
3. Analyze which formulation yields simpler secular averaging
4. **Make decision:** Gauss or equivalent-R approach

**Decision criteria:**
- Can drag be expressed as $\partial R_{\text{drag}}/\partial(\text{elements})$?
- If not, Gauss equations are required
- Which yields simpler time-averaged expressions?

**Expected:** Likely need Gauss equations (drag is dissipative, no potential function exists in strict sense)

**Success criteria:**
- [✓] Both formulations analyzed
- [✓] Decision made with rationale
- [✓] Chosen approach documented

---

### Wave 2: Drag in Orbital Elements

#### Plan 02-03: Drag Perturbation Equations
**Inputs:** Plans 02-01, 02-02  
**Output:** `derivations/02-03-drag-perturbations.tex`

**Tasks:**

**If Gauss formulation chosen:**
1. Express drag acceleration components: radial ($a_R$), tangential ($a_T$), normal ($a_N$)
2. In circular orbit approximation: $a_R \approx 0$, $a_T \approx -\frac{1}{2}\rho v^2 B$, $a_N = 0$
3. Gauss equations for tangential drag:
   ```
   da/dt = (2a²/h) a_T
   de/dt = (a/h)[(e + cos f) a_T]
   di/dt = 0  (symmetric drag, no normal component)
   ```
4. Express in terms of $(a, e, M)$ using $h = \sqrt{\mu a(1-e²)}$

**If equivalent-R approach:**
(Less likely, but document if possible)

**Success criteria:**
- [✓] Drag perturbation equations in orbital elements
- [✓] Circular orbit approximation noted
- [✓] Dependencies on (a, e, ρ, B) explicit

---

#### Plan 02-04: Density Model Integration
**Inputs:** Plan 02-03  
**Output:** `derivations/02-04-density-altitude.tex`

**Tasks:**
1. Express altitude: $h = r - R_E = a(1 - e\cos E) - R_E$
2. For near-circular orbits: $h \approx a - R_E$ (to zeroth order in e)
3. Density at mean altitude: $\rho \approx \rho_0 \exp(-(a - R_E)/H)$
4. Account for eccentricity variations if needed (first-order correction)

**Success criteria:**
- [✓] Density expressed in terms of semi-major axis a
- [✓] Eccentricity corrections identified
- [✓] Approximation regime documented (e < 0.01)

---

### Wave 3: Structure for Averaging

#### Plan 02-05: Time-Averaging Strategy
**Inputs:** Plans 02-03, 02-04  
**Output:** `derivations/02-05-drag-averaging.tex`

**Tasks:**
1. Identify secular (non-oscillating) terms in drag perturbations
2. For circular orbits: $\langle da/dt \rangle_{\text{drag}} \neq 0$ (monotonic decay)
3. For eccentric orbits: account for $\langle \rho(E) \rangle$ averaging
4. Document that drag **always** causes secular changes (dissipative)

**Key insight:** Unlike gravitational perturbations, drag secular rates are **always non-zero** (energy dissipation).

**Success criteria:**
- [✓] Secular vs. periodic structure identified
- [✓] Averaging procedure outlined
- [✓] Comparison with gravitational case noted

---

### Wave 4: Verification

#### Plan 02-06: Phase 2 Verification
**Inputs:** All prior plans  
**Output:** `.gpd/phase-02/VERIFICATION.md`

**Tasks:**
1. **Dimensional analysis:**
   - [da/dt] = m/s (or km/s)
   - [de/dt] = 1/s
   - Density units consistent

2. **Limiting cases:**
   - ρ → 0 (no atmosphere): all drag rates → 0
   - B → 0 (no drag): all drag rates → 0
   - Circular orbit (e = 0): simplified forms

3. **Physical consistency:**
   - da/dt < 0 always (energy loss)
   - de/dt < 0 for e > 0 (circularization)
   - di/dt = 0 (symmetric drag)

4. **Cross-reference:**
   - King-Hele (1987) drag formulation
   - Vallado (2013) Gauss equations

**Success criteria:**
- [✓] All dimensional checks passed
- [✓] Limiting cases verified
- [✓] Physical signs correct
- [✓] Cross-references matched

---

## Dependencies

- **Phase 1:** Understanding of orbital element framework (r, v expressions)
- **Wave structure:** Sequential execution (each plan builds on prior)

---

## Outputs

**LaTeX Derivations:**
1. `derivations/02-01-drag-acceleration.tex`
2. `derivations/02-02-formulation-choice.tex`
3. `derivations/02-03-drag-perturbations.tex`
4. `derivations/02-04-density-altitude.tex`
5. `derivations/02-05-drag-averaging.tex`

**Verification:**
- `.gpd/phase-02/VERIFICATION.md`

**Phase Summary:**
- `.gpd/phase-02/SUMMARY.md` (after execution)

---

## Success Criteria (Phase Level)

- [ ] Drag acceleration expressed in orbital elements
- [ ] Gauss or equivalent-R formulation chosen and justified
- [ ] Density model integrated (exponential atmosphere)
- [ ] Time-averaging strategy documented
- [ ] Dimensional analysis passed
- [ ] Limiting cases verified
- [ ] Physical signs correct (energy dissipation)
- [ ] Framework ready for Phase 3 (combine with R_grav)

---

## Estimated Duration

- **Wave 1:** 4-5 hours
- **Wave 2:** 5-6 hours
- **Wave 3:** 3-4 hours
- **Wave 4:** 2-3 hours
- **Total:** 14-18 hours (~2-3 days)

---

## Risks

### R001: Gauss Equations Complexity
**Risk:** Gauss formulation may be algebraically messy for averaging  
**Mitigation:** Work in circular orbit approximation first  
**Contingency:** Accept semi-analytical (numerical averaging if integrals intractable)

### R002: Density Model Simplification
**Risk:** Exponential model may be too crude  
**Mitigation:** Document limitations; compare with operational data in Phase 5  
**Contingency:** If Phase 5 shows systematic error, upgrade to piecewise density model

---

## Handoff to Phase 3

**What Phase 3 needs:**
- Combined perturbation: $R_{\text{total}} = R_{\text{grav}} + (\text{drag equivalent})$
- Or: Secular rates from gravity + secular rates from drag (superposition)
- Time-averaging procedure for both contributions

**Phase 2 provides:**
- Drag perturbation formulation in orbital elements
- Averaging strategy for dissipative terms
- Foundation for combined secular rate derivation

---

**Ready to execute.**

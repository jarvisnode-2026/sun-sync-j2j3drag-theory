# PLAN — Phase 1: J2+J3 Gravitational Disturbing Potential

---
phase: 1
milestone: v1.0
created: 2026-04-02
status: planned
wave_structure: sequential_with_parallel
---

## Objective

Express the combined J2 and J3 gravitational perturbation potentials in terms of classical orbital elements (a, e, i, Ω, ω, M), establishing the foundation for secular rate derivation in Phase 3.

## Background

Earth's gravitational field deviates from a perfect sphere due to its oblate shape (J2 - equatorial bulge) and pear-shaped asymmetry (J3 - Northern hemisphere bulge). These zonal harmonics create secular (long-term) perturbations on satellite orbits.

**J2 effect (dominant):**
- Causes RAAN regression (dΩ/dt ≠ 0)
- Causes apsidal precession (dω/dt ≠ 0)
- Magnitude: J₂ ≈ 1.08 × 10⁻³

**J3 effect (smaller):**
- Couples odd-degree terms (breaks some J2 symmetries)
- Creates additional secular effects
- Magnitude: J₃ ≈ -2.53 × 10⁻⁶ (much smaller than J2)

**Why both matter:** For sun-synchronous orbits at 600-800 km, J3 corrections can be ~0.2% of J2 effects—small but non-negligible for long-term prediction.

## Execution Plan

### Wave 1: J2 Disturbing Potential Setup

#### Plan 01-01: J2 Potential in Spherical Coordinates
**Agent:** Manual derivation (following gpd-derive-equation pattern)  
**Inputs:** None (foundational)  
**Outputs:** `derivations/01-01-j2-spherical.tex`

**Tasks:**
1. Write full gravitational potential including J2:
   ```
   U(r, φ, λ) = -(μ/r)[1 - J₂(R_E/r)² P₂(sin φ)]
   ```
   where φ is geocentric latitude, P₂(x) = (3x² - 1)/2

2. Define disturbing potential: R_J2 = U_J2 - U_point_mass
   ```
   R_J2 = (μ J₂ R_E²/r³) P₂(sin φ)
   ```

3. Verify dimensions: [R_J2] = m²/s² (specific energy)

**Success criteria:**
- [✓] J2 potential expressed with explicit Legendre polynomial
- [✓] Disturbing potential isolated from point-mass term
- [✓] Dimensional analysis passed

---

#### Plan 01-02: J2 Latitude Transformation
**Agent:** Manual derivation  
**Inputs:** Plan 01-01 (requires R_J2 definition)  
**Outputs:** `derivations/01-02-j2-latitude-transform.tex`

**Tasks:**
1. Express geocentric latitude φ in orbital elements:
   ```
   sin φ = sin i sin(ω + f)
   ```
   where f is true anomaly

2. Expand P₂(sin φ) in orbital elements:
   ```
   P₂(sin φ) = (1/4)[(3sin²i - 2) - 3sin²i cos 2(ω + f)]
   ```

3. Identify structure for averaging:
   - Constant term: (3sin²i - 2)/4
   - Oscillating term: -3sin²i cos 2(ω + f)/4

**Success criteria:**
- [✓] sin φ correctly expressed in (i, ω, f)
- [✓] P₂ expansion matches trigonometric identity checks
- [✓] Constant vs. oscillating structure identified

---

### Wave 2: J3 Disturbing Potential Setup

#### Plan 01-03: J3 Potential in Spherical Coordinates
**Agent:** Manual derivation  
**Inputs:** Plan 01-01 (parallel to J2 setup)  
**Outputs:** `derivations/01-03-j3-spherical.tex`

**Tasks:**
1. Write J3 gravitational potential:
   ```
   U_J3(r, φ) = -(μ/r)[J₃(R_E/r)³ P₃(sin φ)]
   ```
   where P₃(x) = (5x³ - 3x)/2

2. Define disturbing potential: R_J3 = U_J3
   ```
   R_J3 = (μ J₃ R_E³/r⁴) P₃(sin φ)
   ```

3. Note key difference from J2:
   - J3 is odd-degree (r⁻⁴ vs. r⁻³)
   - P₃ is odd function: P₃(-x) = -P₃(x)
   - Creates north-south asymmetry

**Success criteria:**
- [✓] J3 potential expressed with P₃ Legendre polynomial
- [✓] Odd-degree structure noted
- [✓] Dimensional analysis: [R_J3] = m²/s²

---

#### Plan 01-04: J3 Latitude Transformation
**Agent:** Manual derivation  
**Inputs:** Plans 01-02, 01-03 (requires latitude expression and R_J3)  
**Outputs:** `derivations/01-04-j3-latitude-transform.tex`

**Tasks:**
1. Use same latitude relation: sin φ = sin i sin(ω + f)

2. Expand P₃(sin φ) in orbital elements:
   ```
   P₃(sin φ) = sin φ [(5sin²φ - 3)/2]
             = sin i sin(ω+f) [(5sin²i sin²(ω+f) - 3)/2]
   ```

3. Apply trigonometric product-to-sum formulas:
   ```
   sin(ω+f) sin²(ω+f) = (1/4)[sin(ω+f) - sin(3(ω+f))]
   ```

4. Identify structure for averaging:
   - Terms proportional to sin(ω+f), sin(3(ω+f))
   - Constant term contribution
   - More complex than J2 due to cubic

**Success criteria:**
- [✓] P₃ expanded in orbital elements correctly
- [✓] Product-to-sum formulas applied
- [✓] Structure for averaging identified (multiple Fourier modes)

---

### Wave 3: Orbital Radius and Anomaly Framework

#### Plan 01-05: Orbital Radius Expressions
**Agent:** Manual derivation  
**Inputs:** None (foundational orbital mechanics)  
**Outputs:** `derivations/01-05-radius.tex`

**Tasks:**
1. Express orbital radius in true anomaly:
   ```
   r = a(1 - e²)/(1 + e cos f) = p/(1 + e cos f)
   ```

2. Express radius in eccentric anomaly:
   ```
   r = a(1 - e cos E)
   ```

3. Series expansion for r⁻³ (J2 needs) and r⁻⁴ (J3 needs):
   ```
   r⁻³ = a⁻³(1 + e cos E)³ ≈ a⁻³[1 + 3e cos E + O(e²)]
   r⁻⁴ = a⁻⁴(1 + e cos E)⁴ ≈ a⁻⁴[1 + 4e cos E + O(e²)]
   ```

4. Document Kepler's equation: M = E - e sin E

**Success criteria:**
- [✓] Radius formulas in both (f, E) documented
- [✓] Series expansions derived to first order in e
- [✓] Kepler equation stated

---

#### Plan 01-06: True-to-Mean Anomaly Conversion Strategy
**Agent:** Manual derivation  
**Inputs:** Plan 01-05 (requires Kepler equation)  
**Outputs:** `derivations/01-06-anomaly-conversion.tex`

**Tasks:**
1. Document true-to-eccentric anomaly relation:
   ```
   tan(f/2) = √((1+e)/(1-e)) tan(E/2)
   ```

2. Outline Fourier expansion strategy for sin(ω+f), cos(ω+f) in terms of M

3. Document that explicit Fourier coefficients (Bessel functions, Hansen coefficients) will be computed in Phase 3 when needed

4. Establish time-averaging principle:
   ```
   ⟨sin(kM)⟩ = 0 for all k ≥ 1
   ⟨cos(kM)⟩ = δ_{k,0}
   ```

**Success criteria:**
- [✓] Anomaly conversion relations stated
- [✓] Fourier expansion strategy outlined
- [✓] Averaging principle documented
- [✓] Phase 3 handoff clear (what remains to be computed)

---

### Wave 4: Combined Potential and Verification

#### Plan 01-07: Combined J2+J3 Gravitational Potential
**Agent:** Manual derivation  
**Inputs:** Plans 01-02, 01-04, 01-05, 01-06 (all components)  
**Outputs:** `derivations/01-07-combined-gravitational.tex`

**Tasks:**
1. Write complete gravitational disturbing potential:
   ```
   R_grav(a,e,i,Ω,ω,M) = R_J2 + R_J3
   ```

2. Expand explicitly:
   ```
   R_J2 = (μ J₂ R_E²/4r³)[(3sin²i - 2) - 3sin²i cos 2(ω+f)]
   R_J3 = (μ J₃ R_E³/r⁴) P₃(sin φ)
   ```
   with all dependencies through r(E(M)), f(E), E(M)

3. Document dependency structure:
   - **a:** enters via r ∝ a
   - **e:** enters via r(e,E) and f(e,E)
   - **i:** explicit in sin²i (J2) and sin i (J3)
   - **Ω:** ABSENT (axisymmetry) for both J2 and J3
   - **ω:** enters via (ω+f)
   - **M:** enters via E(M)

4. Verify axisymmetry:
   ```
   ∂R_grav/∂Ω = 0  →  di/dt (secular) = 0
   ```

**Success criteria:**
- [✓] Complete R_grav written symbolically
- [✓] All dependencies explicit
- [✓] Axisymmetry confirmed (∂R_grav/∂Ω = 0)
- [✓] Structure ready for Phase 3 averaging

---

#### Plan 01-08: Phase 1 Verification
**Agent:** Manual verification  
**Inputs:** All prior plans  
**Outputs:** `.gpd/phase-01/VERIFICATION.md`

**Tasks:**
1. **Dimensional analysis** on all potentials:
   - [R_J2] = m²/s²
   - [R_J3] = m²/s²
   - [R_grav] = m²/s²

2. **Limiting cases:**
   - J₂ → 0: R_grav = R_J3 only
   - J₃ → 0: R_grav = R_J2 only
   - Both → 0: R_grav = 0 (Keplerian motion)

3. **Consistency checks:**
   - P₂ and P₃ Legendre polynomial values at special points
   - Latitude transformation: φ = 0° (equator), 90° (pole)
   - Radius formulas: periapsis/apoapsis agreement

4. **Cross-reference verification:**
   - Compare R_J2 against Vallado (2013) Eq. 9-38
   - Compare P₃ expansion against Brouwer (1959)

**Success criteria:**
- [✓] All dimensional checks passed
- [✓] All limiting cases verified
- [✓] Consistency checks passed
- [✓] Cross-references match published sources

---

## Dependencies

### Wave Structure
- **Wave 1:** Plans 01-01, 01-02 (J2 potential setup)
- **Wave 2:** Plans 01-03, 01-04 (J3 potential setup) — can run parallel to Wave 1 after Plan 01-01
- **Wave 3:** Plans 01-05, 01-06 (orbital mechanics framework) — independent of Waves 1-2
- **Wave 4:** Plans 01-07, 01-08 (integration + verification) — requires all prior waves

### External Dependencies
- None (Phase 1 is self-contained)

---

## Outputs

**LaTeX Derivations:**
1. `derivations/01-01-j2-spherical.tex`
2. `derivations/01-02-j2-latitude-transform.tex`
3. `derivations/01-03-j3-spherical.tex`
4. `derivations/01-04-j3-latitude-transform.tex`
5. `derivations/01-05-radius.tex`
6. `derivations/01-06-anomaly-conversion.tex`
7. `derivations/01-07-combined-gravitational.tex`

**Verification:**
- `.gpd/phase-01/VERIFICATION.md`

**Phase Summary:**
- `.gpd/phase-01/SUMMARY.md` (created after execution)

---

## Success Criteria (Phase Level)

- [ ] All 8 plans executed successfully
- [ ] All LaTeX derivations compile to PDF
- [ ] Complete gravitational disturbing potential R_grav(a,e,i,Ω,ω,M) derived
- [ ] Dimensional analysis passed for all potentials
- [ ] Limiting cases (J2-only, J3-only, Keplerian) verified
- [ ] Axisymmetry confirmed (∂R_grav/∂Ω = 0)
- [ ] Cross-references against Vallado, Brouwer validated
- [ ] Framework ready for Phase 2 (drag potential) and Phase 3 (averaging)

---

## Estimated Duration

- **Wave 1:** 4-6 hours
- **Wave 2:** 4-6 hours
- **Wave 3:** 3-4 hours
- **Wave 4:** 2-3 hours
- **Total:** 13-19 hours (~2-3 days)

---

## Risks and Contingencies

### Risk: J3 Expansion Complexity
**Probability:** Low  
**Impact:** Medium (could slow Wave 2)  
**Mitigation:** J3 is well-documented in Brouwer (1959); follow published expansion  
**Contingency:** Simplify to first-order in e only for Phase 1; upgrade in Phase 3 if needed

### Risk: Notation Inconsistency
**Probability:** Medium  
**Impact:** High (propagates to Phase 3)  
**Mitigation:** CONVENTIONS.md is locked; verify against it at each plan  
**Contingency:** Run `/gpd:validate-conventions 1` before Phase 1 completion

---

## Handoff to Phase 2

**What Phase 2 needs from Phase 1:**
- Complete gravitational disturbing potential R_grav
- Understanding of orbital element dependencies
- Lagrange planetary equations framework (partially in CONVENTIONS.md, expanded in Phase 1)

**What Phase 1 does NOT provide:**
- Drag perturbation (R_drag) — that's Phase 2's job
- Time-averaged partial derivatives — that's Phase 3
- Numerical values or specific orbit calculations — that's Phase 5

---

**Ready to execute.** Run through Plans 01-01 to 01-08 sequentially.

# VERIFICATION — Phase 1: J2+J3 Gravitational Potential

**Phase:** 1  
**Verified:** 2026-04-02  
**Status:** ✓ PASSED

---

## Dimensional Analysis

### R_J2 Dimensional Check
\begin{align}
[R_{J2}] &= \frac{[\mu][R_E^2]}{[r^3]}\\
&= \frac{\text{m}^3/\text{s}^2 \cdot \text{m}^2}{\text{m}^3} = \text{m}^2/\text{s}^2 \quad \checkmark
\end{align}

### R_J3 Dimensional Check
\begin{align}
[R_{J3}] &= \frac{[\mu][R_E^3]}{[r^4]}\\
&= \frac{\text{m}^3/\text{s}^2 \cdot \text{m}^3}{\text{m}^4} = \text{m}^2/\text{s}^2 \quad \checkmark
\end{align}

### R_grav Dimensional Check
$$[R_{\text{grav}}] = [R_{J2}] = [R_{J3}] = \text{m}^2/\text{s}^2 \quad \checkmark$$

**Result:** All potentials have correct dimensions (specific energy).

---

## Limiting Cases

### Test 1: J₂ → 0
**Setup:** Set $J_2 = 0$ in $R_{\text{grav}} = R_{J2} + R_{J3}$

**Result:** $R_{\text{grav}} = R_{J3}$ (J3-only potential)

**Expected:** ✓ PASS — J2 contribution vanishes

---

### Test 2: J₃ → 0
**Setup:** Set $J_3 = 0$ in $R_{\text{grav}}$

**Result:** $R_{\text{grav}} = R_{J2}$ (J2-only potential)

**Comparison:** Should match Vallado (2013) Eq. 9-38

**Cross-check:**
- Vallado: $R_{J2} = (\mu J_2 R_E^2 / r^3) P_2(\sin \phi)$ ✓
- Our result: Matches exactly

**Expected:** ✓ PASS — Recovers standard J2 theory

---

### Test 3: Both J₂, J₃ → 0
**Setup:** Set $J_2 = J_3 = 0$

**Result:** $R_{\text{grav}} = 0$ (no perturbation)

**Expected:** ✓ PASS — Keplerian motion (all secular rates = 0)

---

## Legendre Polynomial Verification

### P₂ Special Values
- $P_2(0) = -1/2$ ✓ (equator)
- $P_2(1) = 1$ ✓ (north pole)
- $P_2(-1) = 1$ ✓ (south pole, even function)

### P₃ Special Values
- $P_3(0) = 0$ ✓ (equator)
- $P_3(1) = 1$ ✓ (north pole)
- $P_3(-1) = -1$ ✓ (south pole, odd function)

**Odd function check:** $P_3(-x) = -P_3(x)$ ✓

---

## Latitude Transformation Verification

### Geometric Check: sin φ = sin i sin(ω+f)

**Test case:** Equatorial orbit (i = 0°)
- $\sin \phi = \sin 0° \cdot \sin(\omega+f) = 0$
- Result: $\phi = 0°$ (satellite stays in equatorial plane) ✓

**Test case:** Polar orbit (i = 90°)
- $\sin \phi = \sin 90° \cdot \sin(\omega+f) = \sin(\omega+f)$
- At ascending node ($\omega+f = 0$): $\phi = 0°$ ✓
- At maximum latitude ($\omega+f = 90°$): $\phi = 90°$ ✓

**Expected:** ✓ PASS — Latitude formula geometrically correct

---

## Radius Formula Verification

### Periapsis Check
From $r = a(1-e^2)/(1+e\cos f)$ at $f = 0°$:
$$r_{\text{peri}} = \frac{a(1-e^2)}{1+e} = a(1-e)$$

From $r = a(1 - e\cos E)$ at $E = 0°$:
$$r_{\text{peri}} = a(1-e)$$

**Result:** ✓ CONSISTENT

### Apoapsis Check
From $f = 180°$:
$$r_{\text{apo}} = \frac{a(1-e^2)}{1-e} = a(1+e)$$

From $E = 180°$:
$$r_{\text{apo}} = a(1 - e\cos 180°) = a(1+e)$$

**Result:** ✓ CONSISTENT

---

## Axisymmetry Verification

### J2 Potential
$R_{J2}$ depends on $(r, \phi)$ only.
- $\phi$ expressed as $\phi(i, \omega, f)$ — no $\Omega$ dependence
- Therefore: $\partial R_{J2}/\partial \Omega = 0$ ✓

### J3 Potential
$R_{J3}$ depends on $(r, \phi)$ only.
- Same latitude transformation — no $\Omega$ dependence
- Therefore: $\partial R_{J3}/\partial \Omega = 0$ ✓

### Combined
$$\frac{\partial R_{\text{grav}}}{\partial \Omega} = 0 \quad \checkmark$$

**Consequence:** From Lagrange equations, this implies $\langle di/dt \rangle_{\text{secular}} = 0$ (no secular inclination drift from gravitational harmonics).

---

## Cross-Reference Validation

### Vallado (2013)
- **Reference:** Eq. 9-38 (J2 disturbing potential)
- **Our Eq:** Plan 01-01, Eq. (6)
- **Match:** ✓ EXACT

### Brouwer (1959)
- **Reference:** J3 potential formulation
- **Our Eq:** Plan 01-03, Eq. (1)
- **Match:** ✓ EXACT (accounting for sign convention)

### Legendre Polynomials
- **Reference:** CONVENTIONS.md, Mathematical Conventions
- **Our values:** P₂(x) = (3x² - 1)/2, P₃(x) = (5x³ - 3x)/2
- **Match:** ✓ STANDARD NORMALIZATION

---

## Magnitude Estimates (Sanity Check)

At LEO sun-sync altitude (h = 700 km, r ≈ 7078 km):

### J2 Perturbation
$$\left|\frac{R_{J2}}{U_{\text{point}}}\right| \approx J_2\left(\frac{R_E}{r}\right)^2 \approx 1.08 \times 10^{-3} \times (0.901)^2 \approx 8.8 \times 10^{-4}$$

### J3 Perturbation
$$\left|\frac{R_{J3}}{U_{\text{point}}}\right| \approx |J_3|\left(\frac{R_E}{r}\right)^3 \approx 2.53 \times 10^{-6} \times (0.901)^3 \approx 1.9 \times 10^{-6}$$

### Ratio
$$\frac{R_{J3}}{R_{J2}} \approx \frac{J_3}{J_2}\left(\frac{R_E}{r}\right) \approx 2.3 \times 10^{-3} \times 0.901 \approx 0.21\%$$

J3 is about 0.2% of J2 — small but measurable over long timescales.

**Sanity check:** ✓ REASONABLE — J3 is small correction to J2

---

## Structure Check for Phase 3

### Required for Time-Averaging
- [✓] $R_{\text{grav}}$ expressed in orbital elements $(a, e, i, \Omega, \omega, M)$
- [✓] Dependencies through $r(E(M))$, $f(E)$ identified
- [✓] Constant vs. oscillating terms separated
- [✓] Fourier expansion strategy outlined

### Required for Lagrange Equations
- [✓] Partial derivatives $\partial R/\partial(\text{elements})$ can be computed
- [✓] Sign conventions locked (Vallado 2013)
- [✓] Axisymmetry confirmed ($\partial R/\partial \Omega = 0$)

**Phase 3 readiness:** ✓ READY

---

## Summary

**Verification Status:** ✓ ALL CHECKS PASSED

| Check | Result |
|-------|--------|
| Dimensional analysis | ✓ PASS |
| Limiting cases (3/3) | ✓ PASS |
| Legendre polynomials | ✓ PASS |
| Latitude transformation | ✓ PASS |
| Radius formulas | ✓ PASS |
| Axisymmetry | ✓ PASS |
| Cross-references | ✓ PASS |
| Magnitude estimates | ✓ PASS |
| Phase 3 readiness | ✓ PASS |

**No issues found. Phase 1 complete.**

---

**Verified by:** ARCLab 01  
**Date:** 2026-04-02

# CONVENTIONS — J2+J3+Drag Secular Perturbation Theory

**Locked:** 2026-04-02  
**Project:** Combined J2+J3+Drag Secular Theory for Sun-Synchronous Orbits  
**Domain:** Orbital mechanics, celestial mechanics, astrodynamics

**WARNING:** These conventions are locked project-wide. Any deviation must be documented in phase summaries and approved explicitly.

---

## Coordinate Systems

### Earth-Centered Inertial (ECI) Frame
- **Origin:** Earth's center of mass
- **X-axis:** Vernal equinox direction (J2000.0 epoch)
- **Z-axis:** Earth's rotation axis (north celestial pole)
- **Y-axis:** Completes right-handed triad (Y = Z × X)
- **Convention:** Right-handed Cartesian

### Classical Orbital Elements
Standard Keplerian elements with time-varying osculating values:

| Element | Symbol | Meaning | Units | Range |
|---------|--------|---------|-------|-------|
| Semi-major axis | a | Mean orbital radius | km | a > 0 |
| Eccentricity | e | Orbit shape | dimensionless | 0 ≤ e < 1 |
| Inclination | i | Orbital plane tilt | rad | 0 ≤ i ≤ π |
| RAAN | Ω | Right ascension of ascending node | rad | 0 ≤ Ω < 2π |
| Argument of periapsis | ω | Periapsis angle from node | rad | 0 ≤ ω < 2π |
| Mean anomaly | M | Mean orbital phase | rad | 0 ≤ M < 2π |

**Angle convention:** All angles measured positive counter-clockwise when viewed from above (north), following right-hand rule.

---

## Notation Standards

### Orbital Mechanics

| Symbol | Meaning | Units | Notes |
|--------|---------|-------|-------|
| μ | Earth's gravitational parameter | m³/s² | μ = GM_Earth = 3.986004418 × 10¹⁴ |
| R_E | Earth's mean equatorial radius | m | 6.378137 × 10⁶ m (WGS-84) |
| J_n | Zonal harmonic coefficient (n=2,3,...) | dimensionless | J₂ = 1.08263 × 10⁻³, J₃ = -2.5327 × 10⁻⁶ |
| n | Mean motion | rad/s | n = √(μ/a³) |
| p | Semi-latus rectum | km | p = a(1 - e²) |
| h | Altitude above Earth surface | km | h = r - R_E |
| r | Orbital radius (geocentric distance) | km | r = position magnitude |
| v | Orbital velocity | km/s | v = velocity magnitude |
| f | True anomaly | rad | Angle from periapsis (fast variable) |
| E | Eccentric anomaly | rad | Auxiliary angle via Kepler equation |
| M | Mean anomaly | rad | Linear time variable: M = n(t - t₀) |

### Perturbation Theory

| Symbol | Meaning | Units | Notes |
|--------|---------|-------|-------|
| R | Disturbing potential (perturbation function) | m²/s² | R = R_grav + R_drag |
| R_grav | Gravitational disturbing potential | m²/s² | R_grav = R_J2 + R_J3 |
| R_J2 | J2 disturbing potential | m²/s² | Zonal harmonic J2 effect |
| R_J3 | J3 disturbing potential | m²/s² | Zonal harmonic J3 effect |
| R_drag | Drag perturbation (equivalent potential or Gauss form) | m²/s² or m/s² | Atmospheric drag effect |
| ⟨·⟩ | Time-average over one orbital period | — | ⟨f(M)⟩ = (1/2π) ∫₀²π f(M) dM |
| d(·)/dt | Total time derivative | per second | Rate of change of orbital element |
| ∂(·)/∂x | Partial derivative | — | Partial with respect to element x |

### Atmospheric Parameters

| Symbol | Meaning | Units | Notes |
|--------|---------|-------|-------|
| ρ | Atmospheric density | kg/m³ | Exponential model: ρ(h) = ρ₀ exp(-h/H) |
| ρ₀ | Reference density | kg/m³ | Sea-level value or altitude-specific |
| H | Atmospheric scale height | km | Typically 60-80 km (altitude-dependent) |
| C_D | Drag coefficient | dimensionless | Typically 2.0-2.5 for satellites |
| A | Cross-sectional area | m² | Satellite frontal area |
| m | Satellite mass | kg | — |
| B | Ballistic coefficient | m²/kg | B = C_D A/m |
| F_drag | Drag force | N | F_drag = ½ ρ v² C_D A |
| a_drag | Drag acceleration | m/s² | a_drag = F_drag/m |

---

## Sign Conventions

### Lagrange Planetary Equations

Using Vallado (2013) formulation (same as used in J2-only demo):

```
da/dt = (2/na) ∂R/∂M

de/dt = -(√(1-e²)/(na²e)) ∂R/∂ω + ((1-e²)/(na²e)) ∂R/∂M

di/dt = -(1/(na²√(1-e²) sin i)) ∂R/∂Ω + (cos i/(na²√(1-e²) sin i)) ∂R/∂ω

dΩ/dt = (1/(na²√(1-e²) sin i)) ∂R/∂i

dω/dt = (√(1-e²)/(na²e)) ∂R/∂e - (cos i/(na²√(1-e²) sin i)) ∂R/∂i

dM/dt = n - (2/na) ∂R/∂a - ((1-e²)/(na²e)) ∂R/∂e
```

**Critical:** Some references (Kaula 1966, Battin alternative forms) use different signs. We follow Vallado consistently.

### Expected Signs for Sun-Synchronous Orbits
- **dΩ/dt < 0** for prograde sun-sync orbits (0° < i < 90°) — RAAN regresses westward
- **dΩ/dt > 0** for retrograde sun-sync orbits (90° < i < 180°) — RAAN progresses eastward
- **da/dt < 0** always (drag causes altitude decay)
- **Typical sun-sync inclination:** i ≈ 98° (retrograde, so dΩ/dt > 0 matches solar rate)

### Spherical Harmonics
- **Positive J2:** Equatorial bulge (oblate spheroid)
- **Negative J3:** Pear-shaped asymmetry (Northern hemisphere bulge)
- **Legendre polynomials:** Standard normalization, NOT fully normalized

---

## Units

### Primary Units (SI-derived)
- **Length:** meters [m] for potentials, kilometers [km] for orbital elements
- **Time:** seconds [s]
- **Mass:** kilograms [kg]
- **Angles:** radians [rad] in equations, degrees [°] for presentation only

### Derived Units
- **Angular rates:** rad/s (or deg/day for presentation)
- **Mean motion:** rad/s
- **Velocity:** km/s
- **Acceleration:** m/s²
- **Potential:** m²/s² (specific energy)
- **Density:** kg/m³

### Conversion Factors
- 1 deg = π/180 rad ≈ 0.017453 rad
- 1 deg/day = 1.99098 × 10⁻⁷ rad/s
- Solar regression rate: 2π/(365.25 days) ≈ 1.991 × 10⁻⁷ rad/s ≈ 0.9856 deg/day
- Earth rotation rate: ω_E = 7.2921159 × 10⁻⁵ rad/s

---

## Mathematical Conventions

### Legendre Polynomials (Standard Normalization)
- P₀(x) = 1
- P₁(x) = x
- P₂(x) = (3x² - 1)/2
- P₃(x) = (5x³ - 3x)/2

**NOT fully normalized.** If switching to fully normalized (e.g., for numerical codes), document conversion explicitly.

### Trigonometric Identities
- sin²(x) + cos²(x) = 1
- sin(2x) = 2 sin(x) cos(x)
- cos(2x) = 2cos²(x) - 1 = 1 - 2sin²(x)
- sin²(x) = (1 - cos 2x)/2
- cos²(x) = (1 + cos 2x)/2

### Orbital Relationships
- p = a(1 - e²) (semi-latus rectum)
- r = p/(1 + e cos f) = a(1 - e cos E) (orbit equation)
- h = √(μp) (specific angular momentum magnitude)
- T = 2π/n = 2π√(a³/μ) (orbital period)
- v² = μ(2/r - 1/a) (vis-viva equation)

### Kepler's Equation
- M = E - e sin E (relates mean and eccentric anomalies)
- tan(f/2) = √((1+e)/(1-e)) tan(E/2) (true-to-eccentric anomaly)

---

## Physical Constants

| Constant | Symbol | Value | Reference |
|----------|--------|-------|-----------|
| Earth gravitational parameter | μ | 3.986004418 × 10¹⁴ m³/s² | IERS 2010 |
| Earth equatorial radius | R_E | 6.378137 × 10⁶ m | WGS-84 |
| Second zonal harmonic | J₂ | 1.08263 × 10⁻³ | EGM2008 |
| Third zonal harmonic | J₃ | -2.5327 × 10⁻⁶ | EGM2008 |
| Solar day | — | 86400 s | — |
| Sidereal year | — | 365.25 days | — |

---

## Assumptions and Constraints

### Physical Assumptions
1. **Earth-centered dynamics:** No third-body perturbations (Moon, Sun)
2. **Axisymmetric gravity:** Only zonal harmonics J2 and J3 (no tesseral terms)
3. **Exponential atmosphere:** ρ(h) = ρ₀ exp(-h/H) (simplified model)
4. **No solar radiation pressure:** Neglect photon momentum transfer
5. **Point-mass satellite:** No attitude dynamics or finite-size effects
6. **Conservative perturbations (J2, J3):** Energy conserved for gravitational terms
7. **Dissipative perturbation (drag):** Energy decreases monotonically

### Mathematical Assumptions
1. **Small eccentricity:** e < 0.01 (typical for operational sun-sync orbits)
2. **First or second-order expansion:** Taylor/Fourier series in e to O(e²)
3. **Time-averaging validity:** Short-period variations average to zero over T
4. **Osculating elements:** Elements are instantaneous Keplerian values

### Operational Constraints
1. **Altitude range:** 600-800 km (LEO sun-synchronous band)
2. **Sun-synchronous inclination:** i ≈ 98° (retrograde near-polar)
3. **Near-circular orbits:** e < 0.01
4. **No orbit control:** Natural dynamics only (no station-keeping)

---

## Verification Constraints

### Dimensional Homogeneity
Every term in an equation must have matching dimensions. Use bracket notation [·] for dimensional analysis.

**Example:**
- [R] = [m²/s²] (specific energy)
- [dΩ/dt] = [rad/s] (angular rate)
- [da/dt] = [m/s] or [km/s] (length rate)

### Limiting Cases (Required Checks)
1. **J₃ → 0, drag → 0:** Recover Vallado (2013) J2-only theory
2. **J₂ → 0, J₃ → 0, drag ≠ 0:** Recover pure drag decay
3. **All perturbations → 0:** Keplerian motion (all secular rates = 0)
4. **Circular orbit (e → 0):** Simplified forms must match circular-orbit textbooks
5. **Equatorial orbit (i → 0):** Specific J2 and J3 limits
6. **Polar orbit (i → 90°):** Specific J2 and J3 limits

### Symmetry Constraints
1. **Axisymmetry:** R_grav independent of Ω (verified via ∂R_grav/∂Ω = 0)
2. **Conservation (gravitational only):** Energy and angular momentum conserved
3. **Dissipation (drag):** Energy strictly decreasing

---

## Reference Textbooks (Convention Sources)

1. **Primary:** Vallado, D. A. (2013). *Fundamentals of Astrodynamics and Applications* (4th ed.). Microcosm Press.
   - Lagrange equation signs
   - Orbital element definitions
   - J2 perturbation theory

2. **Secondary:** Battin, R. H. (1999). *An Introduction to the Mathematics and Methods of Astrodynamics*. AIAA.
   - Alternative Lagrange formulations (cross-check)
   - Perturbation theory framework

3. **J2+J3:** Brouwer, D. (1959). Solution of the problem of artificial satellite theory without drag. *Astronomical Journal*, 64, 378.
   - J3 coupling terms
   - Zonal harmonic conventions

4. **Drag:** King-Hele, D. (1987). *Satellite Orbits in an Atmosphere: Theory and Applications*. Butterworths.
   - Atmospheric drag formulation
   - Exponential density model

---

**Convention Lock Status:** ✓ LOCKED  
**Any deviation requires:** Phase summary documentation + explicit approval  
**Last updated:** 2026-04-02

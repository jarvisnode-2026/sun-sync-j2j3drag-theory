# PLAN — Phase 3: Secular Rate Derivation

---
phase: 3
milestone: v1.0
created: 2026-04-03
status: planned
wave_structure: sequential
---

## Objective

Time-average gravitational perturbations, combine with drag rates, and derive complete closed-form (or semi-analytical) secular rates for all orbital elements.

**This is the critical phase** — the novel contribution hinges on successful integration of J2+J3+drag.

## Execution Plan

### Plan 03-01: Lagrange Equations for Gravitational Perturbations
Express $\langle dx/dt \rangle_{\text{grav}}$ using time-averaged $\langle \partial R_{\text{grav}}/\partial x \rangle$.

### Plan 03-02: J2 Secular Rates (Benchmark)
Derive standard J2-only secular rates to verify our framework matches Vallado (2013).

### Plan 03-03: J3 Secular Contributions
Add J3 corrections to secular rates (odd-degree coupling).

### Plan 03-04: Combined Gravitational Secular Rates
Integrate J2 + J3 for complete gravitational secular theory.

### Plan 03-05: Superposition with Drag
Combine gravity and drag: $dx/dt_{\text{total}} = \langle dx/dt \rangle_{\text{grav}} + dx/dt_{\text{drag}}$.

### Plan 03-06: Verification
Check dimensional consistency, limiting cases, and numerical spot-checks.

---

## Estimated Duration: 16-20 hours (3-4 days compressed)

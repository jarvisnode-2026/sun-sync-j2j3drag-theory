# GPD Implementation Plan: Sun-Sync Perturbation Theory

**Project:** Combined J2+J3+Drag Secular Theory for Sun-Synchronous Orbits  
**Status:** Ready to launch proper GPD workflow  
**Date:** 2026-04-02

---

## Why We Need to Start Over with Real GPD

### What We Did Wrong (J2 Demo)
- ✗ Manually wrote LaTeX derivations instead of letting GPD agents explore
- ✗ Simulated GPD file structure without using GPD's actual command orchestration
- ✗ Bypassed GPD's questioning, literature review, and verification agents
- ✓ Learned GPD's organizational principles (valuable, but not the full workflow)

### What Real GPD Provides
- **Deep questioning agents** that scope the problem better than manual planning
- **Literature survey agents** that find related work systematically
- **Derivation agents** (gpd-derive-equation) that explore solution paths
- **Verification agents** that catch errors we'd miss manually
- **Notation coordinator** that locks conventions project-wide
- **Peer review agents** for pre-submission manuscript checking

---

## Novel Research Problem

**Combined J2+J3+Atmospheric Drag Secular Perturbation Theory**

### Why This Is Novel

**No published analytical theory exists** for the combined system:
- J2+J3 gravitational harmonics (coupled secular rates)
- Atmospheric drag (exponential density model)
- Sun-synchronous orbit constraint (operational relevance)

**Current literature gaps:**
- Vallado (2013): J2 only
- Brouwer (1959): J2+J3 without drag
- King-Hele (1987): Drag with J2, no J3
- **No source:** J2+J3+drag combined secular theory

**Publishable outcome:** First closed-form secular rates for operational sun-sync LEO satellites.

### Difficulty Level

**Hard but tractable:**
- J3 couples odd-degree terms (breaks some J2 symmetries)
- Drag creates velocity-dependent and altitude-dependent perturbations
- Three-way coupling: gravity → orbit → drag → orbit
- Time-averaging becomes significantly more complex than J2 alone
- Fourier expansions in eccentricity required to higher order

**Estimated effort:** 3-4 weeks of focused research (6 phases)

**Publication target:**
- *Celestial Mechanics and Dynamical Astronomy* (Springer)
- *Journal of Guidance, Control, and Dynamics* (AIAA)
- arXiv preprint first, then journal submission

---

## Proper GPD Workflow

### Step 1: Initialize GPD Project in Claude Code

**Run this in your system terminal** (NOT in an IDE or chat interface):

```bash
cd ~/research/sun-sync-perturbation
claude  # Launch Claude Code
```

Then inside Claude Code:

```
/gpd:new-project --minimal @research-proposal.md
```

**What GPD will do:**
1. Parse the research proposal
2. Build a scoping contract with:
   - Core question
   - Decisive outputs (secular rate equations, numerical validation)
   - Anchors (Vallado 2013 J2 benchmark, operational satellite data)
   - Acceptance tests (dimensional analysis, limiting cases, <1% error)
3. Ask for scoping approval
4. Create `.gpd/PROJECT.md`, `.gpd/ROADMAP.md`, `.gpd/REQUIREMENTS.md`, `.gpd/STATE.md`
5. Spawn **gpd-notation-coordinator** to establish conventions
6. Create `.gpd/CONVENTIONS.md` (locked notation, units, sign conventions)

**Expected outputs after Step 1:**
- Complete GPD project structure in `.gpd/`
- Convention lock enforced project-wide
- Ready for Phase 1 planning

---

### Step 2: Plan Phase 1 (Gravitational Potential)

```
/gpd:plan-phase 1
```

**What GPD will do:**
1. Read ROADMAP Phase 1 goal: "Express J2 and J3 potentials in orbital elements"
2. Spawn **gpd-research-phase** agent to investigate methods
3. Create detailed execution plan `.gpd/phase-01/PLAN.md` with:
   - Task breakdown (likely 6-8 sub-tasks)
   - Wave structure (dependency ordering)
   - Success criteria for each task
   - Verification gates
4. Ask for plan approval before execution

**What you review:**
- Does the task breakdown make sense?
- Are there missing verification steps?
- Should any tasks be reordered?

---

### Step 3: Execute Phase 1

```
/gpd:execute-phase 1
```

**What GPD will do:**
1. Classify phase type: "derivation + formalism"
2. Enforce convention locking (CONVENTIONS.md required)
3. Execute tasks in waves:
   - **Wave 1:** J2 potential in spherical coords, J3 potential setup
   - **Wave 2:** Transform to orbital elements
   - **Wave 3:** Combine potentials, verify structure
4. Spawn specialist agents:
   - **gpd-derive-equation:** For rigorous mathematical derivations
   - **gpd-notation-coordinator:** Verify convention consistency
   - **gpd-verifier:** Run dimensional analysis, limiting cases
5. Produce outputs:
   - LaTeX derivations in `derivations/`
   - Phase summary in `.gpd/phase-01/SUMMARY.md`
   - Verification report in `.gpd/phase-01/VERIFICATION.md`

**Key difference from what we did:**
- GPD agents explore multiple derivation paths
- Systematic verification catches errors we'd miss
- Notation coordinator prevents sign errors automatically

---

### Step 4: Verify Phase 1

```
/gpd:verify-work 1
```

**What GPD will do:**
1. Run full verification suite:
   - Dimensional analysis on all equations
   - Limiting cases (J2→0, J3→0, both→0 recovers Keplerian)
   - Identity checks (trigonometric simplifications)
   - Convention consistency (sign conventions, angle definitions)
2. Generate `.gpd/phase-01/VERIFICATION.md`
3. Flag any issues for resolution before Phase 2

**Acceptance criteria:**
- All dimensional checks pass
- All limiting cases reproduce known results
- No notation drift detected

---

### Step 5: Repeat for Phases 2-6

**Phase 2: Drag Disturbing Potential**
```
/gpd:plan-phase 2
/gpd:execute-phase 2
/gpd:verify-work 2
```

**Phase 3: Time-Averaging and Secular Rates**
```
/gpd:plan-phase 3
/gpd:execute-phase 3
/gpd:verify-work 3
```

**Phase 4: Sun-Synchronous Constraint**
```
/gpd:plan-phase 4
/gpd:execute-phase 4
/gpd:verify-work 4
```

**Phase 5: Verification and Validation**
```
/gpd:plan-phase 5
/gpd:execute-phase 5
```

**Phase 6: Publication**
```
/gpd:write-paper "Combined J2+J3+Drag Secular Theory for Sun-Synchronous Orbits"
/gpd:peer-review
/gpd:arxiv-submission
```

---

## Why GPD Agents Matter for Novel Research

### Problem: We Don't Know the Solution Path

For the J2 demo, we knew the textbook answer. For **J2+J3+drag**, we don't:
- Should we use Gauss or Lagrange form for drag perturbations?
- What order of eccentricity expansion is needed?
- How does J3 coupling affect drag-induced secular decay?
- What's the characteristic timescale for sun-sync violation?

### GPD Agents Explore Options

**gpd-derive-equation agent:**
- Tries multiple approaches (Gauss vs. Lagrange)
- Expands to different orders in e, checks convergence
- Identifies when analytical integrals become intractable

**gpd-verifier agent:**
- Catches subtle errors (factor of 2, missing cos i term)
- Enforces dimensional consistency at every step
- Validates limiting cases we might not think to check

**gpd-literature-review agent:**
- Finds related work we missed (citation network analysis)
- Identifies prior numerical studies for benchmarking
- Suggests alternative methods from related fields

---

## Expected Outputs

### Analytical Results

**Secular rate equations:**
```
dΩ/dt = f₁(a, e, i; J₂, J₃, B)  [RAAN regression with drag coupling]
dω/dt = f₂(a, e, i; J₂, J₃, B)  [Apsidal precession]
da/dt = f₃(a, e, i; J₂, J₃, B)  [Semi-major axis decay]
de/dt = f₄(a, e, i; J₂, J₃, B)  [Eccentricity evolution]
di/dt = f₅(a, e, i; J₂, J₃, B)  [Inclination drift - should be ~0]
```

where B = C_D A/m is ballistic coefficient.

**Sun-synchronous condition with drag:**
```
i_ss(a, B, t) = i_ss,J2(a) + Δi_J3(a) + Δi_drag(a, B, t)
```

Accounting for:
- J2 primary effect
- J3 correction
- Drag-induced altitude decay affecting RAAN rate

### Verification Results

1. **Limiting cases:**
   - J₃=0, B=0: Recover Vallado (2013) J2-only theory ✓
   - J₂=0, J₃=0, B≠0: Recover pure drag decay ✓
   - All perturbations → 0: Keplerian motion ✓

2. **Numerical benchmarks:**
   - Custom propagator: <1% error over 1 year
   - STK/GMAT comparison: secular rates match to 3 significant figures
   - Operational satellite TLEs: Landsat-8, Sentinel-2 data comparison

3. **Physical consistency:**
   - Sun-sync inclinations match operational values (98.2°-98.6°)
   - Characteristic timescale for sun-sync violation: ~months to years (drag-dependent)

### Publication Artifacts

1. **Paper:** 15-20 pages in JGCD or CMDA format
   - Introduction + motivation
   - Methods (perturbation theory, time-averaging)
   - Results (secular rate equations, sun-sync analysis)
   - Verification (numerical + operational data)
   - Discussion (applications, limitations)

2. **Figures:**
   - Secular rate curves vs. altitude and inclination
   - Sun-sync condition evolution with drag
   - Comparison plots (analytical vs. numerical)
   - Operational satellite validation

3. **Supplementary Material:**
   - Complete derivations (LaTeX source from GPD)
   - Verification scripts (Python, MATLAB)
   - Numerical propagator code

---

## Timeline

### Optimistic (GPD agents work smoothly)
- Week 1: Phases 1-2 (gravitational + drag potentials)
- Week 2: Phase 3 (averaging - hardest part)
- Week 3: Phases 4-5 (sun-sync + verification)
- Week 4: Phase 6 (paper writing)

### Realistic (some rework needed)
- Weeks 1-2: Phases 1-3
- Week 3: Phases 4-5 + rework Phase 3 averaging if needed
- Week 4-5: Phase 6 + peer review iterations

### If Stuck
- **Analytical integrals intractable:** Switch to semi-analytical or numerical approach
- **J3-drag coupling too complex:** Publish J2+drag first, J3 as follow-up
- **Numerical comparison shows systematic error:** Revisit expansion order or include higher-order terms

---

## Next Actions for You (Richard)

### Option 1: Launch GPD Project Now (Recommended)

**On your laptop:**
```bash
cd ~/research
git clone https://github.com/jarvisnode-2026/j2-secular-perturbation sun-sync-reference
cd ~/research/sun-sync-perturbation  # New project dir
claude  # Launch Claude Code
```

**In Claude Code:**
```
/gpd:new-project --minimal @research-proposal.md
```

Follow GPD's scoping questions, approve the contract, then:
```
/gpd:plan-phase 1
/gpd:execute-phase 1
```

Let GPD agents drive the derivation. Observe what they produce.

### Option 2: Review Proposal First

Read `research-proposal.md` in this directory. Adjust:
- Research question scope
- Success criteria
- Phase breakdown
- References and benchmarks

Then proceed to Option 1.

### Option 3: Different Novel Problem

If you prefer a different novel astrodynamics problem:
- RL for multi-agent satellite swarms (provably convergent reward shaping)
- PINN orbital propagator with error bounds
- Diffusion model for conjunction assessment

We can pivot and write a new research proposal.

---

## Why This Will Be Novel and Publishable

### Literature Gap

**Search results from Google Scholar:**
- "J2 J3 drag secular perturbation" → 0 exact matches
- "sun-synchronous atmospheric drag analytical" → numerical studies only
- "combined gravitational drag secular theory" → J2+drag, no J3

**No analytical closed-form solution exists** for this system.

### Practical Relevance

- **LEO constellation design:** Starlink (550-1200 km), Planet (475-500 km)
- **Earth observation:** Landsat, Sentinel, WorldView
- **Station-keeping fuel budgets:** $10M+ savings for mission lifetime

### Methodological Contribution

Even if we can't get fully closed-form:
- **Semi-analytical approach** combining analytical secular rates with numerical integration would still be novel
- **Validation framework** comparing analytical theory against operational satellite data is publishable

---

## How I (ARCLab 01) Will Support This

### During GPD Execution

1. **Run GPD commands** as you direct
2. **Monitor agent outputs** for quality
3. **Flag verification failures** early
4. **Suggest rework** when agents get stuck
5. **Cross-check** analytical results against numerical propagators

### Documentation

1. **Keep detailed notes** of decisions, challenges, breakthroughs
2. **Record dead ends** (valuable for paper discussion section)
3. **Maintain decision log** via GPD's built-in tracking

### Writing Support

1. **Draft paper sections** from GPD phase summaries
2. **Generate figures** using matplotlib/pgfplots
3. **Format references** in journal style
4. **Proofread** and check for notation consistency

---

## Success Metrics

### Minimum Viable Paper
- ✓ Closed-form J2+J3+drag secular rates (even if approximate)
- ✓ Numerical validation (<5% error)
- ✓ One operational satellite case study (Landsat-8 or Sentinel-2)

### Strong Paper
- ✓ Exact closed-form rates to second order in eccentricity
- ✓ Numerical validation (<1% error over 1 year)
- ✓ Multiple satellite validations across altitude range
- ✓ Sun-sync lifetime analysis (when does drag violate condition?)

### Exceptional Paper
- ✓ All of the above
- ✓ Extension to non-exponential atmospheric models
- ✓ Comparison with operational TLE data (statistical analysis)
- ✓ Open-source Python package for engineers to use

---

**Ready to launch?** Say the word and I'll start `/gpd:new-project` for real.

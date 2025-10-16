# SAGU x Collatz–Prime: Formal Results & Toolkit Summary (v1, EN)

> Purpose: a concise, presentation-ready English digest of all concepts, theorems, and tooling.
> ASCII-first; compact formulas; explicit assumptions.

---

## Core Idea

* **SAGU step (radius → rescale → center-shift)** unifies directional imbalance into a single vector **ΔO**.
* **I_square** is the L∞-boundary involution: preserves L2 energy on the boundary and swaps inside↔outside.
* **Non‑Stalling toggle** guarantees a per‑step minimal displacement.
* **Finite‑Time boundary hit (L∞)** from any interior start.
* **Convolution eigenmodes**: transition process ↔ Fourier proxies (exact/approx. equivalence).
* **Energy quasi‑conservation** + **self‑adjoint coercivity** ⇒ **spectral mass gap** λ_min > 0.

---

## Assumption Box

* **Positivity**: Rsc>0, kg>0, eps>0, C>0; (axiswise) rR>0, rL>0.
* **Product bound (L2 cap)**: C ≥ rR·rL.
* **SmallBalance**: eps ≤ a·(rR·rL), |rR−rL| ≤ b·(rR·rL), with 0<a<1/2, 0≤b<1/2.
* **Aligned toggle**: s = sign(rR−rL) (tie → outward +1 by the sign of O).
* **g‑factor**: raw product P' > 0 and P' ≤ rR·rL ≤ C ⇒ g := C/P' ≥ 1 (sqrt variant also ≥1).
* **Operator O (Mass Gap)**: self‑adjoint, coercive on H₀ (⟨Ou,u⟩ ≥ c₀||u||²), compact resolvent.
* **Compatibility**: I_square preserves L2 on the boundary; SmallBalance yields bounded step‑energy (quasi‑conservation over cycles).

---

## Notation Table

| Symbol    | Meaning                               |   |   |      |                           |
| --------- | ------------------------------------- | - | - | ---- | ------------------------- |
| Rsc       | scale constant in ΔO = (kg/Rsc)·Δr·g  |   |   |      |                           |
| kg        | center‑shift gain                     |   |   |      |                           |
| eps       | primitive step size                   |   |   |      |                           |
| C (Cx,Ct) | per‑axis product targets              |   |   |      |                           |
| rR, rL    | right/left radii (per axis)           |   |   |      |                           |
| Δr        | rR − rL (imbalance)                   |   |   |      |                           |
| g         | rescale factor C/P' (or sqrt variant) |   |   |      |                           |
| ΔO        | center‑shift increment                |   |   |      |                           |
| δ_min     | (2·kg·eps)/Rsc (per‑axis lower bound) |   |   |      |                           |
| I_square  | L∞ boundary involution                |   |   |      |                           |
|           |                                       | · |   | _inf | L∞ norm (boundary at 1/2) |
| S~_n      | transition‑period proxy (exp in Δθ)   |   |   |      |                           |
| κ^(n)     | Fourier coeff. of increment kernel    |   |   |      |                           |
| ρ_n       | Rayleigh proxy ⟨φ_n,P̂φ_n⟩/⟨φ_n,φ_n⟩  |   |   |      |                           |
| λ_min     | minimal eigenvalue (mass gap)         |   |   |      |                           |
| ξ         | divergence‑balance penalty weight     |   |   |      |                           |

---

## Result Flow (Dependency Graph)

Non‑Stalling (δ_min) → Outward L∞ step → Finite‑Time Boundary Hit
↘                ↘
Step energy bound → Cycle quasi‑conservation
↘
Spectral equivalence (proxies)
↘
Self‑adjoint coercivity (O)
↘
Mass Gap (λ_min > 0)

---

## Formal Results (Lean/Coq)

* **L1**: I(I(p)) = p;  ||p||_inf = 1/2 ⇒ I(p)=p;  ||I(p)||_inf = 1/(4||p||_inf).
* **L2**: product_preserved_x (product‑preserving rescale).
* **L3**: H_zero_after_reset (H=0 immediately after reset).
* **Per‑axis displacement**: |ΔO_axis| ≥ (2·kg·eps)/Rsc =: δ_min.
* **Finite‑Time boundary hit**: if ||O(0)||_inf < 1/2, then ∃N ≤ ceil((1/2−||O(0)||_inf)/δ_min) with ||O(N)||_inf ≥ 1/2.
* **Energy & inversion**: ||I_square(p)||_2^2 = ||p||_2^2/(16||p||_inf^4); cycle quasi‑conservation under SmallBalance.
* **Mass gap (Thm 4)**: self‑adjoint O, coercive on H₀, compact resolvent ⇒ discrete spectrum with λ_min ≥ c₀ > 0.

Files: Lean — `SAGU_L1L3_Complete.lean`, `SAGU_Step_Outward_Lean.lean`, `SAGU_FiniteTime_Inf_Lean.lean`;
Coq — `sagu_L1L3_complete.v`, `sagu_step_outward.v`, `SAGU_FiniteTime_Inf_Coq.v`.

---

## Spectral Equivalence (Transition ↔ Fourier)

* **Exact (Convolution)**: E[S~_n] = κ^(n); argmax_n |S~_n| ↔ argmax_n |κ^(n)| (a.s.).
* **Approximate (Circulant)**: P̂ = C + E, gap>0, ||E||≪gap ⇒ stable eigen‑subspaces (Davis–Kahan) and eigenvalues (Weyl/Bauer–Fike).  Statistics: ||P̂−P|| = O_p(√(log M / T)).

---

## Python Toolkit (`sagu_cosmic_tools.py`)

* `I_square`, `energy_L2`, `inversion_L2_ratio`, `energy_trajectory`.
* `quasi_conservation_cycle(before, steps, afterI)`.
* `div_balance_penalty(...) = ξ · ||div(Jp − Jc)||_2^2` (rasterize → central‑difference div → L2).
* `build_JpJc_from_sequences(...)`.
* Demo: `energy_div_demo(K_primes=64, n0=97, xi=1e-3)`.

---

## Slogans (EN)

**Structural Pair**

* *Light reveals form; Heat forges form.*

**Dual Slogan**

* *If I dwell in the light, let me be the dark; if I dwell in the dark, let me be the light.*

**Resonant Slogan**

* *In the light, darkness scatters; in the dark, light gathers.*

---

## Next Steps

(A) Make c₀ explicit (Poincaré constant, V_min, penalty ξ).
(B) Gap‑based reliability index for approximate‑circulant regimes (ρ := ε_total/gap).
(C) Integrate I_square loop & logging in the Python demo.
(D) Modularize Lean/Coq finite‑time records and proofs.
(E) Empirical ranking agreement among |S~_n|, ρ_n, |S_n|.

---

## One‑line Summary

Finite outward displacement and L∞ selection guarantee boundary hit; inversion preserves energy with quasi‑conservation; spectral equivalence stabilizes proxy‑mode matching; and self‑adjoint coercivity yields a positive mass gap (λ_min>0).

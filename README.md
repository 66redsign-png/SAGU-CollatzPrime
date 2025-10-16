# SAGU x Collatz–Prime: Formal Results & Toolkit (v1)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17365703.svg)](https://doi.org/10.5281/zenodo.17365703)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license)
![status](https://img.shields.io/badge/status-research--prototype-blue)

> **Purpose.** ASCII-first digest + runnable toolkit for
> SAGU (square inversion / 4-sphere) with Collatz–Prime drivers.

## Quick start

```bash
# 1) Create & activate virtualenv (optional)
# macOS / Linux
python -m venv .venv && source .venv/bin/activate
# Windows (PowerShell)
python -m venv .venv; .\.venv\Scripts\Activate.ps1
# Windows (CMD)
python -m venv .venv && .\.venv\Scripts\activate.bat

# 2) Install dependencies (requirements.txt may be empty)
pip install -r requirements.txt

# 3) Mini demo (ASCII dashboard + energy/divergence checks)
python - <<'PY'
from sagu_cosmic_tools import energy_div_demo
print(energy_div_demo(K_primes=64, n0=97, xi=1e-3))
PY
```

## Repo layout (suggested)

```
.
├─ README.md
├─ CITATION.cff
├─ LICENSE
├─ .gitignore
├─ .zenodo.json
├─ .github/workflows/ci.yml
├─ spec/
│  └─ cosmic_frame_spec_v1_1.md
├─ toolkit/
│  └─ sagu_cosmic_tools.py
└─ formal/
   ├─ SAGU_Chain_Complete_Lean.lean
   ├─ lean_energy_snippets.lean
   ├─ sagu_chain_complete.v
   └─ coq_energy_snippets.v
```

## Assumptions (exact)

- Positivity: `Rsc, kg, eps, C, rR, rL > 0`
- Product cap: `C ≥ rR·rL`
- SmallBalance: `eps ≤ a·sqrt(rR·rL)`, `|rR−rL| ≤ b·sqrt(rR·rL)`, `0 < a < 1/2`, `0 ≤ b < 1/2`
- Aligned toggle: `s = sign(rR−rL)` (tie → outward by `sign(O)`)
- Rescale factor: `g = sqrt(C / P') ≥ 1` with `P'=(rR+eps·s)(rL−eps·s)`

## Python Toolkit

- `I_square`, `energy_L2`, `inversion_L2_ratio`, `energy_trajectory`
- `quasi_conservation_cycle(before, steps, afterI)`
- `div_balance_penalty(...) = ξ · ||div(Jp − Jc)||_2^2`
- `build_JpJc_from_sequences(...)`
- Demo: `energy_div_demo(K_primes=64, n0=97, xi=1e-3)`

## Contact

- Maintainer: **SANG JUNG LEE** (이상전)
- Email: <redsign66@naver.com>
- Issues: https://github.com/66redsign-png/SAGU-CollatzPrime/issues

## License

MIT. See `LICENSE`.

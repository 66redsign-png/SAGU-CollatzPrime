SAGU x Collatz–Prime: Formal Results & Toolkit
A compact, reproducible package: math notes (LaTeX), proof sketches (Lean/Coq), and a small Python demo.
Quick Start (Python)
1) Create and activate a virtual environment (optional)
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate

2) Install dependencies
pip install -r requirements.txt

3) Run the mini demo
python - <<'PY'
from sagu_cosmic_tools import energy_div_demo
print(energy_div_demo())
PY
Repo Layout
/lean/   SAGU_L1L3_Complete.lean, SAGU_Step_Outward_Lean.lean, SAGU_FiniteTime_Inf_Lean.lean, lean_energy_snippets.lean
/coq/    sagu_L1L3_complete.v, sagu_step_outward.v, SAGU_FiniteTime_Inf_Coq.v, coq_energy_snippets.v
/python/ sagu_cosmic_tools.py, demos/energy_div_demo.ipynb
/latex/  SAGU_Formal_Notes_v0_4.tex
/docs/   SAGU_Project_Summary_v1.md, SAGU_Project_Summary_v1_EN.md
LICENSE, README.md, CITATION.cff, requirements.txt
What this repo contains
Formal notes: convolution equivalence, finite-time boundary hit (L∞), energy quasi-conservation, mass-gap statement.
Lean/Coq: L1–L3 (no sorry/Admitted), outward-step bound, finite-time hit, energy snippets.
Python: inversion/energy/divergence utilities; one-call demo energy_div_demo().

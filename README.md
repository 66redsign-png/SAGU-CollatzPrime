# SAGU x Collatz–Prime: 공식 결과 및 툴킷

간결하고 재현 가능한 패키지: 수학 노트(LaTeX), 증명 스케치(Lean/Coq), 간단한 Python 데모.

## 빠른 시작 (Python)

```bash
# 1) 가상환경 생성/활성화 (선택)
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 2) 의존성 설치
pip install -r requirements.txt

# 3) 미니 데모 실행
python - <<'PY'
from sagu_cosmic_tools import energy_div_demo
print(energy_div_demo())
PY

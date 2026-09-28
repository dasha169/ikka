IKKA: Inversion Classification via Critical Anomalies
Topologically motivated anomaly-weighting framework for robust visual servoing under distribution shift.

Overview
IKKA introduces a topological anomaly weight

W(x)=E(x)⋅T(x)⋅M(x) where:

E(x) — local extremality (error magnitude + tracker confidence drop)
T(x) — boundary transversality (gradient non-alignment across class probabilities)
M(x) — multi-scale persistence (sublevel-set persistent homology of the error signal, with Cohen–Steiner–Edelsbrunner–Harer stability)
The weight modulates control updates near ambiguous decision regions. On a 230-run Raspberry Pi 4 benchmark, IKKA reduces the 95th-percentile lateral error by 24 % under stress conditions while increasing throughput from 20.0 to 24.8 Hz.

Repository structure
ikka/├── weight.py # W(x) = E(x) · T(x) · M(x)├── extremality.py # E component├── transversality.py # T component├── persistence.py # M component (sublevel-set persistent homology)└── control.py # bounded IBVS yaw-rate commandtests/└── test_weight.py # smoke testsanalysis.py # benchmark replay over manifest.csvmanifest.csv # 230-run experiment manifestrequirements.txtLICENSE # MIT

Installation
git clone https://github.com/dasha169/ikka.gitcd ikkapip install -r requirements.txt
Reproducing the benchmark
python analysis.py --manifest manifest.csv \    --input out_logs/ \    --output artefacts/
This regenerates the figures and statistics in the paper from the per-run logs. The 230-run logs are available from the author on request; an archived data release with a DOI is in preparation.

Counterexample (IKKA vs. SVM)
The synthetic three-class counterexample (Section 6 of the paper) is reproducible via:

python -m ikka.examples.svm_vs_ikka
It constructs a Wada-like triple-boundary junction at the origin and shows that IKKA identifies points an order of magnitude closer to the topologically indispensable junction than SVM support vectors.

Hardware
Raspberry Pi 4B (4 GB RAM)
Pi Camera Module V2
QVGA (320 × 240 px), CPU only
IKKA per-frame overhead: ≈ 1.4 ms
Citation
@article{ikka2026,  title   = {IKKA: Inversion Classification via Critical Anomalies for Robust Visual Servoing},  author  = {Pavlenko, Darya},  journal = {arXiv preprint arXiv:2604.08754},  year    = {2026}}
License
MIT — see LICENSE.

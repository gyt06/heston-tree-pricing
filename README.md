# Heston Option Pricing: 2D Recombining Tree & Convergence Benchmarking

European option pricing under the **Heston stochastic volatility model**, centred on a two-dimensional recombining tree implementation and a systematic benchmarking study against finite-difference (FDM) and Monte Carlo (MC) methods.

This repository contains **my individual contributions** to an Imperial College London M2R group research project (Group 51; module led by Harry Zheng) that compared numerical methods for option pricing under Black–Scholes and Heston dynamics and produced a 50-page technical report defended before a panel of professors.

## My contributions

- **The 2D recombining tree pricer** (`heston_tree.py`): builds a recombining grid over log-price and variance, prices by backward induction, uses bilinear interpolation for off-grid transition targets, and applies a full-truncation scheme so the variance process stays positive.
- **The convergence benchmarking** (`benchmarks/Findings.ipynb`): I designed and ran the experiments comparing the tree against FDM and Monte Carlo, including a stability heatmap that maps the numerical "explosion" boundary across parameter and grid choices, and a log–log efficiency frontier (wall-clock time vs. pricing error) across methods. The Monte Carlo benchmark verifies the expected \(O(M^{-1/2})\) convergence rate.
- **The writing**: I authored the Abstract, Discussion and Conclusion of the group's 50-page report, interpreting the convergence behaviour and the accuracy/cost trade-offs between methods.

## Repository layout

```text
heston-option-pricing/
├── heston_tree.py            # My 2D recombining tree pricer for the Heston PDE
├── benchmarks/
│   └── Findings.ipynb        # My benchmarking notebook: stability heatmap + efficiency frontier (executed, with plots)
├── requirements.txt
└── README.md
```

## Running the code

`heston_tree.py` exposes `heston_tree_european_call(S0, K, T, r, kappa, theta, omega, rho, V0, n, mv, mz, mode)`, returning the price of a European call or put under Heston dynamics. `benchmarks/Findings.ipynb` reproduces the stability and efficiency-frontier figures.

Dependency note: the benchmarking notebook cross-checks against the group's shared pricing package (`src/pricing`, which hosts the FDM and Monte Carlo pricers) in the original project repository. That package is the group's joint code and is not redistributed here.

## Team credits

Group project with clearly separated components: FDM implementations by Alec and Justin, Monte Carlo by Justin, a semi-closed-form characteristic-function method by Victor, and a deep-learning extension by Justin. Only my own code and writing are published in this repository.

## Tech

Python, NumPy, SciPy, Matplotlib, Seaborn, Pandas.

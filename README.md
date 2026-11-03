# Quantum Rebate Research

Exploratory research into whether quantum algorithms offer a useful new way to design **retroactive volume rebate programs** in B2B commercial strategy. The work is a single Jupyter notebook, [`quantum-research.ipynb`](quantum-research.ipynb), built on NVIDIA's [CUDA-Q](https://nvidia.github.io/cuda-quantum/) platform.

## What the notebook covers

Each Part has a theory section followed by a Python cell that runs the examples in CUDA-Q.

| Part | Topic |
|---|---|
| 1 | Retroactive volume rebates: a 3-tier example, quarterly true-ups and the tier cliff |
| 2 | Qubits, the Bloch sphere, CNOT and entanglement |
| 3 | Quantum gates, interference and circuits |
| 4 | The Bernoulli random variable, and loading a probability into a qubit |
| 5 | The Grover operator and amplitude amplification |
| 6 | Quantum amplitude estimation, compared with classical sampling |
| 7 | A quantum approach to constructing rebate programs |

**Part 7** adapts the quantum credit risk model of Egger et al. (2021). Each customer gets one qubit, which measures 1 if they reach the top tier, and a shared demand driver links them. Amplitude estimation then estimates the probability that Tier 3 true-ups exceed the rebate budget. That risk constrains the choice of program design.

## Key finding

In a retroactive program, the hidden risk is correlated true-ups: a strong year for a shared driver pushes many customers over the tier cliff at once. In the illustrative example, the most generous design seems to breach the budget 3% of the time if customers are treated as independent. When customers share a demand driver, that rises to 8%, which is over the 5% risk limit.

## Running the notebook

Requires Python 3.10 or later. CUDA-Q installs with pip on Linux and on Apple Silicon Macs.

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
```

Open the notebook with the `.venv` kernel and **run the cells in order**, because later Parts reuse functions from earlier ones. A full run takes about a minute on a laptop CPU.

CUDA-Q uses its CPU simulator by default. On a machine with a supported NVIDIA GPU, `cudaq.set_target("nvidia")` switches to the GPU simulator.

## Caveats

- **This is exploratory research.** All quantum results come from a classical simulator, and no quantum advantage is claimed.
- **The model's parameters are illustrative.** These include customer volumes, the correlation ρ, the budget and the risk limit. They are not calibrated to real data.
- The single-factor model in Part 7 can also be solved exactly by classical methods. A quantum advantage would need richer dependence between customers. See Part 7.7.

## References

- Egger, D. J., García Gutiérrez, R., Mestre, J. C. and Woerner, S. (2021). *Credit Risk Analysis Using Quantum Computers.* IEEE Transactions on Computers, 70(12), 2136–2145. arXiv:1907.03044.
- Woerner, S. and Egger, D. J. (2019). *Quantum Risk Analysis.* npj Quantum Information, 5, 15.
- Suzuki, Y. et al. (2020). *Amplitude Estimation Without Phase Estimation.* Quantum Information Processing, 19, 75.

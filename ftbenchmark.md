---
title: Fault-Tolerant Benchmark Applications
---

# Fault-Tolerant Benchmark Applications

This page collects benchmark circuits and experiments for fault-tolerant
quantum computing. Each section focuses on a different application family
and lists concrete implementations with code parameters, noise / decoder
assumptions, and basic performance metrics.

The tables below use the following columns:

1. **Name** – short label for the benchmark instance  
2. **Code (type, parameters)** – e.g., surface code `d=3`, Steane `[[7,1,3]]`  
3. **Noise / Decoder** – noise model and decoding strategy  
4. **Qubits** – total physical qubit count (data + ancilla/helper)  
5. **Fidelity** – logical success probability or 1 − logical error rate  
6. **GitHub** – link to code or configuration

---

## 1. Logical Gates

Logical gate benchmarks study encoded single- and two-qubit gates
(e.g., logical `X`, `Z`, `H`, `S`, `T`, `CNOT`) implemented on top of a
quantum error-correcting code. These benchmarks are useful for
comparing different codes, layouts, and decoders under the same physical
noise assumptions.

### Benchmark Instances

| Name | Code (type, parameters) | Noise / Decoder | Qubits | Fidelity | GitHub |
|------|-------------------------|-----------------|--------|----------|--------|
| Logical CNOT (Surface d=3) | Surface code, rotated lattice, distance d=3 | Depolarizing p=1e-3 (2-qubit), MWPM decoder (PyMatching) | 49 | 0.992 | [Link](https://github.com/USERNAME/REPO1) |
| Logical T via MSD (Steane) | Steane code `[[7,1,3]]` with magic-state distillation | Biased dephasing `p_Z = 2e-3`, lookup-table decoder | 35 | 0.985 | [Link](https://github.com/USERNAME/REPO2) |
| Repeated Logical Id (Bacon–Shor) | Bacon–Shor code `n_x=3, n_z=3` | Circuit-level depolarizing p=5e-4, belief-propagation decoder | 27 | 0.998 | [Link](https://github.com/USERNAME/REPO3) |

> Replace `USERNAME/REPO*` with your actual repositories or configs.

---

## 2. Shor’s Algorithm

Shor’s algorithm factors an integer using modular exponentiation and a
quantum Fourier transform (QFT). Fault-tolerant benchmarks typically
use small composite numbers (e.g., 15, 21) encoded in QEC codes and
focus on the cost and reliability of modular arithmetic plus QFT under
realistic noise.

### Benchmark Instances

| Name | Code (type, parameters) | Noise / Decoder | Qubits | Fidelity | GitHub |
|------|-------------------------|-----------------|--------|----------|--------|
| Shor N = 15 (Logical) | Surface code d=3 for all logical qubits | Circuit-level depolarizing p=1e-3, MWPM decoder | 128 | 0.93 | [Link](https://github.com/USERNAME/REPO4) |
| Shor N = 21 (Hybrid Layout) | Mixed surface codes d=3 / d=5 for work registers | Spatially correlated noise (`p_2q=1e-3`), tensor-network decoder | 256 | 0.89 | [Link](https://github.com/USERNAME/REPO5) |
| Shor N = 15 (Color Code) | 2D color code distance d=3 | Biased dephasing (`p_Z > p_X`), MWPM-style color decoder | 162 | 0.91 | [Link](https://github.com/USERNAME/REPO6) |

---

## 3. QAOA

The Quantum Approximate Optimization Algorithm (QAOA) is a
variational algorithm for combinatorial optimization (e.g., MaxCut,
Max-2-SAT). Fault-tolerant QAOA benchmarks emphasize the overhead of
implementing parameterized layers at logical level, including logical
ZZ and X mixers, and measure how logical error rates affect the final
approximation ratio.

### Benchmark Instances

| Name | Code (type, parameters) | Noise / Decoder | Qubits | Fidelity | GitHub |
|------|-------------------------|-----------------|--------|----------|--------|
| QAOA MaxCut (p = 1, 8 nodes) | Surface code d=3 (one logical per graph vertex) | Depolarizing p=1e-3, MWPM decoder | 96 | 0.95 | [Link](https://github.com/USERNAME/REPO7) |
| QAOA MaxCut (p = 2, 12 nodes) | Surface code d=5, lattice-surgery entangling gates | Circuit-level depolarizing p=5e-4, MWPM decoder | 320 | 0.92 | [Link](https://github.com/USERNAME/REPO8) |
| QAOA Portfolio Opt. (p = 1) | Steane `[[7,1,3]]` logical qubits for cost Hamiltonian | Asymmetric noise (`T_1`, `T_2`-derived channels), lookup-table decoder | 70 | 0.90 | [Link](https://github.com/USERNAME/REPO9) |

---

## 4. Grover’s Algorithm

Grover’s search algorithm provides quadratic speedup for unstructured
search. Fault-tolerant Grover benchmarks typically implement an oracle
and diffusion operator using logical gates, then measure how many Grover
iterations can be performed before logical errors dominate.

### Benchmark Instances

| Name | Code (type, parameters) | Noise / Decoder | Qubits | Fidelity | GitHub |
|------|-------------------------|-----------------|--------|----------|--------|
| Grover 1-marked item (n = 4) | Surface code d=3, logical oracle via Toffoli synthesis | Depolarizing p=1e-3, MWPM decoder | 80 | 0.96 | [Link](https://github.com/USERNAME/REPO10) |
| Grover 1-marked item (n = 6) | Surface code d=5, helper-qubit-heavy ancilla factory | Correlated 2-qubit noise, tensor-network decoder | 240 | 0.93 | [Link](https://github.com/USERNAME/REPO11) |
| Grover oracle with QEC-protected data | Bacon–Shor logical data, unencoded ancilla helpers | Amplitude-damping + dephasing, belief-propagation decoder | 112 | 0.90 | [Link](https://github.com/USERNAME/REPO12) |

---

You can:

- Adjust intros to match your own terminology.
- Replace the placeholder repos (`USERNAME/REPO*`) with your actual
  GitHub links.
- Add or remove rows in each table as your benchmark suite grows.

# Quantum Computing Algorithms & Hardware Experiments

[![Qiskit](https://img.shields.io/badge/Qiskit-1.x-6929C4?logo=qiskit&logoColor=white)](https://qiskit.org/)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://python.org)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/preesr/quantum-computing)

Welcome to the **Quantum Computing** repository! This repository contains interactive Jupyter Notebooks implementing fundamental quantum algorithms, quantum communication protocols, quantum game theory, and hardware experiments using **Qiskit 1.x**, **Qiskit Aer**, and **IBM Quantum Cloud Services (`qiskit-ibm-runtime`)**.

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure & Notebook Summaries](#repository-structure--notebook-summaries)
  - [1. Deutsch's Algorithm (1-Bit Query Reduction)](#1-deutschs-algorithm-1-bit-query-reduction)
  - [2. Deutsch-Jozsa & Bernstein-Vazirani Algorithms](#2-deutsch-jozsa--bernstein-vazirani-algorithms)
  - [3. Nonlocal CHSH Game (Quantum Advantage)](#3-nonlocal-chsh-game-quantum-advantage)
  - [4. Quantum Teleportation Protocol](#4-quantum-teleportation-protocol)
  - [5. Quantum Circuit Construction & Transpilation](#5-quantum-circuit-construction--transpilation)
  - [6. Quantum Energy Measurement & Hamiltonian Observables](#6-quantum-energy-measurement--hamiltonian-observables)
- [Prerequisites & Installation](#prerequisites--installation)
- [IBM Quantum Cloud Credentials](#ibm-quantum-cloud-credentials)
- [Summary Table](#summary-table)

---

## Overview

This repository demonstrates the principles of quantum information processing, phase kickback, quantum entanglement, quantum nonlocality, state verification, and Hamiltonian expectation estimation:

- **Quantum Oracles & Query Complexity:** Demonstrates exponential or polynomial query reductions over classical algorithms (Deutsch, Deutsch-Jozsa, Bernstein-Vazirani).
- **Entanglement & Nonlocality:** Validates quantum supremacy in game theory via the CHSH inequality, exceeding the classical 75% win-probability limit.
- **Quantum State Teleportation:** Implements end-to-end qubit teleportation over classical channels using shared EPR pairs ($\Phi^+$ state).
- **Quantum Hardware Execution:** Shows how to transpile circuits, target least-busy 127+ qubit IBM Quantum processors, and execute primitives like `SamplerV2` and `EstimatorV2`.

---

## Repository Structure & Notebook Summaries

### 1. Deutsch's Algorithm (1-Bit Query Reduction)
**Files:**
- [`Query_reduction_with_Deutsch's_algorithm.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Query_reduction_with_Deutsch's_algorithm.ipynb)


- **Core Concept:** Resolves whether a single-bit boolean function $f: \{0,1\} \rightarrow \{0,1\}$ is **constant** or **balanced** using a **single quantum query**, whereas classical algorithms strictly require 2 queries.
- **Key Techniques:**
  - Initialization of an ancilla qubit in the $|-\rangle$ state for phase kickback ($X$ followed by Hadamard $H$).
  - Oracle construction for all 4 possible 1-bit boolean functions.
  - Single-shot execution via `AerSimulator`.

---

### 2. Deutsch-Jozsa & Bernstein-Vazirani Algorithms
**File:** [`Deutsch_Jozsa_Algorithm_Implementation.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Deutsch_Jozsa_Algorithm_Implementation.ipynb)

- **Core Concept:** Generalizes query reduction to $n$-qubit functions and secret bitstring discovery.
- **Key Components:**
  - **Deutsch-Jozsa Algorithm:** Evaluates an $n$-bit function $f: \{0,1\}^n \rightarrow \{0,1\}$ guaranteed to be either constant or balanced using a single query.
  - **Bernstein-Vazirani Algorithm:** Finds a hidden binary string $s \in \{0,1\}^n$ for a function $f(x) = s \cdot x \pmod 2$ in 1 query (versus $n$ classical queries).
- **Key Techniques:**
  - Multi-qubit Hadamard transformation $H^{\otimes n}$.
  - Little-endian bit ordering correction for Qiskit indexing.
  - Phase kickback via function composition `qc.compose(...)`.

---

### 3. Nonlocal CHSH Game (Quantum Advantage)
**File:** [`Improve_win_probability_Nonlocal_CHSH.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Improve_win_probability_Nonlocal_CHSH.ipynb)

- **Core Concept:** Demonstrates quantum nonlocality via the Clauser-Horne-Shimony-Holt (CHSH) game.
- **Key Insights:**
  - **Classical Bound:** Any deterministic or probabilistic classical strategy has a maximum win probability of **$75\%$** ($0.75$).
  - **Quantum Strategy:** By sharing a Bell pair $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ and measuring along optimized rotation angles, the win probability increases to **$\cos^2(\pi/8) \approx 0.85\%$**.
- **Key Techniques:**
  - Parameterized $R_y(\theta)$ rotation gates for basis switching.
  - Comparative monte-carlo simulation over 1,000 games comparing classical vs. quantum strategies.

---

### 4. Quantum Teleportation Protocol
**File:** [`Quantum_Teleportation.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Quantum_Teleportation.ipynb)

- **Core Concept:** Teleports an unknown arbitrary single-qubit quantum state $|\psi\rangle$ from Alice to Bob using an EPR pair and two classical bits.
- **Key Workflow:**
  1. State Preparation: Applies an arbitrary random unitary gate `UGate(\theta, \phi, \lambda)` to qubit $Q$.
  2. Bell Measurement: Alice performs Bell-basis measurement on qubit $Q$ and her half of the entangled pair $A$.
  3. Classical Correction: Bob applies conditional $X$ and $Z$ gates based on Alice's classical measurement results.
  4. Verification: Applies $U^\dagger$ to Bob's qubit $B$; observing $|0\rangle$ with 100% probability confirms exact state reproduction.
- **Key Techniques:**
  - `marginal_distribution` filtering on classical measurement registers.
  - `UGate` matrix visualization using `array_to_latex`.

---

### 5. Quantum Circuit Construction & Transpilation
**File:** [`Quantum_Circuit.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Quantum_Circuit.ipynb)

- **Core Concept:** Complete tutorial on building, transpiling, and executing quantum circuits on real quantum processing units (QPUs) vs local simulators.
- **Key Features:**
  - Bell state $|\Phi^+\rangle$ generation.
  - Pass manager creation using Qiskit preset transpilation managers (`generate_preset_pass_manager`).
  - Execution on real 127+ qubit IBM Quantum backends via `QiskitRuntimeService` and `SamplerV2`.
  - Fallback local simulation with `AerSimulator`.

---

### 6. Quantum Energy Measurement & Hamiltonian Observables
**File:** [`Quantum Experiment - Calculate Energy.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Quantum Experiment - Calculate Energy.ipynb)

- **Core Concept:** Variational quantum eigensolver concepts and observable expectation estimation.
- **Key Details:**
  - Prepares the singlet state $|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|10\rangle - |01\rangle)$.
  - Defines a 2-qubit spin Hamiltonian $H = J Z_1 Z_2 + h_x (X_1 + X_2)$ using Qiskit's `SparsePauliOp`.
  - Runs Qiskit IBM Runtime `EstimatorV2` primitive to extract expectation values $\langle \Psi^- | H | \Psi^- \rangle$.
  - Includes transpilation layout mappings `obs.apply_layout(...)`.

---

## Prerequisites & Installation

### Requirements
- Python 3.10+
- Qiskit 1.x
- Qiskit Aer
- Qiskit IBM Runtime
- Matplotlib, NumPy

### Installation
Clone this repository and install the dependencies:

```bash
git clone https://github.com/preesr/quantum-computing.git
cd quantum-computing
pip install "qiskit[visualization]" qiskit-aer qiskit-ibm-runtime numpy matplotlib
```

---

## IBM Quantum Cloud Credentials

To execute circuits on physical IBM Quantum QPUs, save your IBM Quantum API Token once in Python:

```python
from qiskit_ibm_runtime import QiskitRuntimeService

# Save your token locally (only needed once)
QiskitRuntimeService.save_account(
    channel="ibm_quantum_platform",
    token="YOUR_IBM_QUANTUM_API_TOKEN",
    overwrite=True,
    set_as_default=True
)

# Initialize service and select least-busy QPU
service = QiskitRuntimeService()
backend = service.least_busy(operational=True, simulator=False, min_num_qubits=127)
print("Connected QPU:", backend.name)
```

---

## 📊 Notebook Summary Table

| Notebook | Algorithm / Focus | Qubits | Simulator Support | IBM Hardware Support |
| :--- | :--- | :---: | :---: | :---: |
| [`Query_reduction_with_Deutsch's_algorithm.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Query_reduction_with_Deutsch's_algorithm.ipynb) | Deutsch's Algorithm (1-Bit Query) | 2 | ✅ | ✅ |
| [`Deutsch_Jozsa_Algorithm_Implementation.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Deutsch_Jozsa_Algorithm_Implementation.ipynb) | Deutsch-Jozsa & Bernstein-Vazirani | $n+1$ | ✅ | ✅ |
| [`Improve_win_probability_Nonlocal_CHSH.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Improve_win_probability_Nonlocal_CHSH.ipynb) | CHSH Nonlocal Game (~85.3% Win Rate) | 2 | ✅ | ✅ |
| [`Quantum_Teleportation.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Quantum_Teleportation.ipynb) | Quantum State Teleportation | 3 | ✅ | ✅ |
| [`Quantum_Circuit.ipynb`](file:///Users/preethi/Documents/Antigravity%20Projects/quantum-computing/Quantum_Circuit.ipynb) | Bell Pair & QPU Transpilation | 2 | ✅ | ✅ |
| [`Quantum Experiment - Calculate Energy.ipynb`] | Singlet Energy Estimation (`EstimatorV2`) | 2 | ✅ | ✅ |

---

## 📄 License

This repository is maintained for educational and research purposes in quantum information science and quantum computation.

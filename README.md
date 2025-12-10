# QSBS: Combinatorial Optimization for Resource-Constrained Scheduling

![Optimization](https://img.shields.io/badge/Algorithm-Combinatorial_Optimization-blue)
![Status](https://img.shields.io/badge/Status-Research_Prototype-green)
![Math](https://img.shields.io/badge/Focus-NP--Hard_Heuristics-orange)

## 📖 Overview

This repository contains the implementation and simulation framework for **Query-Set-Based Scheduling (QSBS)**, a heuristic algorithm designed to solve complex scheduling problems in bandwidth-constrained environments.

Originally developed for my Master's Thesis, this project addresses the **NP-hard problem** of mapping compound data requests ("Query Sets") onto limited broadcast channels to minimize average access latency. The core logic involves optimizing data placement and replication under strict resource constraints—a problem class sharing significant mathematical isomorphism with **QUBO (Quadratic Unconstrained Binary Optimization)** and **Job-Shop Scheduling** problems often targeted by modern quantum annealing and QAOA approaches.

## 🚀 Key Algorithms

This project implements and benchmarks three distinct scheduling heuristics:

### 1. QSBS (Query-Set-Based Scheduling)

A novel heuristic that treats a set of requested items as a "Compound Data Item" (CDI). It utilizes **partitioning logic** to cluster correlated data, minimizing the "tuning time" (active listening duration) for clients.

- **Constraint:** Finite channel bandwidth and cycle length.
- **Optimization Target:** Minimize global average access time across Poisson and Normal distribution request patterns.

### 2. CBS (Coherence-Based Scheduling)

Focuses on the "Coherence Degree" of data items—a metric defining how "close" related items are in a temporal stream.

- **Mechanism:** Reduces fragmentation of related data blocks.
- **Application:** Equivalent to minimizing "swap" or "transport" costs in hardware topology mapping.

### 3. iPBA (Improved Placement-Based Allocation)

An enhancement over the standard Placement-Based Allocation (PBA) algorithm.

- **Innovation:** Introduces a priority weighting function based on the square root of probability-to-size ratios ($\sqrt{P/S}$), mathematically derived from Lagrange multiplier optimization of the access time equation.

## 🛠️ Mathematical Foundations

The code is backed by rigorous analytical modeling (detailed in `docs/Thesis.pdf`).

- **Derivation of Lower Bounds:** Formulated the theoretical lower bound for access time using partial derivatives to optimize replica frequencies.
- **Complexity Management:** ADDRESSED the $2^n$ state-space explosion of compound queries by reducing them to "Extended Query Profiles."

> **Equation 4.16 (Near-Optimal Access Time):**
> Derived a general equation for multiple query sets with replication, proving that optimal scheduling priority is proportional to $\sqrt{P_a/n_a}$.

## 📊 Simulation & Benchmarking

A custom **Discrete Event Simulation (DES)** engine was built to validate these algorithms.

- **Parameters:** Tested against $N=1024+$ items, varying channel counts ($K=4..64$), and Zipfian access distributions ($\theta=0.4..1.6$).
- **Results:** QSBS demonstrated superior performance in highly skewed (Zipfian) environments, effectively handling "hot spot" contention.

## ⚡ Relevance to Quantum Algorithm Design

While originally applied to wireless networks, the underlying mathematics of this project are directly applicable to the **Quantum SDK / Algorithm Design** role at Postquant Labs:

1.  **Combinatorial Optimization:** The problem of scheduling variable-size items on $K$ channels is mathematically similar to **mapping quantum circuits** to physical qubits with limited connectivity, or solving **Bin Packing/Knapsack problems** via QAOA.
2.  **Hybrid Pipelines:** The architecture separates the _optimization engine_ (the scheduler) from the _execution layer_ (the broadcast simulation), mirroring **Hybrid Quantum-Classical** workflows where a classical CPU handles parameters and a QPU handles the cost function evaluation.
3.  **SDK Design Principles:** The codebase emphasizes modularity, allowing researchers to plug in different "Sort" functions (heuristics) to test against the same simulation harness—a key requirement for building user-friendly Quantum SDKs.

## 👨‍💻 Author

**Jacob Lin**
_Algorithm Engineer & Full-Stack Developer_
[LinkedIn](https://www.linkedin.com/in/dachunglin) | [Email](mailto:overcomerlin@gmail.com)

_"I build systems that solve hard math problems."_

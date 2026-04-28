# Emerging Technologies Assessment: Classical vs Quantum Algorithms
### Deutsch-Jozsa Problem — ATU Galway | BSc (Hons) Computing

> This repository contains the assessed coursework for the Emerging
> Technologies module. It investigates the computational advantage of
> quantum algorithms over their classical counterparts through a
> systematic implementation of the Deutsch-Jozsa problem using Python
> and Qiskit.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Qiskit](https://img.shields.io/badge/Qiskit-1.x-6929C4?logo=ibm)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)
![Code Style](https://img.shields.io/badge/Code%20Style-PEP8-black)

## Table of Contents
- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Setup Instructions](#setup-instructions)
- [Running the Notebook](#running-the-notebook)
- [Problems Overview](#problems-overview)
- [Data & Reproducibility](#data--reproducibility)
- [Development Standards](#development-standards)
- [References](#references)

## Project Overview

This repository presents a comparative study of classical and quantum computation paradigms through the Deutsch-Jozsa problem, with all implemented solutions contained in `problems.ipynb`. The workflow progresses from classical Boolean testing in Problems 1–2 to quantum oracle construction and algorithm execution in Problems 3–4, enabling direct comparison of query complexity and computational behaviour. The theoretical foundation follows [Deutsch & Jozsa (1992)](https://doi.org/10.1098/rspa.1992.0167) and the [IBM Quantum Learning platform](https://learning.quantum.ibm.com/).

## Repository Structure

```text
emerging_technologies/
│
├── problems.ipynb              # Main notebook — all solutions live here
├── requirements.txt            # Python dependencies for full reproducibility
├── README.md                   # You are here
│
├── /data                       # Auto-generated data outputs
│   ├── p1_random_function_samples.csv   # Sampled Boolean functions (Problem 1)
│   ├── p1_truth_tables.csv              # Full truth tables for verification
│   ├── p2_query_test_results.csv        # Classical query efficiency log
│   ├── p3_oracle_unitaries.json         # Unitary matrices for each oracle
│   ├── p3_statevector_results.json      # Simulated quantum state outputs
│   ├── p4_init_statevector.json         # Part 1 state preparation snapshot
│   ├── p4_deutsch_results.csv           # Part 2 oracle classifications
│   ├── p4_statevector_stages.json       # Part 3 stage-by-stage amplitudes
│   ├── p5_truth_tables.csv              # 4-bit function truth tables (Problem 5)
│   └── p5_dj_results.csv                # Deutsch-Jozsa classifications (Problem 5)
│
├── /img                        # Visualisations and circuit diagrams
│   ├── problem3_oracles.png                       # Problem 3 oracle panel
│   ├── p4_deutsch_circuit_constant_0.png          # Part 2 circuit diagram
│   ├── p4_deutsch_circuit_constant_1.png          # Part 2 circuit diagram
│   ├── p4_deutsch_circuit_identity_balanced.png   # Part 2 circuit diagram
│   ├── p4_deutsch_circuit_negation_balanced.png   # Part 2 circuit diagram
│   ├── p4_amplitude_evolution.png                 # Part 3 amplitude grid
│   ├── p4_measurement_histograms.png              # Part 3 shot histograms
│   ├── p5_dj_circuit_constant_0.png               # Problem 5 circuit diagram
│   ├── p5_dj_circuit_constant_1.png               # Problem 5 circuit diagram
│   ├── p5_dj_circuit_balanced_first_half.png      # Problem 5 circuit diagram
│   ├── p5_dj_circuit_balanced_parity.png          # Problem 5 circuit diagram
│   └── p5_measurement_histograms.png              # Problem 5 shot histograms
│
└── /roughwork                  # Backup and working files (not in version control)
```

All files in `/data` and `/img` are generated automatically when `problems.ipynb` is executed from top to bottom. No manual file creation is required. If any output file already exists, the notebook will overwrite it safely.

## Setup Instructions

These instructions have been tested on macOS, Linux, and Windows (WSL2). Python 3.10 or higher is required.

### 1. Clone the Repository

```bash
git clone https://github.com/PhatTanNguyen45/emerging_technologies.git
cd emerging_technologies
```

### 2. (Recommended) Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies

All required packages are pinned in `requirements.txt` to guarantee consistent behaviour across environments.

```bash
pip install -r requirements.txt
```

Core dependencies include:
- `qiskit` — quantum circuit construction and simulation
- `qiskit-aer` — local quantum simulator backend
- `matplotlib` — circuit visualisation and plotting
- `numpy` — numerical computation
- `pandas` — truth table and results export
- `jupyter` — interactive notebook environment

### 4. Launch the Notebook

```bash
jupyter notebook problems.ipynb
```

Alternatively, open in VS Code with the Jupyter extension or upload to [IBM Quantum Lab](https://quantum.ibm.com/lab) for cloud execution.

## Running the Notebook

Once the notebook is open, select **Kernel → Restart & Run All** to execute all cells sequentially. This will:

1. Create the `/data` and `/img` directories if they do not exist.
2. Generate and export all truth tables and test results to `/data`.
3. Construct, simulate, and visualise all quantum oracle circuits.
4. Save all circuit diagrams to `/img/problem3_oracles.png`.

> ⚠️ **Important**: Always restart the kernel before a full run to
> ensure no residual state from previous executions affects the results.
> This is required for full reproducibility.

## Problems Overview

| Problem | Title | Approach | Key Output | Status |
|---------|-------|----------|------------|--------|
| 1 | Boolean Function Generation | Classical Python | Truth tables -> /data | Complete |
| 2 | Classical Function Testing | Classical Python | Query log -> /data | Complete |
| 3 | Quantum Oracles | Qiskit circuits | Unitary matrices, circuit diagrams | Complete |
| 4 | Deutsch's Algorithm | Qiskit + simulation | Single-query classification, interference plots, audit artifacts | Complete (Part 3 Final) |
| 5 | Deutsch-Jozsa (4-bit) | Qiskit 5-qubit circuit | Truth tables, histograms -> /data /img | Complete |

Problems 1 and 2 establish a classical baseline, demonstrating that deterministic identification of a 4-bit Boolean function requires up to 2^(n-1) + 1 = 9 queries. Problems 3 and 4 show how Deutsch's quantum algorithm solves the equivalent 1-bit problem in a single query, illustrating an exponential separation in query complexity.

## Data & Reproducibility

All data files are generated programmatically within `problems.ipynb` and committed to this repository for independent verification. A reviewer may inspect any `.csv` or `.json` file in `/data` to audit results without re-executing the notebook.

### Large File Policy

No files in this repository exceed GitHub's 100 MB limit. Should future experiments produce large simulation outputs (e.g., statevector data for n > 20 qubits), those files will be excluded via `.gitignore` and auto-downloaded by the notebook using:

```python
import urllib.request, os
if not os.path.exists('data/large_output.csv'):
		urllib.request.urlretrieve(
				"https://<host>/large_output.csv",
				"data/large_output.csv"
		)
```

## Development Standards

This project adheres to the following professional coding standards:

- **PEP 8**: All Python code is formatted to PEP 8 style guidelines, including meaningful variable names, consistent indentation, and line length limits.
- **Docstrings**: Every function includes a Google-style docstring documenting its parameters, return values, and usage examples.
- **Inline Comments**: Comments explain *why* design decisions were made, not just *what* the code does — particularly for gate-level quantum logic.
- **Commit History**: The repository maintains a descriptive commit history that reflects iterative development and refinement rather than single large pushes.
- **Notebook Hygiene**: Cells are ordered logically, outputs are cleared before committing, and the notebook passes a full Restart & Run All without errors.

## References

- Deutsch, D. & Jozsa, R. (1992). *Rapid solution of problems by
	quantum computation*. Proceedings of the Royal Society A.
	https://doi.org/10.1098/rspa.1992.0167

- Nielsen, M. A. & Chuang, I. L. (2010). *Quantum Computation and
	Quantum Information* (10th Anniversary Ed.). Cambridge University Press.
	https://www.cambridge.org/9781107002173

- IBM Quantum Learning — Deutsch-Jozsa Algorithm:
	https://learning.quantum.ibm.com/course/fundamentals-of-quantum-algorithms/quantum-query-algorithms

- Qiskit Documentation:
	https://docs.quantum.ibm.com/

- Python PEP 8 Style Guide:
	https://peps.python.org/pep-0008/

---
*Assessment submission for Emerging Technologies — ATU Galway, 2025/26*
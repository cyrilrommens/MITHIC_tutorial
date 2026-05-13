# MITHIC Workshop Notebooks

This repository contains a set of self-contained Jupyter notebooks that introduce how to compute **multivariate information measures** from data using six different Python libraries. Each notebook is a minimal, runnable example; just enough to install the library, load some data, and compute the core measures it provides.

---

## What's Included

| Notebook | Library | Example measures (non-exhaustive) |
|---|---|---|
| `dit.ipynb` | [`dit`](https://dit.readthedocs.io) | Entropy, Total Correlation, Co-information (exact, from discrete PMFs) |
| `hoi.ipynb` | [`hoi`](https://brainets.github.io/hoi/) | O-information, TC, DTC (KSG estimator, continuous data) |
| `thoi.ipynb` | [`thoi`](https://github.com/Laouen/THOI) | O-information, TC, DTC, S-information (Gaussian copula, fast) |
| `pyinform.ipynb` | [`pyinform`](https://elife-asu.github.io/PyInform/) | Transfer Entropy, Active Information Storage (discrete time series) |
| `jidt.ipynb` | [JIDT](https://github.com/jlizier/jidt) | Transfer Entropy, Active Information Storage (KSG and Gaussian estimators) |
| `idtxl.ipynb` | [IDTxl](https://github.com/pwollstadt/IDTxl) | Causal network inference via multivariate Transfer Entropy + permutation tests |

Each notebook follows the same structure:
1. Brief introduction to the library and its estimator
2. Imports and setup
3. Artificial redundant and synergistic datasets (sanity check)
4. Real data — UCI Wine dataset
5. Visualisation

---

## Prerequisites

- [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or Anaconda
- Git
- Java 17 (only for `jidt.ipynb` and `idtxl.ipynb` — automatically installed by the `.yml` files via `openjdk=17`)

---

## Repository Structure

```
mithic-workshop/
├── dit.ipynb
├── hoi.ipynb
├── thoi.ipynb
├── pyinform.ipynb
├── jidt.ipynb
├── idtxl.ipynb
├── dit.yml
├── hoi.yml
├── thoi.yml
├── pyinform.yml
├── jidt.yml
└── IDTxl.yml
```

Each notebook has a matching `.yml` file that creates an isolated Conda environment with exactly the dependencies it needs.

---

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/mithic2026/MITHIC_TUTORIAL
cd mithic-workshop
```
Alternatively, you can download the desired notebook and its corresponding yml file manually.

### 2. Choose a Notebook and Create Its Environment

Every notebook has its own environment. Pick the one you want to run and follow the instructions below.

#### `dit.ipynb`
```bash
conda env create -f dit.yml
conda activate mithic-dit
```

#### `hoi.ipynb`
```bash
conda env create -f hoi.yml
conda activate mithic-hoi
```

#### `thoi.ipynb`
```bash
conda env create -f thoi.yml
conda activate mithic-thoi
```

#### `pyinform.ipynb`
```bash
conda env create -f pyinform.yml
conda activate mithic-pyinform
```

#### `jidt.ipynb`

JIDT uses `idtxl` only to locate its bundled `infodynamics.jar`. IDTxl must be installed manually after the environment is created because its C extensions require `cython` to be fully available before the build runs, something Conda cannot guarantee when mixing conda and pip installs.

```bash
conda env create -f jidt.yml
conda activate mithic-jidt
git clone https://github.com/pwollstadt/IDTxl.git
cd IDTxl
pip install .
cd ..
```

#### `idtxl.ipynb`

Same manual IDTxl install for the same reason.

```bash
conda env create -f idtxl.yml
conda activate mithic-idtxl
git clone https://github.com/pwollstadt/IDTxl.git
cd IDTxl
pip install .
cd ..
```

> **Note:** use `pip install .` and **not** `python setup.py install`. The legacy egg installer corrupts the `setuptools` namespace and breaks `pkg_resources` at runtime.

### 3. Launch the Notebook

With the environment active, open the notebook in JupyterLab:

```bash
jupyter lab
```

Or open it directly in **Visual Studio Code** with the Jupyter extension, select the matching `mithic-*` kernel from the kernel picker in the top right corner.

---

## Datasets

All notebooks use the same two datasets so methods are comparable across libraries:

**Artificial data** — two controlled three-variable Gaussian systems built from scratch in the notebook:
- *Redundant*: all three variables are noisy copies of one shared source → expected O-information > 0
- *Synergistic*: one variable is the sum of the other two → expected O-information < 0

**Real data** — the [UCI Wine dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_wine.html) (`sklearn.datasets.load_wine`), using the top features ranked by mutual information with the class label. No download required.

---

## Notes

- The notebooks are **introductory examples**, not production pipelines. The goal is to show the install procedure and the minimal API surface of each library.
- If something breaks, that's part of the process. Debug, iterate, and keep exploring.
- Questions and contributions are welcome!

---

*The goal of these notebooks is to develop intuition through hands-on experimentation with information-theoretic tools. Have fun!*

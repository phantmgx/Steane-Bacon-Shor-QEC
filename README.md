# Fault-Tolerant QEC Simulations: Steane [[7,1,3]] and Bacon-Shor

This repository contains circuit-level and phenomenological simulations of quantum error correction (QEC) protocols, focusing on the Steane [[7,1,3]] color code and the Bacon-Shor subsystem code. Simulations are built using `Stim` for fast Clifford simulation, `PyMatching` for MWPM decoding, and `sinter` for parallelized threshold benchmarking.

## Repository Contents

The primary artifact is `Steane_and_Bacon_Shor_Benchmarking.ipynb`, which is structured into two main QEC investigations:

### 1. Steane [[7,1,3]] Logical Memory & Transversal Gates
* **Circuit-Level Noise Model:** Custom implementation of depolarizing and measurement noise parameterized against a physical baseline.
* **Memory Benchmarking:** Multi-round syndrome extraction with proper relative detectors.
* **Fault-Tolerant State Preparation:** Implementation of Goto's 2016 verified $|0\rangle_L$ encoder, using a verification ancilla to prevent weight-2 error cascades.
* **Transversal Operations:** Uncorrected baseline demonstrations of a logical 3-qubit GHZ state and logical Bernstein-Vazirani using transversal gates to observe expected error amplification.

### 2. Bacon-Shor Phenomenological Thresholds
* **Scalable Architectures:** Interleaved Bacon-Shor circuits for distances $d \in \{3, 5, 7, 9\}$.
* **Custom Noise Injection:** A robust Python injector that parses noiseless `.stim` circuits and correctly applies phenomenological error models (`X_ERROR`, `Z_ERROR`, `DEPOLARIZE1`) to data and measurements.
* **Threshold Extraction:** High-statistics Sinter sweep utilizing multiprocessing to extract the phenomenological threshold crossover.

## Outputs & Visualizations
Running the notebook generates several high-resolution artifacts (automatically saved to the local directory):
* Scalable `.svg` files of the logical quantum circuits (including the 21-qubit transversal GHZ and Goto FT encoder).
* `.png` plots of logical vs. physical error rates and threshold crossovers.

## Dependencies
To run the simulations locally, install the required packages:

```bash
pip install stim sinter pymatching numpy matplotlib
```

## Usage
1. Clone the repository.
2. Open `Steane_and_Bacon_Shor_Benchmarking.ipynb` in Jupyter Notebook, Google Colab, or VS Code.
3. **Important:** Ensure that the external circuit files (`bacon_shor_d7.stim` and `bacon_shor_d9.stim`) remain in the same directory as the notebook, as they are required for the Cell 6 threshold sweep.
4. Run all cells. Note: The multi-round Steane memory and $d=9$ Bacon-Shor Sinter sweeps may take 1-2 minutes depending on your CPU core count.

## References
* Goto, H. (2016). *Minimizing resource overheads for fault-tolerant preparation of encoded states of the Steane code*. Scientific Reports, 6, 19578.
* Craig Gidney (2021). *Stim: a fast stabilizer circuit simulator*. Quantum 5, 497.
* Higgins, A. et al. (2023). *PyMatching: A Python package for decoding quantum error-correcting codes using minimum-weight perfect matching*.

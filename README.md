# BB84 Quantum Key Distribution

An algorithmic and physical implementation of the BB84 Quantum Key Distribution (QKD) protocol using Qiskit. This project evaluates the protocol's theoretical security guarantees against practical hardware constraints, featuring scalable temporal-batching execution on physical IBM Quantum processors.

*Developed as a Mini-Project in Quantum Information and Computing (QIC).*

## Key Features

* **Strict Single-Shot Execution:** Adheres to the No-Cloning Theorem by enforcing `shots=1` on all local simulations, guaranteeing that each measured bit represents an independent, true single-photon event.
* **Hardware Circuit Batching:** Bypasses the limited qubit hardware processors by dynamically generating and batching independent quantum circuits, allowing massive key transmissions (e.g., $N=1000$) on the IBM Cloud in a single runtime job.
* **Adversarial Intercept-Resend Simulation:** Models wave-function collapse through mid-circuit eavesdropper measurements, successfully demonstrating the theoretical $25\%$ Quantum Bit Error Rate (QBER) disturbance.
* **Multi-Backend Orchestrator:** Seamlessly executes across noiseless simulators, parameterized noisy simulators and real physical hardware (e.g., `ibm_marrakesh`).

## Results & Convergence

The implementation successfully proves that intercept-resend attacks remain highly visible and securely detectable even when obfuscated by real-world hardware noise. 

1. **Adversarial Detection:** Baseline physical hardware noise hovered comfortably below the $11\%$ Shannon-entropy abort threshold. The introduction of an eavesdropper spiked the QBER to $\approx 25\%$, triggering a mandatory security abort.
2. **Statistical Convergence:** Validates the Law of Large Numbers; at small key lengths ($N=50$), finite-sample effects create high QBER variance, whereas scaling to $N=2000$ perfectly converges the Sifted Key Retention Rate to $50\%$ and Eve's disturbance to $25\%$.

*(See the `figures/` directory for detailed `matplotlib` visualizations of QBER scalability and environment comparisons).*

## Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/mahsa-hemmat//qiskit-bb84-hardware.git
   cd qiskit-bb84-hardware
   # Create and activate a virtual environment
   python3 -m venv env
   source env/bin/activate
   pip install -r requirements.txt
   # To execute the hardware batching test on physical IBM devices, authenticate with your IBM Quantum API token.

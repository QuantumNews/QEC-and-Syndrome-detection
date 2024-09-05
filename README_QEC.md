
# Quantum Circuit Benchmark with Qiskit and IBM Quantum Runtime

This repository demonstrates how to run quantum circuits on IBM Quantum systems using Qiskit and the IBM Quantum Runtime service. The code implements a benchmarking system that submits quantum circuits, applies dynamical decoupling techniques, and retrieves results using Qiskit’s `Estimator` primitive.

## Prerequisites

To use this repository, you must have Python 3.10 or higher installed along with the following Python packages:
- `qiskit`
- `qiskit_ibm_runtime`
- `pylatexenc`
- `qiskit-ibm-provider`
- `qiskit-aer`

These can be installed using the following commands:

```bash
pip install qiskit
pip install qiskit_ibm_runtime
pip install pylatexenc
pip install qiskit-ibm-provider qiskit-aer
```

## Setup

Ensure that you have an IBM Quantum account and access to a valid API token. You can get this from the [IBM Quantum Dashboard](https://quantum-computing.ibm.com/).

Once you have your API token, replace the placeholder `<YOUR_API_TOKEN>` in the code with your actual token.

Example:

```python
from qiskit_ibm_runtime import QiskitRuntimeService

service = QiskitRuntimeService(channel="ibm_quantum", token='<YOUR_API_TOKEN>')
backend = service.get_backend('ibm_brisbane')
```

> Note: The `get_backend()` method is deprecated in newer versions of `qiskit_ibm_runtime`, so ensure to use the `backend()` method instead.

## Running the Code

### 1. Submitting Quantum Circuits
The provided `submit_job` function allows you to submit quantum circuits to IBM Quantum systems. It also includes features for saving job results in a serialized format for later retrieval and inspection.

```python
archive_id = submit_job(circuits, backend_name='ibm_brisbane')
```

### 2. Dynamical Decoupling and Error Suppression
The code integrates dynamical decoupling techniques like the XY4 sequence to suppress noise and coherent errors in idle qubits. A transpiler pass manager is used to optimize the circuit for the specific target backend.

### 3. Running Benchmarks
To run the provided benchmarks, the code includes an example circuit (a Bell state) that can be submitted to the backend, with results displayed as expectation values and their corresponding standard errors.

### 4. Error Handling
The `IBMInputValueError` is handled when the circuit is not compatible with the backend's target system. You can follow Qiskit's transpilation guide to adjust the circuits to match the target hardware.

```python
from qiskit.transpiler.preset_passmanagers import generate_preset_pass_manager
from qiskit.transpiler.passes.scheduling import ALAPScheduleAnalysis, PadDynamicalDecoupling
```

### 5. Viewing Results
You can retrieve the results and display the expectation value and standard error for the circuit.

```python
result = job.result()
expectation_value = result[0].data.evs
print("Expectation Value:", expectation_value)
```

### Example Output

```bash
Expectation Value: 0.042012448132780086
Standard Deviation: 0.018682641759834348
Ensemble Standard Error: 0.016490744814700347
```

## License
This project is licensed under the MIT License.

## Contributions
Feel free to fork the project, submit issues, and contribute via pull requests.

## Contact

For any queries or issues, please reach out to the repository maintainer.

# Fuzzy Logic Speed Controller for DC Motor Based on PI Control

[![NPM](https://img.shields.io/npm/l/react)](https://github.com/ohyescris/ml-cc-motor-speed-control-fuzzy/blob/main/LICENSE) 


> Intelligent speed control of a DC motor using a Fuzzy Logic Controller designed from a conventional PI controller.

---

## Project Highlights

- Intelligent Control using Fuzzy Logic
- Conventional PI controller used as design reference
- Mathematical modeling of a DC motor
- Closed-loop speed control simulation
- Mamdani Fuzzy Inference System
- Python implementation
- Performance evaluation through time-domain responses

---

# Overview

This project presents the development of a **Fuzzy Logic Controller (FLC)** for the speed regulation of a Direct Current (DC) motor.

Unlike purely heuristic fuzzy controllers, the proposed controller is designed using a **conventional PI controller as the reference**, combining the simplicity of classical control with the nonlinear decision-making capabilities of fuzzy inference.

The complete implementation was developed in Python and includes the mathematical model of the motor, controller design, fuzzy inference system, and performance analysis through numerical simulations.

---

# Motivation

DC motors are extensively used in industrial automation because of their excellent speed regulation characteristics.

Although PI controllers remain the industry standard for speed control, their performance may degrade under nonlinear operating conditions or parameter uncertainties.

Fuzzy Logic Controllers provide an intelligent alternative capable of introducing nonlinear control actions through linguistic rules instead of explicit mathematical equations.

This project investigates the application of fuzzy logic to achieve smooth and robust speed regulation while maintaining the design philosophy of a classical PI controller.

---

# Mathematical Model

The controlled plant corresponds to a DC motor modeled from its electrical and mechanical dynamics.

The mathematical model considers:

- Armature resistance
- Armature inductance
- Back-EMF constant
- Torque constant
- Rotor inertia
- Viscous friction coefficient

The resulting transfer function is employed throughout the controller design and simulation.

---

# Controller Design

The proposed controller is developed in two stages.

## PI Controller

A conventional PI controller is initially designed and tuned to obtain the desired transient response.

The resulting controller gains are then used as the reference for constructing the fuzzy controller.

---

## Fuzzy Logic Controller

The analytical PI equation is replaced by a fuzzy inference system composed of linguistic variables and inference rules.

### Controller Inputs

- Speed Error *(e)*
- Change in Error *(Δe)*

### Controller Output

- Control Voltage *(u)*

---

# Universes of Discourse

The first step in the fuzzy controller design consists of defining the universes of discourse for each linguistic variable.

Three universes are considered:

- Speed Error
- Change in Error
- Control Voltage

---

# Membership Functions

Each universe of discourse is partitioned into fuzzy linguistic terms using membership functions.

Typical linguistic labels include:

- Negative Large (NL)
- Negative Medium (NM)
- Negative Small (NS)
- Zero (ZE)
- Positive Small (PS)
- Positive Medium (PM)
- Positive Large (PL)

These membership functions determine how crisp values are transformed into fuzzy variables prior to the inference process.

---

### Figure 2 — Speed Error Membership Functions

![Error Membership Functions](https://github.com/ohyescris/assets/blob/main/images/fuzzy/error_membership_function.png)

---

### Figure 3 — Change in Error Membership Functions

![Delta Error Membership Functions](https://github.com/ohyescris/assets/blob/main/images/fuzzy/delta_error_membership_function.png)

---

### Figure 4 — Control Voltage Membership Functions

![Control Membership Functions](https://github.com/ohyescris/assets/blob/main/images/fuzzy/control_action_membership_function.png)

---

# Fuzzy Rule Base

The controller behavior is defined through a collection of fuzzy IF–THEN rules relating the speed error and its variation to the control voltage.

Example:

```text
IF Error is Positive Large
AND Change in Error is Negative Small

THEN Control Voltage is Positive Medium
```

The complete fuzzy rule base is summarized below.

| **Error (E) \\ ΔError (ΔE)** | **NL** | **NM** | **NS** | **ZE** | **PS** | **PM** | **PL** |
|:----------------------------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
| **NL** | NL | NL | NL | NL | NM | NS | ZE |
| **NM** | NL | NL | NL | NM | NS | ZE | PS |
| **NS** | NL | NL | NM | NS | ZE | PS | PM |
| **ZE** | NL | NM | NS | ZE | PS | PM | PL |
| **PS** | NM | NS | ZE | PS | PM | PL | PL |
| **PM** | NS | ZE | PS | PM | PL | PL | PL |
| **PL** | ZE | PS | PM | PL | PL | PL | PL |

The inference process follows the **Mamdani** approach, and the resulting fuzzy output is converted into a crisp control signal using centroid defuzzification.

---

# Closed-Loop Control Structure

```text
Reference Speed
        │
        ▼
   Speed Error
        │
        ▼
 Fuzzy Controller
        │
        ▼
 Control Voltage
        │
        ▼
     DC Motor
        │
        ▼
Measured Speed
        ▲
        └──────────── Feedback
```

---

# Technologies

- Python
- NumPy
- SciPy
- Matplotlib
- scikit-fuzzy
- Jupyter Notebook

---

# Simulation Results

The controller performance is evaluated through numerical simulations using the mathematical model of the DC motor.

---

## Figure 5 — Speed Response

The speed response illustrates the controller's capability to track the reference speed while maintaining closed-loop stability.

![Speed Response](https://github.com/ohyescris/assets/blob/main/images/fuzzy/velocidade_evolucao_tempo.png)

---

## Figure 6 — Control Voltage

The controller output corresponds to the voltage applied to the motor armature.

This signal represents the control effort required to regulate the motor speed.

![Control Voltage](https://github.com/ohyescris/assets/blob/main/images/fuzzy/tensao_saida_evolucao_tempo.png)

---

## Figure 7 — Error Analysis

The controller performance is further evaluated through the evolution of:

- Speed error
- Change in error

These variables provide valuable insight into convergence, transient behavior and steady-state accuracy.

![Error Analysis](https://github.com/ohyescris/assets/blob/main/images/fuzzy/erro_evolucao_tempo.png)

![Delta Error Analysis](https://github.com/ohyescris/assets/blob/main/images/fuzzy/delta_erro_evolucao_tempo.png)

---

# Discussion

The obtained simulations demonstrate the dynamic behavior of the proposed fuzzy controller under closed-loop operation.

The presented results allow the analysis of:

- Speed tracking performance
- Control effort
- Error convergence
- Evolution of the error derivative
- Influence of the fuzzy membership functions
- Effect of the fuzzy inference mechanism on the generated control action

The relationship between the universes of discourse, membership functions and fuzzy rules provides an intuitive interpretation of the controller behavior while preserving the robustness of a conventional PI-based design.

---

# Conclusion

This project presented the development of a **Fuzzy Logic Controller** for DC motor speed regulation based on a conventional PI controller.

The proposed methodology combines classical control theory with intelligent systems, replacing the analytical PI equation by a linguistic inference mechanism capable of generating nonlinear control actions.

The complete implementation includes the definition of the universes of discourse, membership functions, fuzzy rule base and closed-loop simulation.

Overall, this project demonstrates how fuzzy systems can be successfully employed for nonlinear control applications while preserving the interpretability and design principles of classical controllers.

Future work may include:

- Adaptive Fuzzy Control
- ANFIS (Adaptive Neuro-Fuzzy Inference System)
- Genetic optimization of membership functions
- Embedded implementation
- Hardware-in-the-loop simulations
- Comparison with PID and Model Predictive Control (MPC)

---

# Repository Structure

```text
.
├── dc_motor_fuzzy_controller.ipynb
├── README.md
├── requirements.txt
```

---

# Reproducibility

Clone the repository:

```bash
git clone https://github.com/your_username/your_repository.git
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Launch the notebook:

```bash
jupyter notebook
```

---

# Author

**Cristiano Araújo**

M.Sc. Student in Computer Science (Artificial Intelligence)

### Research Interests

- Intelligent Control
- Fuzzy Systems
- Machine Learning
- Artificial Intelligence
- Signal Processing
- Control Engineering

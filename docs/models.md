# Model and Algorithm Documentation

## 1. Almgren-Chriss Market Impact Model

### Purpose

The Almgren-Chriss model provides a framework for optimal trade execution that minimizes total cost by balancing market impact and execution risk.

### Core Concepts

* **Temporary Market Impact:** Transient effect that decays after execution.
  $T(v) = \eta \cdot v^\alpha$
* **Permanent Market Impact:** Lasting change in price due to executed volume.
  $P(v) = \gamma \cdot v^\beta$
* **Execution Risk:** Uncertainty due to price volatility while the trade is being executed.
* **Hamiltonian Cost Function:** Combines all components to find optimal execution.

### Parameters

* $\alpha, \beta$: curvature parameters
* $\eta, \gamma$: impact sensitivity coefficients
* $\lambda$: risk aversion factor
* $\sigma$: price volatility
* $\Delta t$: time step duration

### Algorithm

* Uses dynamic programming to compute optimal volume at each time step.
* Tracks value functions and optimal actions in matrices for efficient backward computation.

---

## 2. Slippage Estimation Model

### Purpose

To estimate additional cost due to execution inefficiency using a regression approach.

### Technique

* **Linear Regression**
* Inputs: Volatility, fee tier, order size
* Output: Predicted slippage cost in USD

### Benefits

* Fast to train and evaluate
* Interpretable coefficients

---

## 3. Maker/Taker Participation Prediction

### Purpose

To estimate the probability of an order being executed as a maker vs. taker, influencing fee computation.

### Technique

* **Logistic Regression**
* Features: Order size, volatility
* Output: Maker/taker participation probability

### Usage

* Used to compute weighted transaction fee in the cost model

---

## Summary of Model Choices

| Model Type             | Technique Used      | Reasoning                           |
| ---------------------- | ------------------- | ----------------------------------- |
| Market Impact          | Almgren-Chriss      | Robust optimal execution            |
| Slippage Estimation    | Linear Regression   | Simplicity and speed                |
| Maker/Taker Prediction | Logistic Regression | Probabilistic output and efficiency |


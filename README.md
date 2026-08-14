# Black-Scholes Option Pricing via Explicit Finite Difference Method

This repository contains a Python implementation that numerically solves the **Black-Scholes Partial Differential Equation (PDE)** for European Call Option pricing. By transforming the Black-Scholes equation into the dimensionless **Heat Equation**, an **Explicit Finite Difference Method (FDM)** is applied to calculate option prices over a discretized spatio-temporal grid.

---

## 📌 Theoretical Background

### 1. Black-Scholes PDE
The Black-Scholes PDE models the price of a European option $V(S, t)$ as a function of stock price $S$ and time $t$:

$$
\frac{\partial V}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} + r S \frac{\partial V}{\partial S} - r V = 0
$$

where $S$ is the stock price, $t$ is time, $r$ is the risk-free interest rate, and $\sigma$ is volatility.

### 2. Reduction to the Heat Equation
To simplify the numerical solution, we transform the PDE into the Heat Equation using dimensionless variables:
* Log-price spatial variable: $x = \ln(S/K)$
* Time to maturity variable: $\tau = \frac{\sigma^2}{2}(T - t)$
* Transformed option value: $v(x, \tau)$

This yields the classical Heat Equation form:

$$
\frac{\partial u}{\partial \tau} = \frac{\partial^2 u}{\partial x^2}
$$

---

## 📐 Numerical Implementation (Explicit FDM)

Discretizing space $x \in [x_{\min}, x_{\max}]$ into $N_x$ points and dimensionless time $\tau \in [0, \tau_{\max}]$ into $N_t$ steps, the explicit update formula is:

$$
u_{i, j+1} = u_{i, j} + \mu \left( u_{i+1, j} - 2u_{i, j} + u_{i-1, j} \right)
$$

where the stability coefficient $\mu = \frac{\Delta \tau}{\Delta x^2}$.

### CFL Stability Condition
For numerical stability, the Courant-Friedrichs-Lewy (CFL) condition must hold:

$$
\mu \le 0.5
$$

In this implementation, $\mu \approx 0.0030 \le 0.5$, guaranteeing full convergence.

---

## ⚙️ Parameters & Boundary Conditions

### Model Parameters
* **Volatility ($\sigma$):** `0.2`
* **Risk-free Rate ($r$):** `0.05`
* **Strike Price ($K$):** `100`
* **Time to Maturity ($T$):** `1.0`
* **Grid:** $N_x = 50$, $N_t = 1000$

### Boundary Conditions
* **Initial Payoff ($\tau=0$):** $u(x, 0) = \max\left(e^x - 1, 0\right)$
* **Lower Boundary ($x \to x_{\min}$):** $u(x_{\min}, \tau) = 0$
* **Upper Boundary ($x \to x_{\max}$):** $u(x_{\max}, \tau) = e^{x_{\max}} - e^{-r\tau}$

---

## 🛠️ Tech Stack & Environment

* **Language:** Python
* **Libraries:** NumPy, Matplotlib
* **Environment:** Jupyter Notebook (`Blackscholes.ipynb`)

---

## 👤 Author

* **Elif Gül Temizel** — Department of Mathematics, Istanbul Bilgi University
* **Course:** MATH 420

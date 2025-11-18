# Implied Binomial Tree (IBT) Solver

This project implements the **Implied Binomial Tree (IBT)** model in Python, a fundamental technique used in quantitative finance to derive the **risk-neutral probability distribution** directly from observed market option prices.

The model uses a constrained non-linear optimization routine to find the unique set of nodal probabilities that perfectly matches the spot price and the prices of a basket of Call/Put options.

---

## 💡 Core Financial Concept

The standard Cox-Ross-Rubinstein (CRR) model assumes a constant volatility ($\sigma$), resulting in a simple, symmetric (log-normal) probability distribution. Real-world option prices, however, exhibit a **Volatility Smile** or **Skew**.

This IBT project "inverts" the problem:

1.  **Goal:** Find the probability distribution that explains the real market prices.
2.  **Result:** The resulting "implied" distribution is typically non-normal and shows "fat tails," visually demonstrating the market's expectation of extreme price movements (the Volatility Smile).

## 🛠️ Implementation & Technology

### Key Features:

* **Risk-Neutral Pricing:** Implements standard Black-Scholes (BS) and CRR pricing functions.
* **Constrained Optimization:** Uses `scipy.optimize.minimize` (SLSQP method) to minimize the Sum of Squared Errors (SSE) between model prices and market prices.
* **No-Arbitrage Constraints:** The solver is strictly constrained by financial laws:
    * $\sum P_j = 1$ (Probabilities must sum to one).
    * $0 \le P_j \le 1$ (Probabilities must be non-negative).
    * The final IBT prices must lie within the market's Bid-Ask spread.
* **Initial Guess Strategy:** Employs a robust strategy by initializing the solver with a near-optimal solution (from external analysis), guaranteeing rapid convergence to the global minimum.
* **Visualization:** Plots the final Implied Distribution against the A Priori (CRR) Distribution to visualize the Volatility Smile phenomenon.

### Output Visualization

The final graph demonstrates how the smooth, theoretical **A Priori (CRR) Distribution** (red line) must be **deformed** into the "bumpy," two-peaked **Implied Distribution** (blue bars) to accurately match the market's pricing.

<img width="1023" height="656" alt="distribuzione_probabilita_IBT_finale" src="https://github.com/user-attachments/assets/4edc70ba-107d-4a9c-bedf-14833b4f4aff" />

---

## ⚙️ Usage and Customization

### Prerequisites

```bash
pip install numpy scipy matplotlib pandas

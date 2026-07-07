# Aerodynamic Trajectory Solver: Euler vs. Runge-Kutta

A computational study evaluating the truncation errors, stability limits, and convergence rates of **Euler (1st-order)**, **RK2 (2nd-order)**, and **RK4 (4th-order)** numerical integration methods. The algorithms are applied to a non-linear flight equation describing free-fall under quadratic aerodynamic drag and validated against a closed-form analytical solution.

---

##  System Physics & Mathematical Model

The simulation models an object dropping vertically through a fluid medium. The net downward force accounts for constant gravity and atmospheric drag acting opposite to the velocity vector ($F_d \propto v^2$).

Applying Newton's Second Law ($F = ma$):

$$\frac{dv}{dt} = g - kv^2$$

Where:
* $g = 9.81 \text{ m/s}^2$ (Acceleration due to gravity)
* $k = \frac{C_d \rho A}{2m}$ (Consolidated aerodynamic drag coefficient)
* $v(t)$ is the dynamic velocity of the vehicle over time.

### The Analytical Baseline
Because this non-linear ordinary differential equation (ODE) has a known exact solution, we use it as our absolute ground truth to compute numerical error percentage over a fixed flight duration ($t = 10\text{ s}$):

$$v_{\text{exact}}(t) = \sqrt{\frac{g}{k}} \tanh\left(\sqrt{g \cdot k} \cdot t\right)$$

---

## Implemented Numerical Solvers

This project steps through time using three discrete integration methods to analyze how step size ($h$) impacts local and global truncation errors:

1. **Euler's Method ($\mathcal{O}(h)$ Global Error):** Evaluates the derivative purely at the beginning of the time step. Fast but highly prone to drifting on non-linear curves.
2. **RK2 / Heun's Method ($\mathcal{O}(h^2)$ Global Error):** An predictor-corrector approach that averages slopes at the boundary points of the interval.
3. **RK4 Method ($\mathcal{O}(h^4)$ Global Error):** The industry standard for orbital mechanics and flight dynamics. It utilizes four distinct slope samples across the step (start, midpoints, and trial end) to cancel lower-order error terms.

---

## Key Visualizations & Analysis

The Jupyter Notebook generates two core plots to demonstrate algorithmic behavior:

1. **Flight Velocity Profile:** Simulates the trajectory at a massive step size ($h = 0.8\text{ s}$) to visually show Euler's method overshooting and drifting, while RK4 accurately tracks the exact physics curve.
2. **Error Convergence Rates (Log-Log Scale):** Iterates across a range of step sizes (`np.linspace(0.01, 2.0, 150)`) plotting Absolute Error % vs $h$. It graphically validates the theoretical slopes (Linear vs. Quadratic vs. 4th-order steep cliffs) and highlights the numerical stability boundaries.

---

## How to Run

### Prerequisites
Ensure you have a Python environment with the required data-science stack installed:
```bash
pip install numpy pandas matplotlib jupyter
```

Still Under-progress

# 1D Unsteady Couette Flow — Numerical Methods Comparison

## Core Concept
Couette Flow is the flow of a viscous fluid trapped between two parallel plates,
where one plate is fixed and the other suddenly starts sliding at a constant
velocity. It is physically important because it is one of the only real fluid
flows with an exact mathematical solution, which makes it the standard
benchmark for validating numerical CFD methods before trusting them on harder,
unsolvable problems (like full aircraft flow).

The main equation and methods used in this project are as follows:

**Governing Equation (reduced Navier-Stokes)** — Starting from the full 2D
incompressible Navier-Stokes equations and applying the assumptions of
infinite plates, no pressure gradient, and zero vertical velocity, the
equation collapses to the 1D diffusion equation:

$$\frac{\partial u}{\partial t} = \nu \frac{\partial^2 u}{\partial y^2}$$

**Exact Solution (Fourier Series)** — Solved by separation of variables into a
steady linear part and a decaying transient part:

$$u(y,t) = U\frac{y}{H} + \frac{2U}{\pi}\sum_{n=1}^{\infty}\frac{(-1)^n}{n}\sin\left(\frac{n\pi y}{H}\right)e^{-n^2\pi^2\nu t/H^2}$$

**FTCS (Explicit)** — Updates each point using only current, known values.
Cheap per step, but conditionally stable:

$$u_i^{n+1} = u_i^n + r\left(u_{i+1}^n - 2u_i^n + u_{i-1}^n\right), \quad r=\frac{\nu\Delta t}{\Delta y^2} \le 0.5$$

**BTCS (Implicit)** — Solves all points simultaneously via a tridiagonal
system, unconditionally stable but still first-order accurate:

$$-r\,u_{i-1}^{n+1} + (1+2r)\,u_i^{n+1} - r\,u_{i+1}^{n+1} = u_i^n$$

**Crank-Nicolson** — Averages the explicit and implicit stencils, giving
second-order accuracy while remaining unconditionally stable:

$$-\frac{r}{2}u_{i-1}^{n+1} + (1+r)u_i^{n+1} - \frac{r}{2}u_{i+1}^{n+1} = \frac{r}{2}u_{i-1}^n + (1-r)u_i^n + \frac{r}{2}u_{i+1}^n$$

This simulation applies the governing equation three different numerical ways
and checks each against the exact Fourier series solution. FTCS shows what
happens when the stability limit is ignored, BTCS shows that unconditional
stability doesn't buy extra accuracy, and Crank-Nicolson shows what a real
industrial CFD default actually looks like — stable *and* accurate.

---

## Constants

$$H = 0.02 \ \text{m}, \quad U = 1.0 \ \text{m/s}$$
$$\nu = 1.5\times 10^{-5} \ \text{m}^2\text{/s (air)}, \quad \mu = 1.8\times 10^{-5} \ \text{Pa·s (air)}$$
$$N = 41 \ \text{grid points}, \quad \Delta y = 5.0\times 10^{-4} \ \text{m}$$
$$t_{diff} = H^2/\nu = 26.667 \ \text{s}$$

## Key Results

**Wall shear stress development (skin friction proxy)**

| Time (s) | τ_w numerical (Pa) | τ_w exact (Pa) |
|---|---|---|
| 0.53 | 1.42×10⁻⁸ | 2.30×10⁻⁸ |
| 1.33 | 2.97×10⁻⁵ | 3.00×10⁻⁵ |
| 2.67 | 2.64×10⁻⁴ | 2.63×10⁻⁴ |
| 6.67 | 7.48×10⁻⁴ | 7.47×10⁻⁴ |
| 13.33 | 8.87×10⁻⁴ | 8.87×10⁻⁴ |
| 26.67 | 9.00×10⁻⁴ | 9.00×10⁻⁴ |

**Stability showdown at r = 0.55 (above the 0.5 explicit limit)**

| Method | max\|u\| at t=5s | Stable? |
|---|---|---|
| FTCS | 2.99×10³⁹ | No |
| BTCS | 1.00 | Yes |
| Crank-Nicolson | 1.00 | Yes |

**Method comparison**

| Method | Time accuracy | Stability limit | Per-step cost |
|---|---|---|---|
| FTCS | O(Δt) | r ≤ 0.5 | 1 evaluation |
| BTCS | O(Δt) | None | Tridiagonal solve |
| Crank-Nicolson | O(Δt²) | None | Tridiagonal solve |

## Physical Insight

- The first table tells us how wall shear stress builds up from zero as the
  moving plate's influence diffuses across the gap — it doesn't reach even
  half its final value until about t=6.67s, a quarter of the diffusion
  timescale $t_{diff}=H^2/\nu$, and only fully converges around one full
  $t_{diff}$. This is exactly the "spin-up" behavior of a real boundary
  layer forming on an aircraft surface, just compressed into a 1D toy problem.

- A small correlation with aerospace engineering because $\tau_w$ is precisely
  the quantity that gets integrated over a wing or fuselage surface to compute
  skin-friction drag — one of the two major drag components on any aircraft,
  alongside pressure drag.

- The second table shows what "conditionally stable" actually means in
  practice, not just in theory. At r=0.55 — barely 10% past the 0.5 limit —
  FTCS's error doesn't grow gently, it explodes by roughly 39 orders of
  magnitude within 5 seconds. The exact blow-up rate follows the amplification
  factor $G = 1-4r\sin^2(k\Delta y/2)$; at r=0.55 the worst mode has $|G|\approx1.2$,
  and $1.2^{545}\approx10^{43}$ — consistent with what the simulation produced.
  Meanwhile BTCS and Crank-Nicolson, run at that exact same r, stayed at
  max|u|=1.0 — proof that "unconditional stability" isn't a theoretical
  nicety, it's the difference between a usable and a useless simulation.

- The third table is the real engineering takeaway: BTCS buys stability but
  not accuracy (still O(Δt)), while Crank-Nicolson buys both — which is
  exactly why it (or its 2nd/3rd-order relatives) is the default diffusion-term
  discretization in real solvers, including the OpenFOAM case explored
  earlier in this project.

## Assumptions Made
- Plates are infinite (no edge effects)
- Fluid is Newtonian (constant μ, stress ∝ strain rate)
- No applied pressure gradient (flow driven purely by the moving plate)
- Laminar flow (no turbulence)
- No-slip condition at both walls
- Incompressible, constant-density fluid
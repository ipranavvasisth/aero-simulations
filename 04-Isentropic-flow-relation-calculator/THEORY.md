# Isentropic Flow Analysis

## Core Concept
This concept of isentropic flow is mainly used in fluid mechanics 
and thermodynamics, mainly in the high speed aerodynamics area. 
Here the flow is adiabatic and reversible. And for a flow to be 
truly isentropic then it must satisfy these two conditions:

- **Adiabatic (δq = 0)** — There is no heat transfer between the 
fluid and its surroundings. The fluid doesn't gain heat from a 
combustion source nearby nor does it lose its heat to the 
surroundings.

- **Reversible** — There are no friction losses within the flow.
This means there is no internal friction, which is known as 
viscosity, and no turbulence as well.

And if both of these are true then the change in entropy is 0:

$$ds = 0 \Rightarrow s = \text{Constant}$$

**Stagnation Conditions:**
Stagnation conditions (T₀, P₀, ρ₀) represent the temperature, 
pressure, and density the flow would have if brought to rest 
isentropically. They serve as reference conditions from which 
all flow properties are normalized. At M=0, static conditions 
equal stagnation conditions. As Mach number increases, static 
temperature, pressure, and density all fall below their 
stagnation values as thermal energy converts to kinetic energy.

**What This Project Does:**
This project calculates and visualizes the four fundamental 
isentropic flow relations — temperature ratio T/T₀, pressure 
ratio P/P₀, density ratio ρ/ρ₀, and area ratio A/A* — as 
functions of Mach number from M=0 to M=5. It also provides 
a lookup table for any given Mach number, serving as a 
computational version of the isentropic flow tables used 
in aerospace engineering practice.

---

## Governing Equations

**1 — Temperature Ratio:**
$$\frac{T}{T_0} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{-1}$$

**2 — Pressure Ratio:**
$$\frac{P}{P_0} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{-\frac{\gamma}{\gamma-1}}$$

**3 — Density Ratio:**
$$\frac{\rho}{\rho_0} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{-\frac{1}{\gamma-1}}$$

**4 — Area Ratio:**
$$\frac{A}{A^*} = \frac{1}{M}\left[\frac{2}{\gamma+1}
\left(1 + \frac{\gamma-1}{2}M^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}$$

These are the same equations used in Project 2 — Rocket Nozzle 
Flow. The difference is that here they are plotted across the 
full Mach number range rather than evaluated at a single exit 
point.

---

## Key Results

| Mach Number (M) | T/T₀ | P/P₀ | ρ/ρ₀ | A/A* |
|-----------------|------|------|------|------|
| 0.01 | 1.0000 | 0.9999 | 1.0000 | 57.8738 |
| 0.50 | 0.9524 | 0.8430 | 0.8852 | 1.3398 |
| 1.00 | 0.8333 | 0.5283 | 0.6339 | 1.0000 |
| 2.00 | 0.5556 | 0.1278 | 0.2300 | 1.6875 |
| 5.00 | 0.1667 | 0.0019 | 0.0113 | 25.0000 |

---

## Physical Insights

**Connection to Project 2:**
These equations are the same ones used in the Rocket Nozzle Flow 
project. The difference is that instead of evaluating them at 
one specific exit point, here we plot them across all Mach 
numbers to see how each property changes continuously with flow 
speed. Seeing the full curve reveals behavior that a single point 
calculation cannot show.

**Pressure drops faster than temperature:**
In the plots, P/P₀ drops much more steeply than T/T₀. The reason 
is the exponent — pressure is raised to γ/(γ-1) = 3.5 for air, 
while the temperature exponent is 1. This has real consequences 
for aerospace design. At high Mach numbers, pressure drops 
drastically compared to temperature. In reverse, when air hits 
an aircraft and slows down to stagnation, pressure spikes far 
more dramatically than temperature. This is why aerodynamic 
pressure loads on aircraft structures are the dominant design 
concern at high speeds, not just thermal loads.

**The A/A* curve — two branches:**
The area ratio curve has two branches that meet at M=1 where 
A/A* = 1 — the minimum area point, the throat. The left branch 
represents subsonic flow in the converging section of a nozzle, 
while the right branch represents supersonic flow in the 
diverging section. This is the mathematical foundation of the 
C-D nozzle design from Project 2 — now visible as a complete 
curve rather than a single calculated point.

---

## Assumptions Made
- Calorically perfect gas — constant specific heats
- Steady, one dimensional flow
- No heat transfer — adiabatic
- No friction or viscous effects
- No normal shocks

---

## References
- Anderson, J.D. — Modern Compressible Flow.
- Anderson, J.D. — Introduction to Flight.
- Cengel & Cimbala — Fluid Mechanics.
# Isentropic Flow Analysis

## Core Concept
This concept of isentropic flow is mainly used in fluid mechanics and thermodynamics mainly in the high speed aerodynamics area. Here the flow is adiabatic and reversible. And for a flow to be truly isentropic then it must satisfy these two conditions:

- Adiabatic (δq = 0) - Here there is no heat transfer between the fluid and its surroundings. The fluid doesn't gain heat from a combustion source nearby nor does it lose its heat to the surroundings

- Reversible - There is no friction like losses within the flow, this means that there is no internal friction, which is known as viscosity, and no turbulence as well.

And if both of these are true then, the change in entropy is 0:

$$ds = 0 \Rightarrow s = \text{Constant}$$

- Now speaking about the Stagnation conditions:
Stagnation conditions (T₀, P₀, ρ₀) represent the temperature, 
pressure, and density the flow would have if brought to rest 
isentropically. They serve as reference conditions from which 
all flow properties are normalized. At M=0, static conditions 
equal stagnation conditions. As Mach number increases, static 
temperature, pressure, and density all fall below their 
stagnation values as thermal energy converts to kinetic energy.
- And the main question, what does this project do?
This project calculates and visualizes the four fundamental 
isentropic flow relations — temperature ratio T/T₀, pressure 
ratio P/P₀, density ratio ρ/ρ₀, and area ratio A/A* — as 
functions of Mach number from M=0 to M=5. It also provides 
a lookup table for any given Mach number, serving as a 
computational version of the isentropic flow tables used 
in aerospace engineering practice.

## Governing Equations
There are the equations for Temperature, Pressure, Density and Area:
1- Temperature:
$$\frac{T_0}{T} = 1 + \frac{\gamma - 1}{2}M^2$$
2- Pressure:
$$\frac{p_0}{p} = \left( 1 + \frac{\gamma - 1}{2}M^2 \right)^{\frac{\gamma}{\gamma - 1}}$$
3- Density:
$$\frac{\rho_0}{\rho} = \left( 1 + \frac{\gamma - 1}{2}M^2 \right)^{\frac{1}{\gamma - 1}}$$
4- Area:
$$\frac{A}{A^*} = \frac{1}{M}\left[\frac{2}{\gamma+1}
\left(1 + \frac{\gamma-1}{2}M^2\right)\right]^{\frac{\gamma+1}{2(\gamma-1)}}$$

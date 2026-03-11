# Rocket Nozzle Flow — Theory

## Core Concept
A rocket nozzle converts thermal energy from combustion into kinetic 
energy by accelerating exhaust gases to supersonic speeds. The 
Convergent-Divergent (C-D) nozzle is the standard design used in 
all rocket engines to achieve this.

---

## The C-D Nozzle — Three Sections

| Section | Area | Mach Number |
|---------|------|-------------|
| Converging | Decreasing | M < 1 (subsonic) |
| Throat | Minimum | M = 1 (sonic) |
| Diverging | Increasing | M > 1 (supersonic) |

---

## Why Does Flow Accelerate in the Diverging Section?

This is counterintuitive. In everyday experience, a wider pipe slows 
flow down. In supersonic flow the opposite is true.

The Area-Velocity relation explains this:

$$\frac{dA}{A} = (M^2 - 1)\frac{dV}{V}$$

- When M < 1: (M²-1) is negative → decreasing area increases velocity
- When M = 1: (M²-1) = 0 → area is at minimum (throat)
- When M > 1: (M²-1) is positive → increasing area increases velocity

This is why the diverging section accelerates supersonic flow.

---

## Governing Equations

### 1. Area-Mach Relation
Relates the local area ratio to the local Mach number:

$$\frac{A}{A_t} = \frac{1}{M}\left[\frac{2}{\gamma+1}
\left(1 + \frac{\gamma-1}{2}M^2\right)\right]^{(\gamma+1)/2(\gamma-1)}$$

This equation has two solutions for every area ratio > 1:
- One subsonic (converging section)
- One supersonic (diverging section)

### 2. Isentropic Temperature Relation
$$\frac{T_0}{T} = 1 + \frac{\gamma-1}{2}M^2$$

### 3. Isentropic Pressure Relation
$$\frac{P_0}{P} = \left(1 + \frac{\gamma-1}{2}M^2\right)^{\gamma/(\gamma-1)}$$

### 4. Exit Velocity
$$V_e = \sqrt{\frac{2\gamma}{\gamma-1}RT_c
\left(1-\left(\frac{P_e}{P_c}\right)^{(\gamma-1)/\gamma}\right)}$$

### 5. Mass Flow Rate (Choked at Throat)
$$\dot{m} = \frac{P_c A_t}{\sqrt{T_c}}\sqrt{\frac{\gamma}{R}}
\left(\frac{2}{\gamma+1}\right)^{(\gamma+1)/2(\gamma-1)}$$

### 6. Thrust Equation
$$F = \dot{m}V_e + (P_e - P_0)A_e$$

Two terms:
- **Momentum thrust** — $\dot{m}V_e$ — dominant term, mass expelled 
  at high velocity
- **Pressure thrust** — $(P_e - P_0)A_e$ — contribution from exit 
  pressure difference. Negative when nozzle is overexpanded (Pe < P0).

### 7. Specific Impulse
$$I_{sp} = \frac{F}{\dot{m}g_0}$$

The rocket equivalent of fuel efficiency. Units are seconds.
Higher Isp = more thrust per unit propellant consumed.

---

## Key Results (This Simulation)

| Parameter | Value |
|-----------|-------|
| Area Ratio (Ae/At) | 4.0 |
| Exit Mach Number | 2.94 |
| Exit Temperature | 1099.33 K |
| Exit Pressure | 59,573 Pa |
| Exit Velocity | 2242.31 m/s |
| Mass Flow Rate | 16.91 kg/s |
| Thrust | 36,240.82 N |
| Specific Impulse | 218.50 s |

---

## Physical Insights

**Overexpansion** — The nozzle is overexpanded because Pe (59,573 Pa) 
is below atmospheric pressure P0 (101,325 Pa). This means the pressure 
thrust term is negative, reducing total thrust. Perfect expansion 
(Pe = P0) is a design goal for maximum efficiency.

**Temperature drop** — Gas cools from 3000K in the chamber to 1099K 
at exit. This thermal energy is converted directly into kinetic energy 
— the exhaust velocity of 2242 m/s.

**Choked flow** — Once the throat reaches M=1, mass flow rate is fixed 
regardless of what happens downstream. This is why rocket thrust is 
controlled by chamber pressure, not nozzle geometry.

---

## Scope of This Simulation

While this project simulates a C-D nozzle specifically, the underlying 
isentropic flow equations are valid for any isentropic duct flow. The 
same codebase with minor modifications can model:

**Converging Only Nozzle**
Flow accelerates from subsonic to maximum M=1 at exit. Used in jet 
engines and subsonic applications. Cannot achieve supersonic flow. 
Modeled using only the converging section of this code.

**Other Rocket Nozzle Geometries**
- Bell nozzle — standard curved C-D design, what this simulation models
- Conical nozzle — straight walled diverging section, simpler but 
  slightly less efficient
- Aerospike nozzle — self-adjusts to ambient pressure at different 
  altitudes, active research area in modern rocketry
- Plug nozzle — similar self-adjusting concept to aerospike

**Diffusers**
A nozzle in reverse — decelerates flow from high speed to low speed. 
Used in jet engine inlets to slow incoming air before the compressor. 
Same isentropic equations apply.

**Where This Simulation Breaks Down**
The isentropic assumption fails when:
- Normal shocks occur inside the nozzle due to severe overexpansion
- Boundary layer friction effects become significant
- Real gas effects — combustion chemistry changes exhaust properties
- Flow separation occurs at the nozzle wall

These require CFD approaches beyond the scope of this simulation.

---

## Assumptions Made

- Ideal gas behavior
- Isentropic flow (no friction, no heat loss)
- Steady state flow
- One dimensional flow
- Constant specific heats (calorically perfect gas)
- Fully attached flow (no separation)

---

## References

- Anderson, J.D. — Introduction to Flight
- Anderson, J.D. — Modern Compressible Flow
- Mattingly, J.D. — Elements of Propulsion: Gas Turbines and Rockets
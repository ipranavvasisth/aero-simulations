## Brayton Cycle - Theory

## Core Concpet
The fundamental idead of the brayton cycle is that it is the convertion of 
heat energy into mechanical energy throught continous flow. This can also 
be told as the basic thermodynamic process that governs the jet engines 
gas turbines

## The Four Stages
| Stage | Process | What Happens |
|-------|---------|---------------|
|1 -> 2 | Isentopic Compression | The Air is drawn in the compressor |
|2 -> 3 | Isobaric Addition | The high-pressure air enter the combustion chamber |
|3 -> 4 | Isentropic Expanssion | The high-temperature and high-pressure gas enters the turbine |
|4 -> 1 | Isobaric Rejection | The gas is exhausted out of the turbine |

## Governing Equations
Isentropic Temperature after Compression:
$$T_2 = T_1 \cdot r^{(\gamma-1)/\gamma}$$
Pressure after Compression:
$$P_2 = P_1 \cdot r$$
Heat Added:
$$Q_{in} = C_p (T_3 - T_2)$$
Heat Rejected:
$$Q_{out} = C_p (T_4 - T_1)$$
Net Work Output:
$$W_{net} = Q_{in} - Q_{out}$$
Thermal Efficiency:
$$\eta = \frac{W_{net}}{Q_{in}} = 
1 - \frac{1}{r^{(\gamma-1)/\gamma}}$$
Back Work Ratio(BWR):
$$BWR = \frac{W_{compressor}}{W_{turbine}} = 
\frac{C_p(T_2 - T_1)}{C_p(T_3 - T_4)}$$

## Key Results 
| Parameters | Value |
|------------|-------|
|Compression Ratio | 10:1 |
|Thermal Efficiency | 48.21% |
|Net Work Output | 397642.55 J/Kg |
|Back Work Ratio | 41.37% |
|Work By Turbine | 678247.91 J/Kg |
|Work By Compressor | 280605.37 J/Kg |

## Physical Insights and Assumptions Made
- The Back Work Ratio (BWR) of 41.37% means that for every 
 joule of work the turbine produces, 0.4137 J goes directly into 
 driving the compressor just to sustain the cycle. This is 
 why turbine blade efficiency is such a critical factor  in 
 real jet engine design — even small improvements in blade 
 aerodynamics directly affect the fuel economy.

- The efficiency vs compression ratio curve shows clear 
diminishing returns. Moving from r=1 to r=10 yields a 
significant efficiency gain of  50%, while increasing 
from r=30 to r=40 yields less than 2 %. This means 
there is a point beyond which further increasing 
compression ratio gives minimal efficiency benefit 
while significantly increasing stress and load on engine 
components. Real engine designers balance this tradeoff 
carefully.

## State Conditions
| State | Temperature (K) | Pressure (Pa) |
|-------|----------------|---------------|
| State 1 — Inlet | 300 | 101325 |
| State 2 — After Compression | 579.21 | 1013250 |
| State 3 — After Combustion | 1400 | 1013250 |
| State 4 — After Expansion | 725.13 | 101325 |

## Assumptions Made
- Ideal gas behavior
- Isentropic compression and expansion — no friction or heat loss
- Constant specific heats throughout the cycle
- Steady state continuous flow
- No pressure drop in combustion chamber
- Perfect combustion — no chemical dissociation

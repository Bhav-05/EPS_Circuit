# CubeSat Electrical Power Subsystem (EPS) Simulation

## Project Overview
This project models a minimal CubeSat Electrical Power Subsystem (EPS) using CircuitJS. The objective is to simulate **solar charging, battery discharge, and load behavior** over a 90-minute orbit (60 min sun, 30 min eclipse).

---

## Approach

1. **Theory Understanding**  
   - Reviewed CubeSat EPS concepts: solar panel with MPPT, battery storage, loads (OBC, TT&C, Payload), and EPS losses.
   - Identified simulation equivalents in CircuitJS:
     - Solar panel → Pulse voltage source
     - Battery → Voltage source + series resistor
     - EPS losses → Series resistors
     - Loads → Resistors + pulse sources
     - SOC → Monitored qualitatively via battery current

2. **Component Mapping**
| EPS Function       | CircuitJS Component             | Specification / Notes |
|---------------- ---|-------------------------------- -|---------------------|
| Solar Panel + MPPT | Pulse Voltage Source + Resistor | 9 V sun, 0 V eclipse, 2 Ω series |
| Capacitor  (SOC)   | Capacitor + Series r            | 7.4 V, 0.5 Ω series |
| OBC / Housekeeping | Resistor                        | 56 Ω, always on |
| TT&C               | Resistor + Pulse Voltage        | 18 Ω Short bursts via pulse |
| Payload            | Resistor + Pulse Voltage        | 27 ΩActive during sun only |

## ⚙️ Assumptions
1.*Orbit profile**: 90-minute orbit scaled down to 5.4 seconds (3.6 s sun, 1.8 s eclipse).
2. **Solar panel voltage**: 7 V during sunlight, 0 V during eclipse.
3. **Switching frequency**:  
   - 1 / (5.4 s) = **185 mHz**  
   - Duty cycle = 66.7% (sunlight), 33.3% (eclipse).
4. **Battery model**:  
   - Capacitance: **3000 µF (3 mF)**  
   - Initial voltage: 0 V (uncharged)  
   - Max voltage: 9 V (represents full SOC).
   - Internal resistance: 50 mΩ.

3. **Stepwise Circuit Building**
   - Ground nodes set.
   - Solar pulse source connected through series resistor to battery bus.
   - Battery connected with internal resistance.
   - Loads connected with pulse sources to simulate timed behavior.
   - Oscilloscopes and probes monitor battery voltage/current and loads.

4. **Reasoning Behind Choices**
   - Pulse sources replaced PWL and VC switches due to CircuitJS limitations.
   - Series resistors simulate EPS losses and prevent unrealistic currents.
   - Pulse timing aligns with orbit sun/eclipse profile.

---

## Tools Used
- CircuitJS ([https://www.falstad.com/circuit/circuitjs.html](https://www.falstad.com/circuit/circuitjs.html))
- AI Assistance: ChatGPT (component selection and Pulse workaround guidance)
- NASA CubeSat 101 Guide ([link](https://www.nasa.gov/wp-content/uploads/2017/03/nasa_csli_cubesat_101_508.pdf))
- Electronics textbooks (voltage/current/resistor sizing)

---

## Run / Open Instructions
1. Open [CircuitJS](https://www.falstad.com/circuit/circuitjs.html)
2. Import `.cir` or JSON from `src/`
3. Place current probes on battery and loads.
4. Press **Run / Play**
5. Observe Vbatt, Ibatt, and load currents.
6. Adjust pulse parameters to simulate TT&C bursts and Payload sun-only operation.

---

## Outputs
- Circuit files in `src/`
- Screenshots in `figures/`
- Observed behavior documented in `RESULTS.md`

---

## Limitations
- SOC not quantitatively implemented due to CircuitJS limitations.
- Pulse sources used for TT&C/Payload instead of VC switches.



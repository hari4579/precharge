# EV Precharge Circuit

## Project Overview

This project involves the design and development of a precharge circuit for an Electric Vehicle (EV) high-voltage system. The circuit limits the initial inrush current when charging the intermediate DC-link capacitor before the main tractive-system connection is established.

The development process follows three stages:

1. **Simulation:** Validate the electrical behaviour using LTspice.
2. **Prototyping:** Assemble and evaluate the circuit using a breadboard prototype.
3. **PCB Implementation:** Develop a custom PCB for the physical implementation of the circuit.

The design also incorporates a PC817 optocoupler for signal isolation between the relevant control and interfaced circuit sections.

## Electrical Specifications

| Parameter | Value |
|---|---:|
| Maximum tractive-system voltage | 168 V |
| Precharge resistance | 150 Ω |
| Intermediate DC-link capacitance | 4512 µF |
| Calculated precharge time | 2.373 s |
| EV 5.7 compliance | Yes |

## Precharge Circuit Design

The precharge circuit is intended to limit the current flowing into the intermediate DC-link capacitor during initial energisation.

Without precharging, connecting a discharged capacitor directly to the high-voltage battery can result in a large inrush current.

The precharge resistor provides a controlled charging path. Once the capacitor voltage approaches the required level, the main connection can be established according to the vehicle's shutdown and startup control sequence.

### Precharge Components

| Component | Part number / Value |
|---|---|
| Precharge resistor | THS75 – 150 Ω, 5% |
| Precharge relay | ECK50BH4AAA |
| Connector | 2068320201 |
| Optocoupler | PC817 |
| Intermediate capacitor | 4512 µF |

## Precharge Calculations

The precharge circuit uses a 150 Ω resistor and an intermediate capacitance of 4512 µF.

The RC time constant is:

\[
\tau = R \times C
\]

\[
\tau = 150 \times 4512 \times 10^{-6}
\]

\[
\boxed{\tau = 0.6768\text{ s}}
\]

The capacitor charging voltage follows:

\[
V_C(t)=V_S\left(1-e^{-t/RC}\right)
\]

Using the calculated RC time constant, the selected precharge interval is approximately 2.373 seconds.

At a maximum system voltage of 168 V, the initial theoretical current through the precharge resistor is:

\[
I_0=\frac{V}{R}
\]

\[
I_0=\frac{168}{150}
\]

\[
\boxed{I_0=1.12\text{ A}}
\]

The corresponding initial resistor power is:

\[
P_0=I_0^2R
\]

\[
P_0=(1.12)^2\times150
\]

\[
\boxed{P_0=188.16\text{ W}}
\]

These are initial theoretical values. Actual resistor selection and operation must account for pulse-energy capability, duration, repetition rate, and thermal limits rather than relying only on continuous power rating.

## Low-Voltage Control and Isolation

The low-voltage control circuitry manages the precharge control signals and interfaces with the switching circuitry.

### PC817 Optocoupler

A PC817 optocoupler is incorporated to provide galvanic signal isolation between the input and output sides of the interfaced control circuit.

Its operation is based on optical signal transfer:

- An input current drives the internal LED.
- The LED emits light inside the optocoupler.
- The phototransistor on the output side responds to the light.
- The output signal is transferred without a direct electrical connection between the two sides.

This arrangement helps isolate the control signal path from electrical disturbances on the interfaced side.

**Note:** The PC817 provides signal isolation, not isolated power. Appropriate isolated supplies, PCB creepage and clearance, and circuit-level voltage ratings are required to maintain the intended isolation.

## Development and Prototyping Workflow

The circuit was developed through a progressive workflow, moving from simulation to physical prototyping and finally to PCB implementation.

### 1. LTspice Simulation

The circuit was first evaluated using LTspice to study its electrical behaviour before hardware implementation.

The simulation documentation includes the voltage and current response of the precharge circuit.

**Simulation files and plots:**
<img width="1910" height="1017" alt="image" src="https://github.com/user-attachments/assets/c2024095-dbbc-4c22-8aea-f20942e7f628" />


### 2. Breadboard Prototype

After simulation, the control circuit was assembled on a breadboard to evaluate the circuit implementation and signal behaviour.

This stage provided an opportunity to inspect the control circuitry and PC817-based signal isolation before moving to a dedicated PCB.

**Breadboard prototype photographs:**

<img width="1280" height="960" alt="WhatsApp Image 2026-10-30 at 2 12 25 PM" src="https://github.com/user-attachments/assets/dcc8cd31-6583-49af-90c9-7c2277c7b693" />


### 3. PCB Design and Implementation

Following the prototyping stage, the circuit was transferred to a custom PCB.

The PCB provides a dedicated physical implementation of the circuit, with component placement, routing, and interfaces arranged according to the schematic.

The design incorporates the PC817 optocoupler for signal isolation.

**PCB design documentation:**
<img width="1273" height="670" alt="image" src="https://github.com/user-attachments/assets/d65d9cec-917b-47ba-a4dd-2289fc79ec72" />


*Replace the image paths above with the actual image locations in the repository.*

## Schematics and Design Documentation

The repository includes the following design references:

| Design document | Description |
|---|---|
| HV Precharge Schematic | High-voltage precharge path |
| LV Control Schematic | Low-voltage control circuitry |
| LTspice Simulation | Circuit simulation and response curves |
| PCB Layout | Custom PCB design |

## Component Datasheets

The following datasheets are provided for the selected components.

| Component | Datasheet |
|---|---|
| THS75 – 150 Ω resistor | [View Datasheet](https://drive.google.com/file/d/1Oysi_V5_6Vg3fTnCHVQIcoAkNiTrOapR/view?usp=sharing) |
| ECK50BH4AAA – Precharge relay | [View Datasheet](https://drive.google.com/file/d/14o_R9FOyqE87r770coP1-ShiYe6dFc8x/view?usp=sharing) |
| 2068320201 – Connector | [View Datasheet](https://drive.google.com/file/d/17dPSpHEJCGt1xTEilI5NliNfd4M-F8Sz/view?usp=sharing) |
| PC817 – Optocoupler | [View Datasheet](https://www.farnell.com/datasheets/73758.pdf) |

## EV Rule Compliance

The precharge circuit was designed with the EV 5.7 requirement in consideration.

| Requirement | Design status |
|---|---|
| EV 5.7 compliance | Yes |

Refer to the applicable competition rulebook and the team's electrical inspection documentation for the final compliance assessment.

## Conclusion

This project covers the development of an EV precharge circuit from electrical calculations and LTspice simulation through breadboard prototyping and custom PCB implementation.

The design uses a 150 Ω precharge resistor, a 4512 µF intermediate capacitor, a dedicated precharge relay, and PC817-based signal isolation in the control circuitry.

The progressive development workflow provides a documented path from circuit-level analysis to physical hardware implementation.

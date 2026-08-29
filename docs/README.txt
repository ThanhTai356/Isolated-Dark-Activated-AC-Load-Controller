# Isolated Dark-Activated AC Load Controller

An analog hardware and PCB design project that automatically controls 220V AC mains loads based on ambient light levels. Built and verified from simulation to a physical single-sided PCB prototype.

---

## Hardware Overview & Results

| Schematic Design | PCB Layout & 3D Model | Fabricated Hardware |
| :---: | :---: | :---: |
| ![Schematic](docs/schematic.png) | ![PCB](docs/pcb.png) | ![Hardware](docs/hardware.png) |

---

## Circuit Architecture & Working Principle

The system consists of 4 main functional blocks:

1. **Power Supply Block (Linear PSU):**
   - Step-down transformer converts `220V AC` down to `9V AC`.
   - Full-bridge diode rectifier (`1N4007` x4) and capacitor filter network (`1000uF`, `100nF`) convert AC to unregulated DC.
   - `LM7805` linear voltage regulator outputs a stable `5V DC` rail with LED power indication.

2. **Sensor Block (Ambient Light Sensing):**
   - Cadmium Sulfide (CdS) photoresistor (`LDR`) in a voltage-divider configuration with a `10kΩ` potentiometer (`RV1`) for threshold sensitivity adjustment.
   - **Bright Environment:** LDR resistance drops $\rightarrow$ Divider output voltage drops below reference.
   - **Dark Environment:** LDR resistance increases $\rightarrow$ Divider output voltage rises above reference.

3. **Comparator Block:**
   - `LM358` Operational Amplifier configured as an analog voltage comparator.
   - Compares the sensing voltage at non-inverting input ($V_+$, Pin 3) with a fixed $2.5\text{V}$ reference created by a $10\text{k}\Omega / 10\text{k}\Omega$ voltage divider at inverting input ($V_-$, Pin 2).
   - $V_+ > V_-$ (Dark): Output drives to High (`~5V`).
   - $V_+ < V_-$ (Light): Output drives to Low (`0V`).

4. **Driver & Isolated Switching Block:**
   - NPN Transistor `C945` (via `1kΩ` base resistor) acts as a low-side switch to drive a `5V SPDT Relay`.
   - Flyback protection diode (`1N4007`) connected across the relay coil suppresses inductive voltage spikes during turn-off.
   - Relay contacts provide galvanic isolation to switch the `220V AC` lamp safely.

---

## Hardware Specifications & Components

| Component | Part / Value | Role |
| :--- | :--- | :--- |
| **Light Sensor** | CdS LDR (`TORCH_LDR`) | Ambient illuminance detection |
| **Comparator** | LM358 | Threshold comparison |
| **BJT Switch** | 2SC945 (NPN) | Low-side relay coil driver |
| **Voltage Regulator** | LM7805 | 5V DC regulation |
| **Rectifier Diodes** | 1N4007 | Full-bridge rectification & Flyback protection |
| **Relay** | 5V SPDT Relay | Galvanic isolation & 220V AC load switching |
| **EDA Tool** | Proteus Design Suite | Schematic capture, SPICE simulation, and PCB layout |

---

## Repository Structure

```text
├── docs/
│   ├── schematic.png        # Full circuit schematic
│   ├── pcb.png              # PCB layout & 3D visualization
│   └── hardware.png         # Photograph of the assembled PCB unit
├── simulation/
│   └── circuit_design.pdsprj # Proteus project file
└── README.md

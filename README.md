# Multi-Stage Discrete Audio Amplifier Design & Simulation

A comprehensive, high-efficiency audio power amplifier designed and simulated entirely from scratch using **discrete electronic components** (MOSFETs, BJTs, and passives) without relying on integrated operational amplifiers (op-amps). This project covers the entire engineering pipeline: from rigorous analytical manual calculations to multi-stage LTspice validation and hardware testing.

Developed as a core laboratory project for the **EE-313 Electronic Circuit Design** course at NUST.

---

## 📡 Project Overview & Specifications

The system captures low-level millivolt signals from an electret condenser microphone and amplifies them through a structured multi-stage topology to drive a low-impedance loudspeaker load.

* **Output Power:** Delivers 3–5 W of continuous power into an 8-Ω speaker load.
* **Frequency Response:** Stable, flat bandwidth across the complete audio spectrum (100 Hz to 20 kHz).
* **Power Supply:** Operating off a single +24V DC voltage rail.
* **Design Strategy:** Reverse-engineered stage-by-stage parameters from the final Class-AB power stage backward to the initial pre-amplifier to prevent cross-stage loading and ensure maximum power transfer.

---

## 🛠️ System Architecture & Engineering Stages

The amplifier is partitioned into specialized blocks, each calculated independently to optimize impedance matching and gain linearity:

### 1. MOSFET Pre-Amplifier Stage (2N7000)
* **Purpose:** Implemented to provide an exceptionally high input impedance at the front-end, ensuring zero signal degradation or loading effects on the high-impedance electret microphone source.

### 2. BJT Pre-Amplifier Stage (2N3904)
* **Purpose:** Configured as a common-emitter block to drive the primary voltage amplification and achieve high voltage gain.

### 3. Combined Pre-Amplifier with Feedback
* **Purpose:** Merged the MOSFET and BJT blocks into a unified high-gain stage. Integrated a negative feedback network to stabilize total AC gain ($A_v \approx 100$), minimize Total Harmonic Distortion (THD), and extend the amplifier's high-frequency cutoff.

### 4. PNP Driver Stage (2N3906)
* **Purpose:** Functions as a critical current buffer between the high-gain pre-amplifier and the low-impedance output stage. Engineered to provide high current gain, improve overall voltage swing, and insulate the pre-amplifier from downstream loading.

### 5. Class-AB Power Amplifier Output Stage (TIP122 / TIP127)
* **Purpose:** Utilizes complementary Darlington pairs to deliver the final 3–5 W of power directly to the 8-Ω speaker. Features a precision diode-biasing string ($1\text{N}4148$) to eliminate crossover distortion by maintaining an optimized quiescent current ($I_Q \approx 17.3\text{ mA}$).

---

## 📊 Analytical Framework & Core Equations

All component choices and biasing netlists were verified manually before running CAD simulations. Detailed step-by-step mathematical treatments can be found inside the attached engineering report:

* **Supply Rail Design ($V_{CC}$):** Calculated to prevent clipping at peak unclipped output voltage swing:
  $$V_{CC} = \sqrt{8 P R_L} + V_{CE(sat1)} + V_{CE(sat2)} + V_{drop} \approx 24\text{V}$$
* **Quiescent Current Optimization:** Balanced to avoid thermal runaway while eliminating distortion:
  $$I_Q \approx 17.3\text{ mA}$$
* **Impedance Matching Framework:** Checked across cascading junctions to guarantee efficient inter-stage signal routing:
  $$R_{in} = R_4 \parallel R_5 \parallel [(\beta + 1) \cdot R_{6(unbypassed)}] \approx 820\,\Omega$$

---

## 📂 Repository Resources & Quick Links

This repository contains all design assets and source files required to clone, inspect, and run the project:

* 📄 **[Click Here to View the Complete Project Report](./ECD%20project%205th%20sem.pdf)** — Full manual circuit derivations, component tables, calculations, and hardware performance summaries.
* 💻 **[Download the LTspice Schematic File](./Audio_amp.asc)** — Complete master `.asc` circuit model file containing all stages integrated for instant simulation testing.

### How to Run the Simulation:
1. Download and open the `Audio_amp.asc` file inside **LTspice**.
2. Run the transient analysis command (`.tran 10ms`) already set up in the schematic.
3. Probe across the input node ($V_{in}$) and load resistor ($R_3$) to view the unclipped, amplified audio waveforms.

---

## 📸 Simulation Waveforms & Laboratory Testing

### 1. Unified Schematic Layout (LTspice)
<img width="1373" height="722" alt="image" src="https://github.com/user-attachments/assets/2798d94b-a3f1-4d15-af1e-d75557130291" />

### 2. Transient Analysis: Input vs. Output Voltage Waves
<img width="1920" height="868" alt="image" src="https://github.com/user-attachments/assets/41810f99-1c8d-423e-b0c0-711d5e5cad28" />

<img width="1920" height="868" alt="image" src="https://github.com/user-attachments/assets/18b51f6a-8965-462a-b605-4c7f87371315" />


### 3. Physical Hardware Prototype Validation
<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/9a48a656-1511-49c7-8ed9-8e4f3b4a6192" />

https://github.com/user-attachments/assets/cb480c99-ae21-41a2-b12d-da118b1a7c28

The final physical build validated our mathematical constraints, confirming proper transistor biasing, high fidelity audio response, and robust stability across the entire 100 Hz to 20 kHz audio bandwidth.

---

## 👥 Project Team & Credits

This project was successfully executed by **Syndicate B** at the Department of Electrical Engineering, College of E&ME, NUST Rawalpindi:

* **Laiba Zulfiqar** (Reg: 465606) — Core System Analysis, Manual Calculations & Documentation
* **Saira Naseer** (Reg: 464119)
* **Aziz ur Rehman** (Reg: 474104)

**Course Instructor:** Dr. Mojeeb Bin Ihsan  
**Lab Instructor:** LE Syed Moiz Hussain

# TPS5430 Dual Buck Converter Module

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![KiCad](https://img.shields.io/badge/EDA-KiCad_9.0+-blue)
![License](https://img.shields.io/badge/License-Educational-green)
![IC](https://img.shields.io/badge/IC-TPS5430_%C3%972-red)
![Vin](https://img.shields.io/badge/Vin-14.4V--25.2V-yellow)
![Vout](https://img.shields.io/badge/Vout-3.3V_%7C_5V_%7C_12V-purple)
![Iout](https://img.shields.io/badge/Iout-3A_max-orange)
![Fsw](https://img.shields.io/badge/Fsw-500kHz-lightblue)

---

## 📖 Introduction

This project presents the design and implementation of a **DC/DC Buck Converter (Step-Down) Power Supply Module** using **two Texas Instruments TPS5430** ICs. The module accepts a wide input voltage range of **14.4V – 25.2V** and delivers multiple regulated output rails suitable for embedded systems and microcontroller-based applications.

Key features include a **3-mode adjustable main output (VP)**, dual auxiliary LDO rails, a **Power Good LED indicator**, and a **configurable overcurrent protection** threshold set via a shunt resistor.

**Course:** Power Electronics and Applications — Course Code: `BTL_DTCSUD`

---

## 🖼️ PCB Images

### Schematic Overview
> 📷 *[Insert full schematic image here]*

---

### PCB Layout — Top Layer
<img width="951" height="677" alt="image" src="https://github.com/user-attachments/assets/e8deac5c-959e-4de4-999b-f91b19d99dd1" />


---

### PCB Layout — Bottom Layer
<img width="951" height="677" alt="image" src="https://github.com/user-attachments/assets/356c21df-f1db-49d4-b3e9-93e6744f4099" />


---

### 3D Render
<img width="1184" height="881" alt="image" src="https://github.com/user-attachments/assets/3718d535-6884-40cc-8554-7f9df016935c" />

<img width="1184" height="881" alt="image" src="https://github.com/user-attachments/assets/60e26b26-7153-46f1-80bd-1a86d4939a92" />


---

### Assembled Board
> 📷 *[Insert photo of the soldered/assembled board here]*

---

## ⚙️ Technical Specifications

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Input Voltage ($V_{IN}$)** | 14.4V – 25.2V | Recommended operating range |
| **Main Output VP** | **5V / 12V / 3.3–12V** | 3 selectable modes |
| **VP Output Current** | Max **3A** | High-efficiency switching mode |
| **Auxiliary Output 1** | **5V** | Via LDO, for logic circuits |
| **Auxiliary Output 2** | **3.3V** | Via LDO, for MCUs (ESP32, STM32, etc.) |
| **Switching Frequency** | 500 kHz | Fixed internal oscillator |
| **Buck IC** | 2× TPS5430 | Texas Instruments |
| **Overcurrent Protection** | Configurable | Set via shunt resistor value |
| **Power Good Indicator** | LED (VP rail) | Signals stable output on VP |

---

## 🛠️ Design Details

### 1. Dual TPS5430 Architecture

The module employs **two independent TPS5430 ICs**:
- **IC1:** Drives the main output rail **VP**, supporting 3 selectable voltage modes.
- **IC2:** *(Describe the role of the second IC here — e.g., secondary rail, redundancy, or higher current capacity)*

### 2. Three-Mode Main Output (VP)

The VP rail supports three operating modes, selected via a switch or jumper:

| Mode | Output Voltage | Configuration |
| :---: | :---: | :--- |
| **Mode 1** | **5V** | Fixed feedback resistor network |
| **Mode 2** | **12V** | Fixed feedback resistor network |
| **Mode 3** | **3.3V – 12V** | Adjustable via potentiometer |

### 3. Feedback Network Calculation

The output voltage is set by a resistor divider ($R_1$, $R_2$) connected to the **VSENSE** pin, based on the internal reference $V_{ref} = 1.221V$:

$$V_{OUT} = V_{ref} \times \left(1 + \frac{R_1}{R_2}\right)$$

**With $R_1 = 10k\Omega$ (fixed):**

- **5V Mode:**

$$R_2 = \frac{R_1 \times V_{ref}}{V_{OUT} - V_{ref}} = \frac{10000 \times 1.221}{5.0 - 1.221} \approx 3.24k\Omega$$

- **12V Mode:**

$$R_2 = \frac{10000 \times 1.221}{12.0 - 1.221} \approx 1.13k\Omega$$

- **Variable Mode:** $R_2$ is replaced with a **5kΩ potentiometer in series with a 1kΩ fixed resistor**, allowing continuous adjustment from **3.3V to 12V**.

### 4. Auxiliary LDO Outputs (5V & 3.3V)

Both LDO regulators are cascaded from the **5V Buck output**, not directly from $V_{IN}$:
- **Reason:** Reduces the voltage drop across each LDO, minimizing power dissipation ($P_D = \Delta V \times I_{load}$).
- **Benefit:** Allows the use of compact packages (e.g., SOT-223) without thermal issues.

### 5. Power Good LED Indicator

A **Power Good LED** is connected to the VP rail. The LED lights up when VP reaches its target voltage, confirming stable regulation before connecting a load.

### 6. Configurable Overcurrent Protection

A **low-side shunt resistor** sets the overcurrent trip threshold. Changing the resistor value adjusts the protection level to match the target application's requirements. The sensing node is labeled **ISENSE** in the schematic.

---

## 📂 Project Structure

```text
BTL_DTCSUD/
├── docs/                       # Documentation & Report files
│   └── ...
├── Kicad/                      # Hardware Design Files
│   └── Buck_TPS5430/
│       ├── *.kicad_sch         # Schematic file
│       ├── *.kicad_pcb         # PCB Layout file
│       └── ...
├── reference/                  # Datasheets & Assignment requirements
│   └── ...
├── .gitignore
├── GIT_GUIDE
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- **[KiCad EDA](https://www.kicad.org/)** — Version 9.0 or higher recommended
- **[Git](https://git-scm.com/)** — For version control

### Installation

**Option 1: Clone via Git (Recommended)**
```bash
git clone https://github.com/nhq441/design_TPS5430_regulator.git
```

**Option 2: Download ZIP**
1. Click the green **<> Code** button at the top right of this repository page.
2. Select **Download ZIP**.
3. Extract the `.zip` file to your working directory.

### Opening the Project
1. Launch **KiCad**.
2. Navigate to: `Kicad/Buck_TPS5430/`
3. Open: `Buck_TPS5430.kicad_pro`

---

## 🤝 Contributing

This project follows the **Gitflow Workflow**:

- **`main`**: Stable, verified designs only.
- **`develop`**: Primary integration branch for ongoing work.
- **`feature/*`**: Individual feature branches (e.g., `feature/Schematic`, `feature/PCB-Layout`).
  - Always branch from `develop` and merge back via Pull Request.

---

## 📄 License

This project is developed for **educational purposes** within the scope of the **Power Electronics and Applications** course.

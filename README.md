# TPS5430 Buck Converter Module

![Status](https://img.shields.io/badge/Status-Work%20In%20Progress-orange)
![KiCad](https://img.shields.io/badge/EDA-KiCad_9.0+-blue)
![License](https://img.shields.io/badge/License-Educational-green)

## 📖 Introduction
This project focuses on the design and implementation of a **Step-down (Buck) DC-DC power supply module** utilizing the **Texas Instruments TPS5430** IC. The module is engineered to accept a wide input voltage range (up to 35V) and convert it into a stable **5V output** capable of delivering up to **3A** of continuous current.

In addition to the main power rail, the board integrates an auxiliary **3.3V LDO** linear regulator to power low-voltage logic circuits, making it suitable for modern microcontrollers such as the ESP32 or STM32.

**Course Context:** Major Assignment 1 (Bài tập lớn 1) - Course Code: `BTL_DTCSUD`.

---

## ⚙️ Technical Specifications

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Input Voltage ($V_{IN}$)** | 10V - 35V | Recommended operating range. |
| **Output Voltage 1** | **5.0V/12V** | Regulated via TPS5430 Buck Converter. |
| **Output Current 1** | Max **3A** | High-efficiency switching mode. |
| **Output Voltage 2** | **3.3V** | Regulated via AMS1117/LM1117 LDO. |
| **Switching Frequency** | 500 kHz | Fixed internal oscillator. |

---

## 🛠️ Design Considerations

### 1. Enable Pin Configuration (TPS5430)
The **ENA pin (Pin 5)** is configured with a mechanical switch to control the operation of the regulator:
* **ON State:** Switch Open (Floating). The internal pull-up source enables the device.
* **OFF State:** Switch Closed (Connected to GND). The device stops switching when voltage is $< 0.5V$.

> **⚠️ CRITICAL WARNING:**
> Do **NOT** connect an external pull-up resistor from the ENA pin to the main input ($V_{IN}$). The absolute maximum rating for the ENA pin is **7V**. Connecting it to 12V or 24V will permanently damage the IC.

### 2. Feedback Network Calculation
To ensure a precise 5V output, the voltage divider network ($R_1, R_2$) connected to the **VSENSE** pin is calculated based on the internal reference voltage ($V_{ref} = 1.221V$):

* **$R_1$ (Top Resistor):** $10k\Omega$ (Recommended fixed value).
* **$R_2$ (Bottom Resistor):** using the standard transfer formula:

$$R_2 = \frac{R_1 \times V_{ref}}{V_{OUT} - V_{ref}} = \frac{10000 \times 1.221}{5.0 - 1.221} \approx 3.24k\Omega$$

Similar with 12V ouput:

$$R_2 = 1.23k\Omega$$

### 3. LDO Thermal Management (3.3V Rail)
The input of the 3.3V LDO is cascaded from the **5V Buck output**, rather than the main high-voltage input ($V_{IN}$).
* **Reasoning:** This minimizes the voltage drop across the linear regulator ($V_{drop} = 5V - 3.3V = 1.7V$).
* **Benefit:** Significantly reduces power dissipation ($P_D = V_{drop} \times I_{load}$), allowing the use of smaller packages (e.g., SOT-223) without overheating.

### 4. Current Sensing
A low-side shunt resistor is integrated into the design layout to facilitate current monitoring. The measurement node is labeled **ISENSE**.

---

## 📂 Project Structure

```text
BTL_DTCSUD/
├── docs/                       # Documentation & Report files
│   └── conference-template-a4.docx
├── Kicad/                      # Hardware Design Files
│   └── Buck_TPS5430_Project/
│       ├── *.kicad_sch         # Schematic file
│       ├── *.kicad_pcb         # PCB Layout file
│       └── ...
├── reference/                  # Datasheets & Assignment Requirements
│   ├── Bai tap lon 1.docx      # Project Requirements
│   └── tps5430.pdf             # Main IC Datasheet
├── .gitignore                  # Git ignore configuration
└── README.md                   # Project documentation
```

## 🚀 Getting Started

### Prerequisites
Before you begin, ensure you have the following software installed:
* **[KiCad EDA](https://www.kicad.org/)**: Version 9.0 is highly recommended for compatibility.
* **[Git](https://git-scm.com/)**: For version control and repository management.

### 📥 Installation

#### Step 1: Get the Project Files
Choose one of the following methods to download the source code:

**Option 1: Clone via Git (Recommended) 🧑‍💻**
This method is best if you want to easily update the project later or contribute changes.
```bash
git clone [https://github.com/nhq441/design_TPS5430_regulator.git](https://github.com/nhq441/design_TPS5430_regulator.git)
```

**Option 2: Download ZIP 📦**
Choose this if you are not familiar with Git or just want the files quickly without version control.
1. Click the green **<> Code** button at the top right of this repository page.
2. Select **Download ZIP** from the dropdown menu.
3. Extract the downloaded `.zip` file to your working directory.

#### Step 2: Open the Project 📂
Once you have the files on your computer:
1. Launch **KiCad**.
2. Navigate to the project directory: `Kicad/Buck_TPS5430_Project/`
3. Open the project file: `Buck_TPS5430_Project.kicad_pro`

---

## 🤝 Contributing

This project follows the standard **Gitflow Workflow** to ensure organized development:

* **`main`**: Reserved for stable, production-ready code/designs.
* **`develop`**: The primary integration branch for ongoing work.
* **`feature/*`**: Branches for specific tasks or features (e.g., `feature/Schematic`, `feature/PCB-Layout`).
    * *Please create feature branches from `develop` and merge back via Pull Request.*

---

## 📄 License

This project is developed strictly for **educational purposes** within the scope of the **"Power Electronics and Applications"** course.

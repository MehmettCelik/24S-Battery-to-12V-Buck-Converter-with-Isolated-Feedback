## 📌 About the Project
This project was developed to provide a highly reliable, low-noise 12V auxiliary power supply for electric vehicles and high-voltage energy storage systems. 
Designed within the Hydromarmara team by Mehmet Celik, this hardware acts as a precision Power Distribution Board (PDB) / DC-DC Buck Converter. 
The core design specifically focuses on safely stepping down a 24S battery pack voltage to a stable 12V output, utilizing an isolated feedback loop to ensure maximum stability and noise immunity for sensitive analog and digital modules.

### Key Features
* **Input Voltage:** Up to ~100.8V (Designed for 24S Li-ion battery packs)
* **Output Voltage:** 12V DC (Regulated)
* **Topology:** High-Voltage Step-Down (Buck) Converter with Isolated Feedback
* **Switching Frequency:** 250kHz
* **Target Application:** Providing ultra-low ripple auxiliary power to sensitive MCUs, sensors, and communication interfaces.

---

## 🛠️ Core Components & Working Principle

Unlike standard converters, this design prioritizes a clean output and high-voltage safety. The control and voltage regulation stages are driven by the following core components:

| Hardware Unit | Component Code | Role in Project & Working Principle |
| :--- | :--- | :--- |
| **PWM Controller** | `UC3845` | High-performance current-mode PWM controller. It drives the main high-voltage MOSFET to step down the 100V input. The current-mode architecture ensures a rapid transient response to sudden load changes. |
| **Precision Reference** | `TL431` | Acts as an adjustable precision shunt regulator on the 12V output side. It continuously monitors the output voltage and detects even the slightest voltage deviations (ripple). |
| **Optocoupler** | `LTV-356T` | Provides galvanic isolation for the feedback loop. It securely transmits the voltage error signal from the TL431 (low-voltage side) back to the UC3845 (high-voltage side) without coupling electrical noise between the two domains. |

*(For the full list of passive components, MOSFETs, and diodes, refer to the `Hardware/BOM.csv` file.)*

---

## 📊 Performance Characteristics (Simulated)
The system has been rigorously tested via LTSpice for various steady-state and load transient scenarios. The isolated feedback loop ensures exceptional voltage regulation with extremely low ripple, proving its capability to feed sensitive electronics.

| Test Condition | Input Voltage (Vin) | Efficiency (η) | Output Ripple (Vripp) |
| :--- | :--- | :--- | :--- |
| **0.1A Steady, 0.2A Transient** | 100.8V | 61.00% | ±0.058% |
| **0.3A Steady, 0.4A Transient** | 100.8V | 76.08% | ±0.075% |

---

## 📂 Folder Structure
```text
📦 24S-to-12V-Buck-Converter
 ┣ 📂 Hardware
 ┃ ┣ 📜 Schematic.pdf
 ┃ ┣ 📜 PCB_Layout.pdf
 ┃ ┣ 📂 3D
 ┃ ┗ 📜 BOM.csv
 ┣ 📂 Simulation
 ┃ ┣ 📜 Buck_Converter.asc
 ┃ ┗ 📜 transient_plot.plt
 ┗ 📜 README.md

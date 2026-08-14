# Closed-Loop UVC LED Buck Converter Driver for Water Disinfection

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform: Arduino](https://img.shields.io/badge/Platform-Arduino%20Nano-00979D.svg)](https://www.arduino.cc/)
[![EDA: KiCad 8.0](https://img.shields.io/badge/EDA-KiCad%208.0-314194.svg)](https://kicad.org/)
[![Simulation: LTspice](https://img.shields.io/badge/Simulation-LTspice-FF0000.svg)](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)

A custom closed-loop asynchronous buck converter designed to drive an 8-LED **Crystal IS Klaran UVC array (SA265-35030-SA1)** in a **2S4P** configuration for *E. coli* inactivation in water. 

Developed at the **Department of Instrumentation and Applied Physics, Indian Institute of Science (IISc), Bangalore** under the supervision of **Prof. Sanjiv Sambandan**.

---

## 📌 System Specifications

| Parameter | Value | Details |
| :--- | :--- | :--- |
| **Input Voltage ($V_{\text{in}}$)** | `18 V` | Primary DC supply rail |
| **Output Voltage ($V_o$)** | `14 V` | Nominal string voltage ($2 \times V_F$) |
| **Target Output Current ($I_o$)** | `2.0 A` | `500 mA` across 4 parallel strings |
| **Switching Frequency ($f_s$)** | `20 kHz` | Timer1 Fast PWM mode |
| **Operating Duty Cycle ($D$)** | `77.8%` | Calculated for $18\text{V} \to 14\text{V}$ conversion |
| **Conduction Mode** | `CCM` | Continuous Conduction Mode across all loads |
| **Target Pathogen** | *E. coli* | 4-log ($99.99\%$) inactivation target |
| **Target UV Dose** | `15–20 mJ/cm²` | Delivered at $265\text{ nm}$ germicidal wavelength |

---

## ⚡ Key Hardware Features

* **High-Side MOSFET Driving:** Uses an **IR2110** high-side driver IC with a bootstrap network ($D_3$, $C_1$) to fully enhance the high-side N-channel MOSFET (**IRLZ44N**) without gate pulse degradation.
* **Transient Snubber:** Integrated RCD snubber ($12\text{ k}\Omega$, $30\text{ nF}$, 1N4148) across the freewheeling diode (**1N5822**) to suppress high-frequency switching ringing.
* **Precision Feedback:** Current sensing via an **ACS712-05A** Hall-effect module ($185\text{ mV/A}$ sensitivity) linked to an **Arduino Nano** running a discrete **PI current control** loop.
* **Onboard Regulation:** Integrated **L7812** regulator powering the driver $V_{CC}$ and microcontroller input rail.

---

## 📊 LTspice Simulation Results

Simulation under full load ($7\,\Omega$ equivalent array resistance) confirmed Continuous Conduction Mode (CCM):

| Parameter | Design Target | Simulated Value | Status |
| :--- | :--- | :--- | :---: |
| **Output Voltage ($V_o$)** | $14.00\text{ V}$ | **$13.91\text{ V}$** | ✅ Pass |
| **Output Current ($I_o$)** | $2.00\text{ A}$ | **$1.99\text{ A}$** | ✅ Pass |
| **Inductor Ripple ($\Delta I_L$)** | $\le 200\text{ mA}$ | **$157\text{ mA}$** ($7.8\%$) | ✅ Pass |
| **Output Voltage Ripple ($\Delta V_o$)** | $\le 0.35\text{ V}$ | **$0.10\text{ V}$** | ✅ Pass |

---






## 📜 Author & Citation

* **Author:** Aarav C Balaji  
* **Advisor:** Prof. Sanjiv Sambandan  
* **Affiliation:** Department of Instrumentation and Applied Physics, Indian Institute of Science (IISc), Bangalore  


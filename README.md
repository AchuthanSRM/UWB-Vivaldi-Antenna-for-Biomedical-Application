# Double-Slot Ultra-Wideband (UWB) Vivaldi Antenna for Biomedical Applications

![Antenna Fabricated Prototype](antenna_photo.jpg)

## Overview
This repository contains the design, simulation files, and testing results for a **Double-Slot Ultra-Wideband (UWB) Vivaldi Antenna** optimized for medical imaging and sensing systems. The antenna is designed for early detection and monitoring of medical problems, such as cancerous tumors and non-contact health monitoring. 

By utilizing two symmetrical tapered slots and a vertical feed splitter, this design achieves excellent directional radiation, high gain, and stable impedance matching across a wide frequency band, while strictly adhering to biomedical safety limits (SAR).

## Key Features & Physical Specifications
* **Substrate Material:** Rogers RO4003C ($\epsilon_r = 3.55$, Thickness = $0.813$ mm) for low dielectric loss at microwave frequencies.
* **Double-Slot Configuration:** Two symmetrical tapered slots ensure balanced surface current distribution and enhanced directivity.
* **Microstrip Feedline & Splitter:** A feedline (Length = $13$ mm, Width = $1.2$ mm) connected to a vertical splitter divides the signal equally into two branches for uniform excitation.
* **Corrugated Edges:** 28 periodic corrugations ($1.7$ mm wide, spaced $2.1$ mm apart) are introduced along the antenna edges. These suppress surface waves and significantly improve radiation performance.
* **Copper Layer:** $0.035$ mm thickness.

## Antenna Geometry & Mathematical Modeling
The tapered slots of the Vivaldi antenna structures are defined by an exponential flare to allow for a gradual increase in slot width. This ensures a smooth transition of the electromagnetic wave propagation from the guiding mode to the radiation mode.

The generalized exponential taper profile is defined as:

$$
y(x) = C \cdot e^{ax}
$$

Where $C$ is the initial slot width constant, $a$ is the taper rate, and $x$ is the position along the length of the antenna. 

For the specific parametric curve generation in CST Studio Suite, the primary outer flare curve is modeled using the following set of equations:

$$
X(t) = X_{offset} + t
$$

$$
Y(t) = W_s + G \cdot \exp \left( \ln \left( \frac{W - W_s}{G} \right) \cdot \left( \frac{t}{L_{slot}} \right) \right)
$$

$$
Z(t) = H_{sub}
$$

**Design Parameters:**
* $X_{offset} = 20$ mm
* $W_s$ (Inner ridge/finger width) = $30$ mm
* $G$ (Throat gap) = $0.3$ mm
* $W$ (Total mouth width) = $95$ mm

### Impedance & Return Loss
The characteristic impedance ($Z_0$) of the microstrip feedline used for matching is governed by:

$$
Z_0 = \frac{60}{\sqrt{\epsilon_{eff}}} \ln \left( \frac{8h}{w} + \frac{w}{4h} \right)
$$

The Return Loss ($S_{11}$), which represents the total reflected power from the antenna’s input terminal, is calculated as:

$$
S_{11} = 20 \log_{10}|\Gamma| \quad \text{where} \quad \Gamma = \frac{Z_L - Z_0}{Z_L + Z_0}
$$

## Performance Metrics & Simulation Results
The antenna was modeled and simulated using **CST Microwave Studio** (Time Domain Solver).

### 1. Return Loss ($S_{11}$) & Impedance Matching
Maintained primarily below $-10$ dB across the operational band ($3$ GHz – $11$ GHz), with deep optimal resonances at $6–7$ GHz. The fabricated prototype closely matches this simulated response.
![S11 Return Loss Graph](s11-graph.png)

### 2. Gain & Directivity
The dual-slot radiating structure acts as a 2-element array, achieving a high directional gain of approximately **$10–12$ dBi** in the upper frequency bands.
![Antenna Gain Plot](gain-plot.png)

## Biomedical Safety & SAR Analysis
A critical component of this project is ensuring the antenna operates safely near human tissue. Tests were conducted using a multi-layer Human Head Phantom model (Skin, Fat, Skull, Dura, CSF, Gray/White Matter) in CST.

### Specific Absorption Rate (SAR)
The antenna's peak SAR value is **$0.0373$ W/kg** (at $7.536$ GHz), which is drastically below the international IEEE/ICNIRP safety limit of $1.6$ W/kg for 1g of tissue. 
![SAR Heatmap Analysis](sar-heatmap.png)

* **Placement Distance Optimization:** Performance was analyzed at distances of $3$ mm, $5$ mm, $7$ mm, and $10$ mm from the tissue. A placement distance of **$7$ mm** was found to yield the highest antenna gain with minimal electromagnetic energy absorbed by the phantom.
* **Tumor Power Loss Detection:** Power loss analysis demonstrated measurable differentiation when encountering biological tissue, scaling predictably as tumor radius increases (from $6$ mm to $10$ mm).The power loss versus radius analysis provides important insight into how electromagnetic energy is absorbed by biological tissues as the size of the tumor region increases. It is observed that as the radius increases from 6 mm to 10 mm, the power loss steadily increases.Low power loss levels are seen at small radii due the radio frequency interaction between the antenna and tissue being limited. When the antenna radius is bigger than the average radius.
  ![Powerloss vs radius](power_loss.png)
### Dielectric Properties: Healthy Tissue vs. Cancerous Tumor
The core principle behind using a UWB Vivaldi antenna for biomedical imaging is **dielectric contrast**. Biological tissues interact differently with electromagnetic waves based on their physiological composition, particularly their water and sodium content. 

Cancerous tumors typically undergo angiogenesis (the formation of new blood vessels) to support rapid growth. This results in a significantly higher water and blood content compared to surrounding healthy tissues, drastically altering their electrical properties.

| Property | Healthy Tissue (Baseline) | Cancerous Tumor (Malignant) | Impact on Microwave Signals |
| :--- | :--- | :--- | :--- |
| **Water Content** | Low to Moderate | High | Increased fluid absorbs more electromagnetic energy. |
| **Relative Permittivity ($\epsilon_r$)** | Lower (e.g., Fat $\approx 5$) | Significantly Higher ($\approx 50+$) | Causes severe signal scattering, phase shifts, and stronger reflections at the tissue boundary. |
| **Conductivity ($\sigma$)** | Lower | Higher | Increases the localized Specific Absorption Rate (SAR) and signal attenuation. |
| **Electromagnetic Power Loss** | Minimal | High | Creates a measurable energy drop that the antenna system detects as an anomaly. |
### Power Loss Analysis: Healthy Tissue vs. Cancerous Tumor
Power loss analysis assesses the extent to which electromagnetic energy emitted from the antenna is absorbed into biological tissues. Both healthy and malignant tumors were simulated to determine how much power is absorbed into each type of tissue at multiple operational frequencies.

The table below demonstrates the exact simulated power loss for the double-slot antenna, showing that cancerous tumors absorb consistently more power than healthy tissue:

| Frequency (GHz) | Power Loss in Healthy Tissue (W) | Power Loss in Cancerous Tumor (W) |
| :--- | :--- | :--- |
| **4.132** | 0.00029306 | 0.00043855 |
| **6.023** | 0.00049643 | 0.00054210 |
| **6.720** | 0.00045839 | 0.00058728 |
| **7.536** | 0.00051620 | 0.00055330 |
| **8.840** | 0.00037287 | 0.00038287 |

#### Mechanism of Detection
When the double-slot Vivaldi antenna directs an ultra-wideband pulse into the human head phantom, the electromagnetic waves propagate through healthy, low-permittivity tissues (such as fat and bone) with minimal disruption. 

However, when the traveling waves encounter a cancerous tumor, the sudden spike in permittivity and conductivity acts as an electromagnetic obstacle. The tumor absorbs a larger portion of the energy (measured as **Power Loss**) and scatters the remaining signal. By monitoring these power losses and return signal reflections ($S_{11}$), the system can successfully identify the presence, size, and approximate location of the malignancy without requiring invasive medical procedures.

## Repository Structure
* `/Simulation_Files` - Contains the base `CST Microwave Studio` (.cst) project files and human phantom model configurations.
* `/Results_and_Graphs` - Exported data for Return Loss ($S_{11}$), Gain, SAR heatmaps, and Power Loss vs. Radius graphs.
* `/Documentation` - Detailed design methodology, exponential flare equations, and project reports.
* `/Fabrication` - Images and VNA measurement data of the physical antenna prototype.

## Technologies Used
* **Simulation:** CST Studio Suite (3D Electromagnetic Solver)
* **Fabrication:** Printed Circuit Board (PCB) etching on Rogers RO4003C
* **Testing:** Vector Network Analyzer (VNA)

## Acknowledgements
Developed at the Department of Electronics and Communication Engineering, SRM Institute of Science and Technology (SRMIST), Kattankulathur. This project directly contributes to the UN's Sustainable Development Goals (SDG 3: Good Health and Well-Being & SDG 9: Industry, Innovation, and Infrastructure).

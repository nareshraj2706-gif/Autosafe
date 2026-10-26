# AutoSafe – AI/ML-Powered Smart Safety System for MTC Buses

> **Team:** TechSafers · **Team ID:** HSC|TN|00561 · **State/UT:** Tamil Nadu (Chennai)
> **Theme:** Road Safety & Smart Public Transportation

AutoSafe is a proposed low-cost, edge-based safety unit for Metropolitan Transport Corporation (MTC) buses in Chennai. It continuously monitors the bus surroundings and the driver, detects hazards, warns the driver in real time, and shares hazard information with nearby buses.

---

## ⚠️ Project Status – Please Read First

This README is derived **only** from the project presentation (`AutoSafe_HSC_Presentation.pptx`). The presentation describes a **concept and a planned low-cost prototype**. It does not state that any hardware has been assembled or any code written.

| Label | Meaning |
|---|---|
| **[Proposed]** | Described in the presentation as part of the design or planned prototype |
| **[Implemented]** | Confirmed built and working. **None** of the features are confirmed as implemented in the source material |
| **[TBC]** | To Be Confirmed. Not specified in the presentation |

> Wherever this document says **To Be Confirmed**, the team must fill in the detail before the repository is published. Sections such as installation and execution are **templates** until the actual code exists.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Features](#2-features)
3. [Prerequisites](#3-prerequisites)
4. [Installation](#4-installation)
5. [Setup](#5-setup)
6. [Environment Variables](#6-environment-variables)
7. [Execution Instructions](#7-execution-instructions)
8. [Troubleshooting](#8-troubleshooting)
9. [Repository Contents](#9-repository-contents)
10. [Team and Acknowledgements](#10-team-and-acknowledgements)
11. [References](#11-references)

---

## 1. Project Overview

### Problem
MTC buses run in crowded urban traffic where the following raise accident risk:
- Sudden braking, blind spots, pedestrians, two-wheelers and animals
- Driver fatigue
- Limited awareness beyond the driver's field of view with conventional bus safety
- No communication of approaching dangers between vehicles

### Proposed Solution
AutoSafe is an AI/ML-powered system that:
- Continuously monitors the bus surroundings
- Detects vehicles, pedestrians, animals and obstacles
- Uses 360° cameras and sensors to cover blind spots
- Monitors the driver for drowsiness and distraction
- Uses distance/motion sensors for collision warning
- Issues real-time audio and visual alerts
- Applies all-weather sensor fusion

### Innovation (as stated in the presentation)
- Bus-to-bus (V2V) sharing of hazards using LoRa / ESP8266
- One low-cost unit combining outside hazard detection, blind-spot sensing and driver monitoring
- Anomaly detection for abnormal driving conditions
- Affordable, adaptable hardware for MTC fleets

### Processing Pipeline (Proposed)

```
1 Sense → 2 Detect → 3 Analyze → 4 Communicate → 5 Alert → 6 Prevent
```

| Stage | Description |
|---|---|
| Sense | Sensors monitor the area around the bus |
| Detect | Vehicles, pedestrians, animals, obstacles |
| Analyze | Collision risk and abnormal conditions |
| Communicate | V2V alerts to nearby buses |
| Alert | Real-time audio/visual warnings |
| Prevent | Driver takes timely action |

---

## 2. Features

| # | Feature | Status |
|---|---|---|
| F1 | AI hazard detection: vehicles, pedestrians, animals, obstacles (YOLO / TensorFlow Lite) | [Proposed] |
| F2 | 360° camera coverage (front / side / rear / driver) | [Proposed] |
| F3 | Blind-spot sensing (radar; ultrasonic and IR sensors) | [Proposed] |
| F4 | Driver monitoring: drowsiness and distraction warnings | [Proposed] |
| F5 | Collision warning using distance/motion sensors (HC-SR04, MPU6050 IMU) | [Proposed] |
| F6 | Real-time audio and visual alerts (buzzer, LED/OLED display, speaker voice alert) | [Proposed] |
| F7 | All-weather sensor fusion (cameras combined with ultrasonic/IR/radar) | [Proposed] |
| F8 | Anomaly detection for abnormal driving conditions / risk prediction | [Proposed] |
| F9 | Bus-to-bus (V2V) hazard sharing via LoRa SX1278 / ESP8266 | [Proposed] |
| F10 | Location and connectivity (GPS, GSM) | [Proposed] |
| F11 | Data logging of risk data for incident analysis and accident-prone route analysis | [Proposed] |
| F12 | Lane and behaviour detection using pre-trained models | [Proposed] |
| F13 | Edge (on-bus) processing for real-time response | [Proposed] |
| F14 | Power from bus supply via 12/24V → 5V converter, optional backup battery | [Proposed] |

> **Implementation status of every feature above: To Be Confirmed.**

---

## 3. Prerequisites

### 3.1 Hardware (Proposed, from the presentation)

| Category | Components named in the presentation | Quantity / exact model |
|---|---|---|
| Main processor | Raspberry Pi 5 | TBC |
| Controllers | ESP32 / ESP32-CAM | TBC |
| Cameras | Front, side, rear and driver cameras | TBC |
| Distance sensors | HC-SR04 ultrasonic, IR sensors | TBC |
| Blind-spot sensor | Radar | Model TBC |
| Motion sensor | MPU6050 IMU | TBC |
| V2V communication | LoRa SX1278 / ESP8266 | Final choice TBC |
| Connectivity / location | GSM module, GPS module | Models TBC |
| Output devices | Buzzer, LED/OLED display, speaker | Models TBC |
| Power | 12/24V → 5V converter, optional backup battery | Ratings TBC |
| Protection and mechanical | Cooling fan/heatsink, enclosures, mounting brackets, fuse and protection | Specifications TBC |

### 3.2 Software (from the presentation)

| Item | Detail |
|---|---|
| Operating system | Raspberry Pi OS (version TBC) |
| Language | Python (version TBC) |
| Editor | VS Code |
| AI/ML | YOLO / TensorFlow Lite (specific model, version and training data TBC) |
| Microcontroller firmware toolchain (ESP32 / ESP8266) | To Be Confirmed |
| Python dependencies | To Be Confirmed (`requirements.txt` not yet defined) |

---

## 4. Installation

> **Template.** The presentation does not specify repository structure, dependency list, or install steps. Replace every TBC item once the code exists.

```bash
# 1. Clone the repository
git clone <REPOSITORY_URL>      # URL: TBC
cd <REPOSITORY_FOLDER>          # Folder name: TBC

# 2. Create and activate a Python virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install Python dependencies
pip install -r requirements.txt   # requirements.txt: TBC (not yet created)
```

**AI/ML model files:** The presentation says pre-trained models are used. Model names, sources, file formats and where to place them are **To Be Confirmed**.

**Microcontroller firmware (ESP32 / ESP32-CAM / ESP8266):** Build tool, flashing steps and firmware source location are **To Be Confirmed**.

---

## 5. Setup

### 5.1 Hardware Setup (Proposed)

1. Mount cameras (front, side, rear, driver) and sensors (ultrasonic, IR, radar, IMU). Positions: **TBC**.
2. Connect the sensors, cameras, GPS, GSM, LoRa/ESP8266 and output devices to the Raspberry Pi 5 and ESP32 / ESP32-CAM controllers. **Pin mapping and wiring diagram: TBC.**
3. Supply power through the 12/24V → 5V converter with fuse and protection; connect the optional backup battery.
4. Fit the cooling fan/heatsink and enclosure for heat and vibration protection.

### 5.2 Software Setup

1. Flash Raspberry Pi OS to the Raspberry Pi 5.
2. Install Python and project dependencies (see [Installation](#4-installation)).
3. Load the pre-trained detection model(s). **TBC**
4. Set configuration and thresholds. **Threshold values: TBC.** The presentation says thresholds are to be tuned through route testing.

---

## 6. Environment Variables

**To Be Confirmed.** The presentation does not define any environment variables or configuration files.

The table below is a **placeholder template** for the team to complete. The rows are suggestions based on the components named in the presentation and are **not** taken from the presentation.

| Variable | Purpose | Example / Default |
|---|---|---|
| `<MODEL_PATH>` | Location of the detection model | TBC |
| `<CAMERA_SOURCES>` | Camera device identifiers | TBC |
| `<LORA_CONFIG>` | LoRa / ESP8266 V2V settings | TBC |
| `<GPS_PORT>` | GPS module connection | TBC |
| `<GSM_PORT>` | GSM module connection | TBC |
| `<ALERT_THRESHOLDS>` | Collision, drowsiness and distraction thresholds | TBC |
| `<LOG_PATH>` | Where risk data is logged | TBC |

---

## 7. Execution Instructions

> **Template.** No entry point, script names or run commands are given in the presentation.

```bash
source venv/bin/activate
python <MAIN_SCRIPT>.py     # Entry point: TBC
```

**Expected runtime behaviour (Proposed, per the presentation):**
1. Sensors and cameras continuously monitor the bus surroundings and driver.
2. Detected hazards are analysed for collision risk and abnormal conditions.
3. The driver receives real-time audio/visual alerts.
4. Hazard alerts are sent to nearby buses over V2V.
5. Risk data is logged. Log format and storage: **TBC**.

**Running tests:** see [`TEST_CASES.md`](TEST_CASES.md). Automated test tooling: **TBC**.

---

## 8. Troubleshooting

The presentation does not include troubleshooting steps. The entries below are based on the **risks and mitigations stated in the presentation (Slide 5)**; detailed fixes are **To Be Confirmed** after prototype testing.

| Symptom / Risk | Possible cause (per presentation) | Suggested direction (per presentation) |
|---|---|---|
| Poor camera detection in rain, glare or low light | Camera accuracy limits | Rely on fusion with ultrasonic/IR/radar sensors; detailed steps TBC |
| Device overheating or unstable | Heat and vibration in the bus environment | Cooling fan/heatsink, enclosure, mounting brackets, fuse and protection; detailed steps TBC |
| Too many or irrelevant alerts | False alerts causing driver alert fatigue | Tune thresholds and test on real routes; threshold values TBC |
| V2V messages not received | Range or signal issues in dense traffic | Use LoRa for longer-range V2V; diagnostics TBC |
| Unit loses power | Bus supply interruption | Optional backup battery; behaviour on power loss TBC |
| Any other issue | n/a | To Be Confirmed |

---

## 9. Repository Contents

| File | Description |
|---|---|
| `README.md` | This file |
| `Technical_Design_Document.md` | Problem statement, architecture, modules, data flow, stack, limitations |
| `TEST_CASES.md` | Planned test cases with placeholders for actual results |
| `SAMPLE_DATA.md` | Illustrative sample inputs and expected outputs |
| `sample_sensor_readings.csv` | Illustrative sensor input samples |
| `sample_expected_outputs.json` | Illustrative expected outputs for the sample inputs |
| Source code, firmware, model files | **To Be Confirmed** (not yet provided) |

---

## 10. Team and Acknowledgements

| Name | Role |
|---|---|
| Dhanya A | Team Lead |
| Mangayarkarasi T | Mentor & Principal Investigator |
| Mahathi K | Team Member |
| Naresh R | Team Member |

Developed under **Sairam Institutions** with **EPICS in IEEE** and **IEEE SIGHT**.

**Stakeholders named in the presentation:** MTC; Chennai Traffic Police; technology partners (sensors, IoT, GPS, V2V); educational institutions and research labs; Government and Smart City authorities; automotive/IoT companies.

**SDGs addressed:** SDG 3 · SDG 11 · SDG 17

---

## 11. References

As listed in the presentation:

1. Bilstrup, K., Uhlemann, E., Ström, E. G., & Bilstrup, U. (2009). *Evaluation of the IEEE 802.11p MAC method for vehicle-to-vehicle communication.*
2. Wijesiri, N. A., et al. (2019). *Performance comparison of C-V2X Mode 4 and IEEE 802.11p for vehicular communication.*
3. Tandon, A., et al. (2020). *Electric Vehicles in India: Opportunities and Challenges.*
4. Nagar, S., et al. (2024). *Integration of Vehicle-to-Grid (V2G) Technology and Advanced Driver Assistance Systems (ADAS).*
5. IEEE. *IEEE 802.11p: Wireless Access in Vehicular Environments (WAVE).* https://standards.ieee.org/
6. 3GPP. *Cellular Vehicle-to-Everything (C-V2X) Standards.* https://www.3gpp.org/
7. WHO. *Global Status Report on Road Safety 2023.* https://www.who.int/publications/i/item/9789240086517

---

## License

To Be Confirmed.

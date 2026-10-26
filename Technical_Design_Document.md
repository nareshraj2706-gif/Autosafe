# Technical Design Document – AutoSafe

**Project:** AutoSafe – AI/ML-powered smart safety system for MTC buses
**Team:** TechSafers (ID: HSC|TN|00561) · **State/UT:** Tamil Nadu (Chennai)
**Theme:** Road Safety & Smart Public Transportation
**Source:** `AutoSafe_HSC_Presentation.pptx` (7 slides)
**Document version:** 0.1 (draft) · **Date:** 26 October 2026

---

## Status Legend

| Label | Meaning |
|---|---|
| **[Proposed]** | Described in the presentation as design or planned prototype |
| **[Implemented]** | Confirmed built and working. **None** is confirmed in the source material |
| **[TBC]** | To Be Confirmed. Not specified in the presentation |

> The presentation describes a concept and a *planned* low-cost prototype. This document therefore describes the **intended design**. Where it needs detail the presentation does not give, the entry is marked **To Be Confirmed** rather than assumed.

---

## 1. Problem Statement

MTC buses operate in crowded urban traffic in Chennai. The presentation identifies these risks:

1. Sudden braking, blind spots, pedestrians, two-wheelers and animals
2. Driver fatigue, which adds to accident risk
3. Conventional bus safety gives limited awareness beyond the driver's field of view
4. Approaching dangers are not communicated between vehicles

**Objective:** Provide a low-cost, edge-based system that monitors the bus surroundings and driver, detects hazards, alerts the driver in real time, and shares hazards with nearby buses so that the driver can act before a collision.

**Quantified targets (e.g., detection accuracy, latency, range):** To Be Confirmed. None are stated in the presentation.

---

## 2. System Architecture

### 2.1 Architectural Approach [Proposed]

A six-stage pipeline processed on the bus (edge processing):

```
┌───────┐   ┌────────┐   ┌─────────┐   ┌─────────────┐   ┌───────┐   ┌─────────┐
│ Sense │ → │ Detect │ → │ Analyze │ → │ Communicate │ → │ Alert │ → │ Prevent │
└───────┘   └────────┘   └─────────┘   └─────────────┘   └───────┘   └─────────┘
```

| Stage | Function |
|---|---|
| 1. Sense | Sensors monitor the area around the bus |
| 2. Detect | Vehicles, pedestrians, animals, obstacles |
| 3. Analyze | Collision risk and abnormal conditions |
| 4. Communicate | V2V alerts to nearby buses |
| 5. Alert | Real-time audio/visual warnings |
| 6. Prevent | Driver takes timely action |

The presentation lists "Alert" after "Communicate", but does not state whether the local alert and the V2V transmission run in parallel or in sequence. **TBC**

### 2.2 Logical Component View [Proposed]

```
        ┌────────────────────────── ON-BUS UNIT ──────────────────────────┐
        │                                                                   │
 INPUTS │  Cameras (front/side/rear/driver)    ┐                           │
        │  HC-SR04 ultrasonic, IR, radar        ├─►  Raspberry Pi 5  ──┐   │
        │  MPU6050 IMU                          ┘   (main processor)   │   │
        │  GPS                                       ▲                 │   │
        │                                            │                 │   │
        │                         ESP32 / ESP32-CAM controllers        │   │
        │                           (role split: TBC)                  │   │
        │                                                              ▼   │
 OUTPUT │   Buzzer · LED/OLED display · Speaker voice alert   ◄── Alert logic│
        │                                                              │   │
 COMMS  │   LoRa SX1278 / ESP8266 (V2V)  ◄────────────────────────────┤   │
        │   GSM                          ◄─────────────────────────────┘   │
        │                                                                   │
 POWER  │   Bus 12/24V → 5V converter (+ optional backup battery)           │
        └───────────────────────────────────────────────────────────────────┘
                              │ V2V (LoRa)
                              ▼
                      Nearby AutoSafe-equipped buses
```

> **Note:** The diagram above is a logical view assembled from the components listed in the presentation. Exact interconnections (which sensor connects to the Raspberry Pi versus the ESP32), and the interfaces and protocols used, are **To Be Confirmed**.

### 2.3 Deployment Model [Proposed]
- Edge processing on the bus for real-time response
- Modular design that can be fitted to MTC buses
- Powered from the bus supply via a 12/24V → 5V converter, optional backup battery
- Protection: cooling fan/heatsink, enclosures, mounting brackets, fuse and protection

---

## 3. Modules

All modules below are **[Proposed]**. Implementation status: **TBC**.

| ID | Module | Responsibility (per presentation) | Inputs | Outputs | Detail |
|---|---|---|---|---|---|
| M1 | Sensing / Data Acquisition | Monitor the area around the bus | Cameras, HC-SR04, IR, radar, MPU6050, GPS | Raw sensor and camera data | Sampling rates TBC |
| M2 | Object Detection | Detect vehicles, pedestrians, animals, obstacles | Camera frames | Detected objects and classes | YOLO / TensorFlow Lite; exact model TBC |
| M3 | Lane and Behaviour Detection | Lane and behaviour detection using pre-trained models | Camera frames | Lane/behaviour information | Model TBC |
| M4 | Blind-Spot Sensing | Cover blind spots with 360° cameras and sensors | Cameras, radar, ultrasonic/IR | Blind-spot hazard status | Fusion method TBC |
| M5 | Driver Monitoring | Detect drowsiness and distraction | Driver camera | Drowsiness / distraction status | Detection method and thresholds TBC |
| M6 | Collision-Risk and Anomaly Analysis | Analyse collision risk and abnormal driving conditions | Detections, distance/motion data | Risk level, anomaly flags | Anomaly detection algorithm TBC |
| M7 | Sensor Fusion | All-weather operation by combining cameras with ultrasonic/IR/radar | Camera and non-camera sensor data | Fused hazard assessment | Fusion algorithm TBC |
| M8 | V2V Communication | Share hazards between buses | Hazard events | V2V messages to nearby buses; received messages | LoRa SX1278 / ESP8266; message format TBC |
| M9 | Alerting | Real-time audio and visual warnings | Risk level, V2V alerts, driver status | Buzzer, LED/OLED, speaker voice alert | Alert levels and wording TBC |
| M10 | Location and Connectivity | Provide position and wide-area link | GPS, GSM | Location data; GSM link | GSM usage (e.g., reporting) TBC |
| M11 | Data Logging | Record risk data for incident analysis and route/pattern analysis | Risk events, location | Stored log records | Format, storage, retention TBC |
| M12 | Power and Protection | Supply and protect the unit | Bus 12/24V | 5V supply, optional backup | Ratings TBC |

---

## 4. Data Flow

### 4.1 Primary Flow [Proposed]

```
Sensors + Cameras ──► Acquisition (M1)
                          │
        ┌─────────────────┼──────────────────┐
        ▼                 ▼                  ▼
 Object/Lane/Behaviour  Distance/Motion   Driver camera
 Detection (M2, M3)     data (M4, M7)     Monitoring (M5)
        │                 │                  │
        └───────► Fusion + Risk/Anomaly Analysis (M6, M7) ◄──┘
                              │
              ┌───────────────┼────────────────┐
              ▼               ▼                ▼
        Alerting (M9)   V2V send (M8)    Data Logging (M11)
              │               │
              ▼               ▼
      Driver acts      Nearby buses ──► their Alerting (M9)
```

### 4.2 Data Flow Steps

| Step | From → To | Data | Detail |
|---|---|---|---|
| 1 | Sensors/cameras → M1 | Frames, distance, motion, location | Formats and rates TBC |
| 2 | M1 → M2/M3 | Camera frames | Preprocessing TBC |
| 3 | M1 → M4 | Distance/radar/IR data | Processing TBC |
| 4 | M1 → M5 | Driver-camera frames | Processing TBC |
| 5 | M2–M5 → M6/M7 | Detections and status | Data structures TBC |
| 6 | M6 → M9 | Risk level / anomaly | Alert levels TBC |
| 7 | M6 → M8 | Hazard event | V2V message structure TBC |
| 8 | M8 (remote) → M9 | Received hazard alert | Handling of received alerts TBC |
| 9 | M6 → M11 | Risk event with location | Log schema TBC |

### 4.3 Data Stored
The presentation states that risk data is recorded for incident analysis and to reveal accident-prone routes and driving patterns. Retention, privacy handling (including driver-camera footage), and access control are **To Be Confirmed**.

---

## 5. Technology Stack

| Layer | Technology (from the presentation) | Status |
|---|---|---|
| Main processing | Raspberry Pi 5 | [Proposed] |
| Controllers | ESP32 / ESP32-CAM | [Proposed] |
| AI/ML: object detection and classification | YOLO / TensorFlow Lite | [Proposed] |
| AI/ML: risk prediction | Anomaly detection (algorithm TBC) | [Proposed] |
| AI/ML models | Pre-trained models (names and sources TBC) | [Proposed] |
| Cameras | Front, side, rear, driver | [Proposed] |
| Distance / blind-spot sensors | HC-SR04 ultrasonic, IR, radar | [Proposed] |
| Motion sensor | MPU6050 IMU | [Proposed] |
| V2V communication | LoRa SX1278 / ESP8266 | [Proposed] |
| Connectivity and location | GSM, GPS | [Proposed] |
| Output | Buzzer, LED/OLED display, speaker | [Proposed] |
| Operating system | Raspberry Pi OS | [Proposed] |
| Language / tools | Python, VS Code | [Proposed] |
| Power | 12/24V → 5V converter, optional backup battery | [Proposed] |
| Firmware language for ESP32 / ESP8266 | To Be Confirmed | n/a |
| Libraries and frameworks (e.g., computer vision, serial/LoRa drivers) | To Be Confirmed | n/a |

---

## 6. Implementation Details

### 6.1 What the presentation states
- AI/ML models are **pre-trained** and handle object, lane and behaviour detection.
- Processing is done at the edge, on the bus, for real-time response.
- Cameras are combined with ultrasonic/IR/radar sensors for all-weather use.
- Thresholds are to be tuned and tested on real routes.
- LoRa is chosen for longer-range V2V.
- Hardware protection: cooling fan/heatsink, enclosures, mounting brackets, fuse and protection.
- A low-cost prototype with a full component budget has been **planned**.

### 6.2 Implementation status

| Area | Status |
|---|---|
| Architecture and design | Designed (per presentation "Our Journey") |
| Prototype hardware | Planned. Build status **TBC** |
| Software / firmware | **TBC** |
| Model selection, training or fine-tuning | **TBC** |
| Field testing with MTC | Proposed (requires approvals and access) |

### 6.3 Items to be defined before implementation is documented

| Item | Status |
|---|---|
| Specific detection model, version and input resolution | TBC |
| Classes detected and training/fine-tuning data | TBC |
| Drowsiness and distraction detection method | TBC |
| Collision-risk logic (e.g., distance and speed thresholds) | TBC |
| Anomaly detection algorithm and the "abnormal conditions" it covers | TBC |
| Sensor fusion method | TBC |
| Sensor/camera placement and field-of-view coverage | TBC |
| Division of work between Raspberry Pi 5 and ESP32 / ESP32-CAM | TBC |
| V2V message format, range, and choice between LoRa and ESP8266 | TBC |
| Alert levels, priority, and voice messages | TBC |
| Log format, storage, retention | TBC |
| Software structure, entry points, configuration | TBC |
| Performance targets (latency, accuracy, false-alert rate) | TBC |
| Component budget figures | TBC (a budget is mentioned, but figures are not in the deck) |

---

## 7. Limitations and Risks

### 7.1 Stated in the presentation

| Limitation / Risk | Planned mitigation (per presentation) |
|---|---|
| Camera accuracy in rain, glare and low light | Combine cameras with ultrasonic/IR/radar sensors |
| Heat and vibration on in-bus electronics | Cooling fan/heatsink, enclosures, mounting brackets, fuse and protection |
| False alerts causing driver alert fatigue | Tune thresholds and test on real routes |
| Reliable V2V range and signal in dense traffic | LoRa for longer-range V2V |
| Approvals and field-testing access with MTC | Partner with MTC and Chennai Traffic Police for pilots |
| Integrating many sensors and cameras into one reliable unit | Modular design (details TBC) |
| Running real-time AI detection on low-cost hardware | Edge processing with pre-trained models (feasibility TBC) |
| Keeping alerts accurate in Chennai traffic, weather and lighting | Threshold tuning on real routes |
| Staying within a low student-project budget | Low-cost, widely available components |

### 7.2 Current scope limitations
- **No validated performance results:** no accuracy, latency, range or false-alert figures are provided. **TBC**
- **Prototype status unconfirmed:** the design is currently documented as proposed.
- **Pre-trained models:** performance on Chennai-specific conditions (e.g., two-wheelers, animals) is **TBC**.
- **V2V** depends on other buses being equipped. Behaviour with a single equipped bus is **TBC**.
- **Safety and regulatory certification** for use on public buses: **TBC**.
- **Privacy** handling for driver and external camera data: **TBC**.

---

## 8. Impact and Stakeholders (Context)

**Intended impact:** fewer road accidents; better driver awareness of blind-spot hazards; safer passengers, pedestrians, cyclists, two-wheeler riders and motorists; fewer blind-spot accidents during turning, lane changes and reversing. These are **intended outcomes, not measured results**.

**Benefits:** saving lives and reducing injuries; faster emergency response and incident analysis; low-cost scalable fit for MTC buses; route and driving pattern insight. **SDGs:** 3, 11, 17.

**Stakeholders:** MTC; Chennai Traffic Police; technology partners; educational institutions and research labs; Government and Smart City authorities; automotive/IoT companies.

---

## 9. References

1. Bilstrup, K., Uhlemann, E., Ström, E. G., & Bilstrup, U. (2009). *Evaluation of the IEEE 802.11p MAC method for vehicle-to-vehicle communication.*
2. Wijesiri, N. A., et al. (2019). *Performance comparison of C-V2X Mode 4 and IEEE 802.11p for vehicular communication.*
3. Tandon, A., et al. (2020). *Electric Vehicles in India: Opportunities and Challenges.*
4. Nagar, S., et al. (2024). *Integration of Vehicle-to-Grid (V2G) Technology and Advanced Driver Assistance Systems (ADAS).*
5. IEEE. *IEEE 802.11p: Wireless Access in Vehicular Environments (WAVE).* https://standards.ieee.org/
6. 3GPP. *Cellular Vehicle-to-Everything (C-V2X) Standards.* https://www.3gpp.org/
7. WHO. *Global Status Report on Road Safety 2023.* https://www.who.int/publications/i/item/9789240086517

---

## 10. Team

Dhanya A (Team Lead) · Mangayarkarasi T (Mentor & Principal Investigator) · Mahathi K (Team Member) · Naresh R (Team Member)
Developed under Sairam Institutions with EPICS in IEEE and IEEE SIGHT.

# Test Cases – AutoSafe

**Project:** AutoSafe – AI/ML-powered smart safety system for MTC buses
**Team:** TechSafers (ID: HSC|TN|00561)
**Document version:** 0.1 (draft) · **Date:** 26 October 2026

## How to Use This Document

- These are **planned** test cases derived from the **proposed** features in the project presentation. No test has been run and no results exist.
- **Actual Result** columns are empty placeholders to be filled during testing.
- **Status** values: `Not Run` (default) · `Pass` · `Fail` · `Blocked`.
- **Sample inputs** (S01–S16) refer to `sample_sensor_readings.csv` and `SAMPLE_DATA.md`. These are illustrative.
- **TBC** = To Be Confirmed. Thresholds, targets and message formats are not defined in the presentation, so expected results that depend on them are marked TBC and must be completed before execution.
- **Test environment** (hardware revision, software version, route, test dates, tester): **To Be Confirmed**.
- Implementation status of each feature is **TBC**. If a feature is not implemented, mark its test `Blocked`.

---

## 1. Hazard Detection (AI/ML)

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-DET-001 | Object detection (M2) | Pedestrian in front zone | Sample S05 (pedestrian, confidence 0.91) | Pedestrian detected; driver alerted (audio + visual); event logged | _[to be filled]_ | Not Run |
| TC-DET-002 | Object detection (M2) | Vehicle ahead | Sample S07 (vehicle, confidence 0.95) | Vehicle detected; alert depends on distance/closing speed (thresholds TBC) | _[to be filled]_ | Not Run |
| TC-DET-003 | Object detection (M2) | Animal on road | Sample S06 (animal, confidence 0.84) | Animal detected; driver alerted (audio + visual); event logged | _[to be filled]_ | Not Run |
| TC-DET-004 | Object detection (M2) | Obstacle on road | Sample S08 (obstacle, confidence 0.88) | Obstacle detected; driver alerted (audio + visual); event logged | _[to be filled]_ | Not Run |
| TC-DET-005 | Object detection (M2) | No hazards in view | Sample S14 (no detections) | No alert raised | _[to be filled]_ | Not Run |
| TC-DET-006 | Lane / behaviour detection (M3) | Lane and behaviour detection using pre-trained model | Camera frames (specific input TBC) | Lane/behaviour information produced; output format and pass criteria TBC | _[to be filled]_ | Not Run |
| TC-DET-007 | Object detection (M2) | Two-wheeler in view | Camera frames with two-wheeler (specific input TBC) | Two-wheeler detected; accuracy criteria TBC | _[to be filled]_ | Not Run |

## 2. Collision Warning and Anomaly Detection

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-COL-001 | Collision warning (HC-SR04) | Object very close ahead | Sample S01 (40 cm) | Collision warning; buzzer, display and voice alert; event logged | _[to be filled]_ | Not Run |
| TC-COL-002 | Collision warning (HC-SR04) | Clear road ahead | Sample S02 (350 cm) | No alert | _[to be filled]_ | Not Run |
| TC-COL-003 | Collision warning (IR sensor) | Close object detected by IR | IR sensor reading (value TBC) | Warning raised; threshold TBC | _[to be filled]_ | Not Run |
| TC-COL-004 | Anomaly detection (MPU6050) | Sudden hard braking | Sample S03 (−8.5 m/s²) | Abnormal driving condition flagged and logged; alert behaviour TBC | _[to be filled]_ | Not Run |
| TC-COL-005 | Anomaly detection (MPU6050) | Normal driving | Sample S04 (−0.4 m/s²) | No anomaly flagged; no alert | _[to be filled]_ | Not Run |

## 3. Blind-Spot Sensing

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-BLD-001 | Blind-spot sensing (M4) | Two-wheeler in left blind spot, camera and radar agree | Samples S09 + S10 | Blind-spot hazard (left) alert; event logged | _[to be filled]_ | Not Run |
| TC-BLD-002 | Blind-spot sensing (M4) | Object in blind spot detected by radar only | Radar object present = 1; no camera detection | Alert behaviour TBC (fusion rules not defined) | _[to be filled]_ | Not Run |
| TC-BLD-003 | Blind-spot sensing (M4) | Empty blind spot | No camera detection; radar object present = 0 | No blind-spot alert | _[to be filled]_ | Not Run |
| TC-BLD-004 | 360° coverage | Hazard from each side of the bus (front, left, right, rear) | Hazard placed at each side | Detected from each side; coverage and range TBC | _[to be filled]_ | Not Run |

## 4. Driver Monitoring

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-DRV-001 | Driver monitoring (M5) | Drowsiness | Sample S11 (eyes closed 3.0 s) | Drowsiness warning (audio + visual); event logged | _[to be filled]_ | Not Run |
| TC-DRV-002 | Driver monitoring (M5) | Distraction | Sample S12 (head turned away 4.0 s) | Distraction warning (audio + visual); event logged | _[to be filled]_ | Not Run |
| TC-DRV-003 | Driver monitoring (M5) | Attentive driver, normal blink | Sample S13 (eyes closed 0.2 s) | No warning | _[to be filled]_ | Not Run |
| TC-DRV-004 | Driver monitoring (M5) | Driver camera obstructed or not visible | Driver camera covered | System behaviour TBC (not defined) | _[to be filled]_ | Not Run |

## 5. Sensor Fusion and Environmental Conditions

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-ENV-001 | All-weather fusion (M7) | Low-light conditions | Night or low-light route; hazard present | Hazard still detected with fusion of non-camera sensors; accuracy criteria TBC | _[to be filled]_ | Not Run |
| TC-ENV-002 | All-weather fusion (M7) | Rain | Rain; hazard present | Hazard detected; accuracy criteria TBC | _[to be filled]_ | Not Run |
| TC-ENV-003 | All-weather fusion (M7) | Glare | Strong glare on camera; hazard present | Hazard detected via non-camera sensors; accuracy criteria TBC | _[to be filled]_ | Not Run |
| TC-ENV-004 | False alerts | Alert fatigue check on a real route | Route drive without real hazards | False-alert rate within acceptable limit (limit TBC) | _[to be filled]_ | Not Run |

## 6. Alert Output

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-ALT-001 | Alerting (M9) | Buzzer output | Trigger any hazard (e.g., S01) | Buzzer sounds | _[to be filled]_ | Not Run |
| TC-ALT-002 | Alerting (M9) | LED/OLED display | Trigger any hazard (e.g., S05) | Visual warning shown on LED/OLED; content TBC | _[to be filled]_ | Not Run |
| TC-ALT-003 | Alerting (M9) | Speaker voice alert | Trigger any hazard (e.g., S05) | Voice alert played; wording TBC | _[to be filled]_ | Not Run |
| TC-ALT-004 | Alerting (M9) | Real-time response | Trigger hazard | Alerts issued in real time; latency target TBC | _[to be filled]_ | Not Run |
| TC-ALT-005 | Alerting (M9) | No hazard, no alert | Samples S02, S04, S13, S14 | No audio or visual alert | _[to be filled]_ | Not Run |

## 7. V2V Communication

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-V2V-001 | V2V send (M8) | Hazard shared to nearby bus | Sample S05 on Bus A; Bus B nearby | Bus B receives the hazard message | _[to be filled]_ | Not Run |
| TC-V2V-002 | V2V receive (M8/M9) | Received hazard alerts driver | Sample S16 | Received hazard alert shown to driver; buzzer/voice TBC | _[to be filled]_ | Not Run |
| TC-V2V-003 | V2V range (LoRa SX1278 / ESP8266) | Increasing distance between buses | Buses at increasing distances | Message received up to the supported range; range target TBC | _[to be filled]_ | Not Run |
| TC-V2V-004 | V2V reliability | Dense traffic | Multiple vehicles and buses in an urban route | Messages reliably received; reliability criteria TBC | _[to be filled]_ | Not Run |
| TC-V2V-005 | V2V send (M8) | No nearby equipped bus | Hazard raised; no other unit in range | Local alert works normally; no failure | _[to be filled]_ | Not Run |

## 8. Location, Connectivity and Logging

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-LOC-001 | GPS (M10) | Position available | Sample S15 | Position obtained and attached to logged events | _[to be filled]_ | Not Run |
| TC-LOC-002 | GSM (M10) | GSM connectivity | GSM module powered with network available | Connectivity established; usage and pass criteria TBC | _[to be filled]_ | Not Run |
| TC-LOG-001 | Data logging (M11) | Risk event logged | Any alert sample (e.g., S05) | Event recorded in the log; schema TBC | _[to be filled]_ | Not Run |
| TC-LOG-002 | Data logging (M11) | Log supports route analysis | Several logged events with positions | Accident-prone locations identifiable from logs; method TBC | _[to be filled]_ | Not Run |

## 9. Power and Hardware Robustness

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-PWR-001 | Power (M12) | 12 V bus supply | 12 V input | Converter outputs 5 V; unit operates normally | _[to be filled]_ | Not Run |
| TC-PWR-002 | Power (M12) | 24 V bus supply | 24 V input | Converter outputs 5 V; unit operates normally | _[to be filled]_ | Not Run |
| TC-PWR-003 | Power (M12) | Bus power lost (if backup battery fitted) | Disconnect bus supply | Unit continues on backup battery; duration TBC | _[to be filled]_ | Not Run |
| TC-HW-001 | Heat management | Extended operation in warm conditions | Continuous run | Unit remains stable with cooling fan/heatsink; temperature limit TBC | _[to be filled]_ | Not Run |
| TC-HW-002 | Vibration | Operation while the bus is moving | Route drive | Mounting and connections stay secure; unit keeps working | _[to be filled]_ | Not Run |

## 10. System-Level

| Test ID | Feature / Module | Scenario | Input Data | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| TC-SYS-001 | End-to-end pipeline | Sense → Detect → Analyze → Communicate → Alert | Hazard presented in front of the bus | Hazard detected, analysed, alert issued to driver, V2V sent, event logged | _[to be filled]_ | Not Run |
| TC-SYS-002 | Startup | Power-on | Power up the unit | All modules start; startup time and self-check TBC | _[to be filled]_ | Not Run |
| TC-SYS-003 | Fault handling | A sensor or camera disconnected | Disconnect one sensor | Behaviour TBC (not defined in the presentation) | _[to be filled]_ | Not Run |
| TC-SYS-004 | Real-time performance | Full system load on the Raspberry Pi 5 | All cameras and sensors active | Real-time detection sustained; frame rate target TBC | _[to be filled]_ | Not Run |

---

## Summary Table (to be completed after test runs)

| Group | Total | Pass | Fail | Blocked | Not Run |
|---|---|---|---|---|---|
| Hazard Detection | 7 | | | | 7 |
| Collision / Anomaly | 5 | | | | 5 |
| Blind-Spot | 4 | | | | 4 |
| Driver Monitoring | 4 | | | | 4 |
| Fusion / Environment | 4 | | | | 4 |
| Alert Output | 5 | | | | 5 |
| V2V | 5 | | | | 5 |
| Location / Logging | 4 | | | | 4 |
| Power / Hardware | 5 | | | | 5 |
| System-Level | 4 | | | | 4 |
| **Total** | **47** | | | | **47** |

**Tester:** _[TBC]_ · **Test date:** _[TBC]_ · **Software/hardware version:** _[TBC]_

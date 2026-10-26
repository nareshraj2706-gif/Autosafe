# Sample Data – AutoSafe

> **IMPORTANT – Illustrative only.** The AutoSafe presentation does not define data formats, thresholds, or message structures, and no real system output exists yet. The samples below are **illustrative inputs created for demonstration and test planning**. They are not recordings from a real system.
>
> - Input values are deliberately **clear-cut** (far from any plausible threshold) so expected outcomes hold whatever thresholds are chosen.
> - Field names and file formats are **proposed for documentation only**. Final data formats are **To Be Confirmed**.
> - Alert thresholds, V2V message format, alert wording and log schema are **To Be Confirmed**.
> - Where an expected output depends on an undefined detail, it is shown as **To Be Confirmed**.

## Files

| File | Purpose |
|---|---|
| `sample_sensor_readings.csv` | 16 illustrative input samples (S01–S16) covering sensors, detections, driver monitoring, GPS and V2V |
| `sample_expected_outputs.json` | Expected system behaviour for each sample |
| `SAMPLE_DATA.md` | This document: the same data in readable form |

Sensors and sources referenced come from the presentation: HC-SR04 ultrasonic, MPU6050 IMU, front/side/driver cameras with object detection, radar (blind spot), GPS and V2V (LoRa / ESP8266).

---

## 1. Sample Inputs and Expected Outputs

Timestamps in the CSV are illustrative (IST).

### 1.1 Distance and Motion Sensors

| ID | Source | Zone | Input | Expected risk | Buzzer | Display | Voice | V2V broadcast | Logged |
|---|---|---|---|---|---|---|---|---|---|
| S01 | HC-SR04 | Front | Distance = 40 cm | Collision warning | Yes | Yes | Yes | TBC | Yes |
| S02 | HC-SR04 | Front | Distance = 350 cm | None | No | No | No | No | TBC |
| S03 | MPU6050 | Vehicle | Longitudinal accel = −8.5 m/s² | Abnormal driving condition flagged | TBC | TBC | TBC | TBC | Yes |
| S04 | MPU6050 | Vehicle | Longitudinal accel = −0.4 m/s² | None | No | No | No | No | TBC |

### 1.2 Camera-Based Hazard Detection

| ID | Source | Zone | Input | Expected risk | Buzzer | Display | Voice | V2V broadcast | Logged |
|---|---|---|---|---|---|---|---|---|---|
| S05 | Camera detection | Front | Pedestrian, confidence 0.91 | Hazard: pedestrian | Yes | Yes | Yes | Yes | Yes |
| S06 | Camera detection | Front | Animal, confidence 0.84 | Hazard: animal | Yes | Yes | Yes | Yes | Yes |
| S07 | Camera detection | Front | Vehicle, confidence 0.95 | Hazard: vehicle (depends on distance/closing speed, TBC) | TBC | TBC | TBC | TBC | Yes |
| S08 | Camera detection | Front | Obstacle, confidence 0.88 | Hazard: obstacle | Yes | Yes | Yes | Yes | Yes |
| S14 | Camera detection | Front | No detections | None | No | No | No | No | TBC |

### 1.3 Blind-Spot Sensing (Camera + Radar Fusion)

| ID | Source | Zone | Input | Expected risk | Buzzer | Display | Voice | V2V broadcast | Logged |
|---|---|---|---|---|---|---|---|---|---|
| S09 + S10 | Camera + radar | Left blind spot | Two-wheeler (confidence 0.89) and radar object present = 1 | Blind-spot hazard: left | Yes | Yes | Yes | TBC | Yes |

### 1.4 Driver Monitoring

| ID | Source | Zone | Input | Expected risk | Buzzer | Display | Voice | V2V broadcast | Logged |
|---|---|---|---|---|---|---|---|---|---|
| S11 | Driver camera | Driver | Eyes closed 3.0 s | Drowsiness warning | Yes | Yes | Yes | No | Yes |
| S12 | Driver camera | Driver | Head turned away 4.0 s | Distraction warning | Yes | Yes | Yes | No | Yes |
| S13 | Driver camera | Driver | Eyes closed 0.2 s (blink) | None | No | No | No | No | TBC |

### 1.5 Location and V2V

| ID | Source | Input | Expected behaviour |
|---|---|---|---|
| S15 | GPS | Position 13.0827, 80.2707 (illustrative, Chennai) | Position attached to logged risk events |
| S16 | V2V receive | Hazard message received from nearby bus (BUS-B, illustrative ID) | Received hazard alert shown to the driver; buzzer and voice **TBC**; not re-broadcast |

---

## 2. Notes on Interpreting the Samples

1. **"Yes / No"** values are the expected behaviour for the clear-cut sample only.
2. **TBC** means the presentation does not define the behaviour (for example, whether sudden braking triggers an immediate driver alert or only a flag and log entry).
3. **Alert wording** (display text and voice messages) is not defined and is therefore not shown.
4. **V2V message format** is not defined. S16 describes behaviour only, not a payload.
5. **Real data:** once the prototype is built, replace these samples with recorded data and update the expected outputs from observed behaviour, with team approval.

## 3. Related Documents

- `TEST_CASES.md` references these samples (S01–S16) as input data.
- `Technical_Design_Document.md` describes the modules that produce the behaviour above.

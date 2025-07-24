# 📋 Vahini AI Pen — Data Acquisition Guide (v0.2)

## 🧠 Objective

To build a high-quality IMU dataset tailored for offline handwriting recognition in regional Indian languages (e.g., Hindi, Telugu), enabling intelligent digital ink conversion and interaction modeling.

---

## ✍️ Recording Environment

* **User Position**: Seated, comfortable posture at a flat desk
* **Writing Surface**: A4 paper (80–100 GSM), backed with 4–5 sheets for support
* **Lighting**: Bright, uniform indoor lighting
* **Hand Posture**: Natural grip; start with right-hand users, extend to left-handers

---

## 🖋️ Digital Pen Setup (Anonymized)

| Module             | Role                                     |
| ------------------ | ---------------------------------------- |
| IMU Unit           | Captures motion, tilt, angular rotation  |
| Environmental Unit | Captures compass/orientation vectors     |
| Pressure Module    | Detects pen–surface contact force        |
| BLE MCU            | Streams sensor data wirelessly (via BLE) |

> *Note: Specific sensor brands/models anonymized for vendor-agnostic reproducibility.*

---

## 🗃️ Data Schema

Each writing session produces:

* `sensor_data.csv`
  Columns: `timestamp`, `acc_x/y/z`, `gyro_x/y/z`, `mag_x/y/z`, `pressure`, `sample_id`

* `labels.csv`
  Format: `char`, `start_time`, `end_time`, `user_id`, `language`

* `calibration.txt`
  Sensor offsets, gain, bias correction (per session)

---

## 🪄 Language-Specific Instructions

| Language | Coverage          | Writing Notes                  |
| -------- | ----------------- | ------------------------------ |
| Hindi    | अ–ह, ॠ, क्ष, ङ... | Block + cursive, if applicable |
| Telugu   | అ–ఔ, క–హ, ద్ద...  | Include vowel-modifiers        |
| English  | A–Z, a–z          | Standard print + cursive       |

---

## 🎯 Companion App (in development)

* BLE-based connection to the pen
* Displays characters for writing tasks
* Records IMU + pressure + interaction timestamp
* Multilingual UI for participant ease
* Auto-labels character samples per user session

---

## 🔁 Recording Procedure

1. Character prompt shown on phone/tablet
2. Participant writes on physical paper
3. Sensor stream is recorded with timestamps
4. Optional: “Mark done” tap/gesture used for label tagging
5. Proceed to next prompt

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/058358e7-9ece-49f3-b587-d2a0612ef3b6" />


---

## ✅ Participant Guidelines

* Write **one character per session**
* Maintain **natural handwriting speed**
* Pen cap off; tip aligned before each trial
* Keep strokes within printable area (optional guide)

---

## 🧪 Data Validation

* Manual spot checks for drift, mislabeling
* Optional preprocessing: `split_characters.py`
* Store datasets in `.pkl` or `.npy` format (Tensor-compatible)

---

## 📁 Folder Format

```
/dataset/
  ├── user_01/
  │   ├── sensor_data.csv
  │   ├── labels.csv
  │   ├── calibration.txt
  ├── user_02/
  │   └── ...
```

---

## 🧠 Optional: U-Net for Pen-Tip Segmentation

To establish **ground-truth pen trajectory**, optionally integrate:

* **Tablet + external camera setup** (60–120 FPS)
* Use **U-Net**-based segmentation model to isolate the pen tip
* Correlate with IMU time-series using synchronized timestamps
* Enables **multi-modal dataset fusion**: camera + IMU

> This pipeline improves recognition granularity but is not mandatory for core IMU dataset development.

---

## 📌 Notes

* Minimum **5–10 samples per character per user**
* Separate folders for language/script variations
* Dialect annotations encouraged
* Explore **gesture/tap** commands as extended events (`tag="gesture_save"`)

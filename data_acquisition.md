# 📋 Vahini AI Pen — Data Acquisition Guide

## 🧠 Objective

To build a robust IMU dataset for handwriting recognition using the Vahini AI Pen, targeting regional languages like Hindi, Telugu, etc., for character recognition and AI model training.

---

## ✍️ Recording Environment

* **Position**: User should be seated comfortably at a table.
* **Surface**: Standard A4 white paper (80–100 GSM) placed over 5 supporting sheets.
* **Lighting**: Well-lit indoor environment with minimal distractions.
* **Grip**: Natural hand posture. (Encourage right-hand grip initially; left-hand later.)

---

## 🖋️ Vahini AI Pen Setup

| Component          | Purpose                   |
| ------------------ | ------------------------- |
| Accelerometer (x2) | Motion and tilt detection |
| Gyroscope          | Angular movement tracking |
| Magnetometer       | Orientation and stability |
| Force Sensor       | Pen contact pressure      |
| BLE SoC (STM32WB)  | Wireless data transfer    |

---

## 🗃️ Data Structure

Each recording will generate:

* `sensor_data.csv`:

  * Timestamps, Acc\_X/Y/Z, Gyro\_X/Y/Z, Mag\_X/Y/Z, Force, Sample ID
* `labels.csv`:

  * Columns: `char`, `start_time`, `end_time` (referencing `Millis` in `sensor_data.csv`)
* `calibration.txt`:

  * Sensor offsets, temperature compensation, etc.

---

## 🪄 Language Expansion Process

| Language | Character Set     | Writing Instructions         |
| -------- | ----------------- | ---------------------------- |
| Hindi    | अ–ह, ॠ, ङ, क्ष... | Block and cursive encouraged |
| Telugu   | అ–ఔ, క–హ          | Include compound characters  |
| English  | A–Z, a–z          | Follow natural print/cursive |

---

## 🎯 Data Collection App (To Be Developed)

* Connects to Vahini Pen via BLE
* Displays target characters on screen
* Tracks written character by IMU and fire button events
* Auto-stores per-character samples via labels
* UI in multilingual options for participant comfort

---

## 🔁 Procedure

1. Display character on tablet/phone
2. User writes character on paper
3. Timestamp + IMU + Force data logged
4. When done, fire button is tapped (optional)
5. Auto-save entry (segment & label)
6. Proceed to next character

---

## ✅ Guidelines for Participants

* **One character at a time**
* **Use natural speed**
* **Ensure pen cap is removed before writing**
* **Write within boundary (optional guide on page)**

---

## 🧪 Dataset Validation

* Post-recording, validate each sample visually
* Use `split_characters.py` for automatic segmentation
* Store in `.pkl` or `.npy` format for model training

---

## 📁 Storage Format

```
├── user_01/
│   ├── sensor_data.csv
│   ├── labels.csv
│   ├── calibration.txt
├── user_02/
│   ├── ...
```

---

## 📌 Notes

* Capture at least 5–10 samples per character
* Add separate folder for each language
* Annotate dialects if applicable

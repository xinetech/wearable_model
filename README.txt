
Wearable KiCad Schematic Skeleton (v1) — 2025-10-14

Folders:
- wearable_ppg_ecg.kicad_pro            → Project file (open this in KiCad)
- wearable_ppg_ecg.kicad_sch            → Top-level schematic
- sheets/*.kicad_sch                  → Sub-sheets for each domain
- lib/superid_wearable.kicad_sym      → Custom symbol library (simple rectangles with pins)

How to open:
1) Open wearable_ppg_ecg.kicad_pro in KiCad 7/8.
2) In Schematic Editor, if symbols show as missing, add the library:
   Preferences → Manage Symbol Libraries → Project Specific → Add:
   Path = ${KIPRJMOD}\lib\superid_wearable.kicad_sym (or use the absolute path).
3) Wire global nets with "Place → Global Label" across sheets, e.g. +3V3, GND, VBAT, VLED, SCL, SDA, etc.
4) Replace the placeholder symbols with official vendor symbols if desired, or keep these rectangles for rapid iteration.
5) When finalized, proceed to PCB Editor and assign footprints.

Notes:
- This skeleton includes core ICs: nRF52840, AFE4404, AD8232, BQ24074, TPS63031, MAX17048, BMI270, W25Q80, DRV2605L, USB-C, Antenna, Photodiode, LEDs.
- You will still need to add passives (caps, resistors, inductors) around each IC per datasheet/app notes. Place these from KiCad's default "Device" library.
- Power rails: +5V_USB → BQ24074 → VBAT → TPS63031 → +3V3. VLED is derived from VBAT.
- Buses: I2C0(SCL/SDA) connects MCU ↔ AFE4404/MAX17048/BMI270/DRV2605L. SPI0 connects MCU ↔ W25Q80.
- Signals: ECG_OUT → MCU ADC; AFE_INT/IMU_INT/ECG_ALARM/HAPTIC_EN → MCU GPIOs.

After you finish passives and wiring, I can generate PCB + Gerbers.

# DDR Pad with Arduino 4 to 8 FSR + GUI
A high-performance cheap DIY arcade dance pad built on a solid MDF frame, featuring 3D-printed PETG brackets and custom polycarbonate panels. Driven by an Arduino Pro Micro (1000Hz HID), it uses 8 FSR sensors in a parallel circuit with hardware RC filters to wipe out latency and electrical noise. The ultimate stamina build at a smart price!

# 🕺 DIY FSR Custom Dance Pad - The Smart Budget Build

A high-performance, arcade-grade DIY dance pad (DDR / ITG) built from scratch. This project bypasses overpriced pre-built kits and sponsored components to deliver rock-solid 1ms responsiveness on a smart budget.

## 🎯 Technical Specifications
* **Polling Rate:** 1000Hz native (1ms latency) via hardware HID emulation.
* **Sensors:** 8 FSR (Force Sensing Resistor) sensors configured in a parallel layout.
* **Brain:** Arduino Pro Micro (ATmega32U4) with USB-C.
* **Signal Conditioning:** Dedicated hardware RC filters for every analog pin.
* **Chassis:** 15mm 18mm MDF base, 3D-printed PETG brackets, and impact-resistant Polycarbonate arrows.

## 💾 Software Overview
This repository includes:
- **Firmware Normal Version:** Customized Arduino sketch utilizing the native HID Keyboard.h library for instant keystrokes, with internal filters and post processing
- **Firmware Lite Version:** Customized Arduino sketch utilizing the native HID Keyboard.h library for instant keystrokes without post-processing. Only hit your FSR and check the result!
- **DDR V.4.0 FSR APP**: A custom Python GUI desktop application to monitor raw ADC values (0-1023) from the Arduino in real-time. Crucial for measuring mechanical pre-load and fine-tuning threshold limits.

**HARDWARE**
- 1x Arduino Pro Micro ATmega32U4 5V 16MHz
- 8x FSR406 Force Sensitive Resistor 0.5 Inch
- 8x 100NF Capacitors
- 8x 10k Resistors
- 1x Universal PCB Prototype Board Double Sided Tin-plated
- 1x LAN Cable 8 pin about 3mt (300cm)
- 1x Single rigid cable for 5V 

## 🛠️ Electronics Architecture (The "Splitter" Junction)
To eliminate ghost inputs and disconnects caused by foot-stomp vibrations, the electronics are housed in an external Control Box near the PC. Every analog channel features a dedicated Pull-Down resistor and an ammortizing capacitor.

```text
               +5V (From Arduino to Pad)
                |
             [ FSR ] (On Pad - Connected in Parallel pairs)
                |
 PIN A0 --------+--------+
(Arduino)       |        |
            [Resistor] [Capacitor]
             10k Ohm    0.1uF (104)
                |        |
               GND ------+ (Common Ground back to Arduino)
```

**Why this circuit?**
The 10k Ohm Resistor acts as a Pull-Down, pulling the analog pin firmly to 0V when the arrow is idle. This stops the sensors from floating and misfiring.
The 0.1µF (104) Ceramic Capacitor acts as an electronic damper. Since a 150cm cable acts like an antenna, it picks up electromagnetic noise. The capacitor absorbs high-frequency spikes and dumps them to GND right before they enter the Arduino.

<img width="50%" height="50%" alt="20260601_083310" src="https://github.com/user-attachments/assets/92d354db-2cd8-4d1b-a2cd-8bd1a6531b20" />

<img width="50%" height="50%" alt="20260601_083301" src="https://github.com/user-attachments/assets/6108d923-7d45-4955-8b7b-9357eb3e6e62" />
<img width="50%" height="50%" alt="20260602_171027" src="https://github.com/user-attachments/assets/df121d77-1860-4c42-af75-f90716bc490c" />
<img width="50%" height="50%" alt="20260601_123646" src="https://github.com/user-attachments/assets/62f88587-4ad0-4679-a5b0-85fd00ac2579" />
<img width="50%" height="50%" alt="20260602_171416" src="https://github.com/user-attachments/assets/2e914e3d-3f95-4e70-ade8-dfdda73faca9" />
<img width="50%" height="50%" alt="20260602_171411" src="https://github.com/user-attachments/assets/f3c68f5d-73bc-4025-b1d1-af2f12c8389f" />
<img width="50%" height="50%" alt="20260602_171408" src="https://github.com/user-attachments/assets/122a1625-ff2b-41f6-9459-c6d2edb3df95" />


## 🚀 How to Replicate This Build
- Clone this repository
- Flash the firmware onto the Arduino Pro Micro using the Arduino IDE (select Arduino Leonardo as the board).

<img width="1093" height="605" alt="image" src="https://github.com/user-attachments/assets/556dab21-a2a7-4a64-a0b6-0af8e4bd185e" />
<img width="683" height="374" alt="image" src="https://github.com/user-attachments/assets/091c0ff1-7a90-4f83-8e31-2d9bf2d835a3" />


Just remember to include **Library Joystick** from here
https://github.com/mheironimus/arduinojoysticklibrary
Add directly as .zip
<img width="720" height="457" alt="image" src="https://github.com/user-attachments/assets/a4c6bb42-eca8-4f04-9359-cab6553253c5" />

- Upload on your Arduino
<img width="560" height="156" alt="image" src="https://github.com/user-attachments/assets/3ca90cb8-0c93-4c85-888a-7ff2a837a763" />

- Now fire up the DDR V.4.0 FSR APP, balance your FSR and ADC (higher is better) until idle values stabilize near zero, load up StepMania/OutFox, and start stamping!
<img width="1918" height="1137" alt="Software DDR PAD V 4" src="https://github.com/user-attachments/assets/4a2012fe-92db-4f9e-87ab-bb5062dcb4db" />

---

## 📐 3D Printing Settings (Structural Brackets)
The corner and side brackets are printed to maximize mechanical durability for the threaded inserts embedded in the MDF, prioritizing perimeters over 100% infill density.
- **Material:** PETG (Perfect balance of strength and impact flexibility). otherwise PLA.
- **Wall Line Count:** 5 walls (Thick shell to handle countersunk screw pressure).
- **Infill**: 7% to 13% using Gyroid pattern (Provides omnidirectional shock resistance).
- **Layer Height:** 0.28mm (Optimizes inter-layer bonding and saves print time/energy) or just go with 0.20mm
- **Top/Bottom Layers:** 5 solid layers.

## OTHERS FILES
- **STL**: Printable STL
- **DWG**: Drawings

## 💰 Needed
**PAD WITH 3D PRINTED**
- 1x MDF 15mm / 18mm 840mm x 840mm
- 5x HDF 5mm 280mm x 280mm (BEWARE...it works but it bend)
- 4x Polycarbonate 5mm 279mm x 279mm (yes...it bend and return in position)
- Over 60x printed pieces (follow instructions)

**PAD WITH WOOD (a lot less screw)**
- 1x MDF 15mm / 18mm 840mm x 840mm
- 5x MDF 10mm 280mm x 280mm (Easy fix on the corners)
- 24x MDF 3.2mm 50mm x 50mm (for Polycarbonate corners, and FSR sensors)
- 16x MDF 3.2MM 50mm x 25mm (for Polyarbonate sides)
- 4x Polycarbonate 5mm 279mm x 279mm (yes...it bend and return in position)

## **PHOTOS**
<img width="50%" height="50%" alt="20260529_163911" src="https://github.com/user-attachments/assets/6cf1459a-30c3-4a43-95ab-53479d8675c2" />
<img width="50%" height="50%" alt="20260530_163717" src="https://github.com/user-attachments/assets/dca66901-8889-4c1d-bbd2-292641988711" />
<img width="50%" height="50%" alt="20260530_164143" src="https://github.com/user-attachments/assets/8acb0dcc-85d6-42f6-9115-bc6e7bda58ef" />
<img width="50%" height="50%" alt="20260601_143857" src="https://github.com/user-attachments/assets/c4d60bbc-a8d8-4ab6-982a-e58e65c37c9e" />

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

---

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

## 📐 3D Printing Settings (Structural Brackets)
The corner and side brackets are printed to maximize mechanical durability for the threaded inserts embedded in the MDF, prioritizing perimeters over 100% infill density.
- **Material:** PETG (Perfect balance of strength and impact flexibility). otherwise PLA.
- **Wall Line Count:** 5 walls (Thick shell to handle countersunk screw pressure).
- **Infill**: 7% to 13% using Gyroid pattern (Provides omnidirectional shock resistance).
- **Layer Height:** 0.28mm (Optimizes inter-layer bonding and saves print time/energy) or just go with 0.20mm
- **Top/Bottom Layers:** 5 solid layers.

## 💾 Software Overview
This repository includes:
- **Firmware Normal Version:** Customized Arduino sketch utilizing the native HID Keyboard.h library for instant keystrokes, with internal filters and post processing
- **Firmware Lite Version:** Customized Arduino sketch utilizing the native HID Keyboard.h library for instant keystrokes without post-processing. Only hit your FSR and check the result!
- **DDR V.4.0 FSR APP**: A custom Python GUI desktop application to monitor raw ADC values (0-1023) from the Arduino in real-time. Crucial for measuring mechanical pre-load and fine-tuning threshold limits.

## OTHERS FILES
- **STL**: Printable STL
- **DWG**: Drawings

## 💰 Needed
**PAD**
- 1x MDF 15mm / 18mm 840mm x 840mm
- 5x MDF 10mm 280mm x 280mm
- 4x Polycarbonate 5mm 279mm x 279mm 

**HARDWARE**
- 1x Arduino Pro Micro ATmega32U4 5V 16MHz
- 8x FSR406 Force Sensitive Resistor 0.5 Inch
- 8x 100NF Capacitors
- 8x 10k Resistors
- 1x Universal PCB Prototype Board Double Sided Tin-plated 

## 🚀 How to Replicate This Build
- Clone this repository.
- Degrease your polycarbonate sheets with isopropyl alcohol and apply the arrow graphic decals to the under side of the panels using the wet application method (water + drop of soap) for a mirror-smooth, scratch-proof finish.
- Solder the component matrix inside the external Control Box, grouping the 10k resistors and 104 capacitors onto a prototyping stripboard.
- Flash the firmware onto the Arduino Pro Micro using the Arduino IDE (select Arduino Leonardo as the board).
- Fire up the DDR V.4.0 FSR APP, balance your FSR until idle values stabilize near zero, load up StepMania/OutFox, and start stamping!

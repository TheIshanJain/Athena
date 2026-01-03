# ATHENNA 🤖

**ATHENNA** is a modular, RF‑controlled surveillance and rescue robot featuring a 3‑axis robotic arm, a tracked drivetrain, dual‑mode control (manual + autonomous), and a robust power architecture designed for long standby and field reliability.

This repository is intended to be a **complete, build‑from‑scratch reference**. It contains:

* Circuit diagrams
* Arduino source code (TX & RX)
* Hardware explanations
* Build notes and design decisions

If you are a student, maker, or robotics enthusiast looking to build a **real, field‑deployable robot** rather than a desk demo, this project is for you.

---

## 📑 Table of Contents

* Key Features
* System Architecture
* Power System
* Robotic Arm (3‑DOF)
* Control Logic
* Repository Structure
* Circuit Diagrams
* Build Notes & Lessons Learned
* Future Improvements
* Media & Documentation
* License

---

## 🔧 Key Features

* RF‑based long‑range wireless control (NRF24L01)
* Dual‑mode operation:

  * **Manual mode** — RF joystick + potentiometers
  * **Autonomous mode** — ultrasonic obstacle avoidance (optional)
* 3‑axis robotic arm (X, Y, Z) with gripper
* Track‑belt drive system for rough / uneven terrain
* Dual‑Arduino architecture for control redundancy
* Relay‑based mode and power switching
* Sleep / low‑power standby mode
* Modular, hackable design for easy upgrades

---

## 🧠 System Architecture Overview

ATHENNA is divided into **two primary subsystems**:

### 1. Transmitter Unit (Controller)

* Arduino Nano
* NRF24L01 RF module
* Joysticks (robot motion + arm control)
* Potentiometers (arm calibration and default positions)
* Powered via regulated 5V

### 2. Receiver Unit (Robot)

* Arduino Nano (or dual‑Nano setup)
* NRF24L01 RF module
* L298N motor driver (tracked drivetrain)
* Servo motors (robotic arm)
* Relay module (mode switching)
* Ultrasonic sensor (optional autonomous mode)
* 3S Li‑ion battery pack with linear regulators

---

## ⚡ Power System

* **Battery**: 3 × 18650 Li‑ion cells (3S ≈ 12V)
* **Voltage Regulation**:

  * 7805 → Arduino, logic circuitry, SG90 servos
  * 7809 → MG995 high‑torque servo
* **Motor Power**: Direct 12V supply via L298N
* **Protection & Reliability**:

  * Relays for isolating power and control modes
  * Dedicated cooling fan for motor driver

> **Note:** The NRF24L01 is powered from the Arduino’s 3.3V pin. For electrically noisy environments, an external 3.3V regulator with proper decoupling is strongly recommended.

---

## 🦾 Robotic Arm — 3 DOF

| Axis      | Servo          | Function                |
| --------- | -------------- | ----------------------- |
| X         | Standard servo | Base rotation           |
| Y (Lower) | MG995          | Arm lift / load bearing |
| Y (Upper) | SG90           | Elbow articulation      |
| Z         | SG90           | Gripper open / close    |

* Arm structure is **homemade**, using PVC and 3D‑printed brackets
* Potentiometers allow manual calibration and default pose storage

---

## 🧭 Control Logic

### Manual Mode

* RF packets transmit:

  * Joystick X/Y values
  * Robotic arm axis positions
* Receiver directly maps values to motors and servos

### Autonomous Mode (Optional)

* Ultrasonic sensor scans for obstacles
* Simple decision flow:

  * **Stop → Rotate → Move forward**
* Relay logic isolates manual controls during autonomous operation

---



## 🧩 Circuit Diagrams

All circuit diagrams are provided in the `/circuit diagrams` folder and include:

* Transmitter 
* Receiver 

The diagrams are intentionally **maker‑friendly**, optimized for zero‑PCB builds and hand‑soldered prototyping.

---

## 🧪 Build Notes & Lessons Learned

* Linear regulators dissipate significant heat — **use heatsinks**
* NRF24L01 modules are highly sensitive to electrical noise
* A common ground across all subsystems is critical
* Relays greatly simplify debugging and improve safety
* Always test arm servos individually before final assembly

---

## 🚀 Future Improvements

* Custom PCB‑based transmitter and receiver
* ESP‑based telemetry, logging, and video streaming
* PID‑based autonomous navigation
* IMU‑assisted arm stabilization
* Battery health and current monitoring

---

## 📸 Media & Documentation

The build process, failures, and iterations are documented through short, engineering‑focused videos.

*(Links can be added here)*

---

## 📜 License

This project is open‑source and released under the **MIT License**.

You are free to:

* Build it
* Modify it
* Improve it
* Use it for learning or competitions

Attribution is appreciated.

---

## 🙌 Final Note

ATHENNA is not a polished commercial robot.
It is an **engineer’s robot** — built, broken, fixed, and improved in the real world.

If you build your own version, break it, improve it, and learn from it — then this repository has done its job.

Happy building.

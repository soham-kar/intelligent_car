# 🤖 Arduino Voice-Controlled Obstacle Avoidance Robot

This project implements a smart robot that can move using **voice commands** (via serial input) and intelligently avoid obstacles using an **ultrasonic sensor** and **IR sensor**. The robot is controlled using an **Adafruit Motor Shield**, and features a **servo-based head** to visually indicate turns.

---

## 🧠 Features

- 🎤 Voice control via serial commands
- 🧭 Obstacle avoidance using ultrasonic sensor (NewPing)
- 🚗 4-wheel drive using AFMotor
- 🦾 Servo-based directional head movement
- 🔁 Bidirectional motion (forward + reverse)
- 🚦 IR sensor safety for backward movement
- 🛑 Auto-stop when obstacle detected

---

## 🔧 Hardware Required

| Component                  | Quantity |
|---------------------------|----------|
| Arduino Uno / Mega        | 1        |
| Adafruit L293D Motor Shield | 1      |
| DC Motors (TT gear or BO) | 4        |
| Ultrasonic Sensor (HC-SR04)| 1       |
| IR Sensor (for reverse)   | 1        |
| Servo Motor (SG90)        | 1        |
| Battery Pack (9V or 12V)  | 1        |
| Jumper Wires + Chassis    | -        |

---

## 🛠️ Libraries Used

Install these libraries via Arduino Library Manager:

- [`AFMotor`](https://github.com/adafruit/Adafruit-Motor-Shield-library)
- [`NewPing`](https://bitbucket.org/teckel12/arduino-new-ping/wiki/Home)
- [`Servo`](https://www.arduino.cc/en/Reference/Servo)

---

## 🎮 Voice Commands

| Command         | Action                          |
|----------------|----------------------------------|
| `move forward` | Move forward while checking distance |
| `move backward`| Move backward (uses IR safety)   |
| `left` / `turn left` | Turn left with servo indicator |
| `right` / `turn right`| Turn right with servo indicator |
| `stop`         | Stop all motors immediately      |

> 🗣️ **Voice commands are sent via Serial Monitor** (9600 baud) or Bluetooth module (e.g., HC-05).

---

## 🖼️ System Diagram


---
## 📷 How It Works

1. 🧠 Robot listens for a voice command (via Serial).
2. 🎯 For `move forward`, it checks ultrasonic distance:
   - If distance < 10cm → Stop
   - Else → Drive forward
3. 🧼 For `move backward`, it checks IR sensor:
   - If object detected → Stop
   - Else → Drive backward
4. ↪️ For left/right, it:
   - Turns servo to look left/right
   - Rotates wheels accordingly
5. 🛑 After obstacle, resets servo and motor state.

---

## 📝 Code Overview

- `AFMotor` controls all 4 DC motors.
- `NewPing` reads distance from HC-SR04.
- `Servo` rotates head to show turning direction.
- Commands are matched from `Serial.readString()`.

> 🧪 Includes safety: robot stops if obstacle is too close or IR detects danger when reversing.

---

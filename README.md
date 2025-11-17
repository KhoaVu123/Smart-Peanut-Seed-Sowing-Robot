# Smart Peanut Seed Sowing Robot (AI-Ready)

A low-cost, STEM-friendly agricultural robot that can **sow peanut seeds at two positions simultaneously**, controlled by a **wireless PS2 gamepad** and built on an **Arduino/ STEMVN board** platform.  

---

## 1. Project Overview

Traditional peanut farming in Vietnam still relies heavily on manual labour. Sowing each seed by hand is:

- Time-consuming  
- Physically demanding (especially for elderly farmers and women)  
- Prone to human error (uneven spacing, depth, etc.)

This project proposes a **semi-automatic seed sowing robot** that:

- Moves along planting beds (ridges)  
- Allows the user to steer it with a **PS2 wireless controller**  
- Drops peanut seeds **simultaneously at two positions** using a servo-based mechanism  

The system is built using affordable, widely available components (Arduino-compatible STEMVN board, DC motors, servo motor, PS2 controller) so that **farmers, schools and STEM clubs** can replicate and extend it.

The robot is designed to be **“AI-ready”**: future versions can integrate AI features (e.g. path planning, row detection, yield optimisation) on top of the existing hardware and control logic.

---

## 2. Key Features

- 🚜 **Two-row seed sowing**  
  Servo mechanism opens two holes at once, improving speed and consistency compared to manual sowing.

- 🎮 **Intuitive PS2 controller**  
  Use the left joystick for movement and a button (e.g. `X / CROSS`) to trigger seed release.

- 🔌 **Arduino / STEMVN based control**  
  Open, low-cost microcontroller platform (Arduino Uno-compatible) with easy programming.

- 🧩 **Modular, open design**  
  Separate movement system, seeding mechanism and control electronics – easy to upgrade or repair.

- 🎓 **Perfect for STEM education**  
  Combines **mechanics, electronics and programming** in one real-world project.

- 🌱 **Environment-friendly & scalable**  
  Uses simple, low-power components and can be adapted to other crops (corn, beans, etc.) and to different field layouts.

---

## 3. Hardware Overview

**Main Components**

- **Controller board**: STEMVN Board (Arduino Uno-compatible)
- **Drive system**  
  - DC gear motors (left & right)  
  - Motor driver (e.g. L298N or similar)  
  - 4-wheel or tracked chassis
- **Seeding system**  
  - Seed hopper for peanuts  
  - Seed distribution tubes (2 sowing positions)  
  - Servo motor controlling the seed gate
- **Remote control**  
  - Wireless PS2 gamepad  
  - PS2 receiver module
- **Power**  
  - Rechargeable battery pack (approx. 4.2 V, low-voltage DC system)

**Approximate robot specs**

- Dimensions: 270 mm (L) × 250 mm (W) × 210 mm (H)  
- Weight: ~2 kg  
- Power: rechargeable battery, charged via 5 V DC adapter

---

## 4. Software Overview

The robot firmware is written in **C/C++ for Arduino** and uploaded via EasyCode / Arduino IDE.  
It uses two main libraries:

```cpp
#include <PS2X_lib.h>  // PS2 controller support
#include <Servo.h>     // Servo motor control
```

### Main logic

- **Setup (`setup()`)**
  - Initialise Serial (for debugging)
  - Configure PS2 gamepad pins
  - Attach servo to `SERVO_PIN`
  - Set motor driver pins (ENA/ENB, IN1–IN4) as outputs

- **Loop (`loop()`)**
  - Read PS2 gamepad state
  - Map joystick values to movement:
    - `PSS_LY` forward / backward  
    - `PSS_LX` left / right
  - Call helper functions:
    - `moveForward()`, `moveBackward()`, `turnLeft()`, `turnRight()`, `stopMotors()`
  - If sow button is pressed (e.g. `PSB_CROSS`):
    - Rotate servo to open seed gate  
    - Wait (e.g. `delay(500)`) for seeds to drop  
    - Return servo to closed position

Example movement function:

```cpp
void moveForward() {
  digitalWrite(IN1, HIGH); digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH); digitalWrite(IN4, LOW);
  analogWrite(ENA, 150);   // speed left
  analogWrite(ENB, 150);   // speed right
}
```

---

## 5. Repository Contents

This repository currently contains:

- `Gieo lac 2 lo.html`  
  HTML code (e.g. documentation, visualisation or simple UI demo for the project).

- `EasycodeV4.0.2_Setup.exe`  
  Installer for the **EasyCode** IDE used to program the STEMVN / Arduino board.  
  Because this file is large, it is **hosted on Google Drive instead of inside the repository**.  
  See the download link in the section below.

---

## 6. Software Download

The EasyCode IDE installer required to program the STEMVN / Arduino board can be downloaded from Google Drive:

- **EasycodeV4.0.2_Setup.exe**: [Click here](https://drive.google.com/drive/u/0/folders/1ufYK7DLcyUFjd8wbWLYIC1pgFNweaL9D)

You can also add any future tools or drivers here as separate bullet points.

---

## 7. Getting Started

### 7.1. Prerequisites

**Hardware**

- Assembled robot:
  - STEMVN / Arduino Uno board  
  - Motor driver  
  - 2 × DC motors + wheels  
  - 1 × Servo motor  
  - Seed hopper + 2 seed outlets  
  - PS2 wireless controller + receiver  
  - Battery pack, power switch  

**Software**

- Windows PC (or other OS supported by EasyCode)  
- Web browser (Chrome/Edge/Firefox)  
- EasyCode IDE (download from your Google Drive link above)  
- (Optional) Arduino IDE if you prefer

### 7.2. Install EasyCode

1. Open the Google Drive link in the **Software Download** section.  
2. Download `EasycodeV4.0.2_Setup.exe` to your computer.  
3. Double-click the installer and follow the steps to complete installation.  
4. Connect the STEMVN / Arduino board to your PC via USB.  
5. Ensure the correct drivers are installed (Arduino Uno driver, if needed).

### 7.3. Upload the Firmware

> If you already have the firmware project file (.ino or EasyCode project), place it in this repository (for example under `src/`).

1. Open **EasyCode**.  
2. **Open** the existing project or `.ino` file for the seed sowing robot.  
3. Select the correct **board type** (Arduino Uno / compatible).  
4. Select the correct **COM port**.  
5. Click **Upload** to flash the firmware to the board.  
6. Wait until the upload is complete and EasyCode reports success.

### 7.4. HTML File (`Gieo lac 2 lo.html`)

Depending on how you designed it, this HTML file can be used as:

- A simple **documentation page** describing the project, or  
- A **demo interface / visualization** (e.g. explaining the sowing process, block diagram, etc.)

To view it:

1. Open the repository folder.  
2. Double-click `Gieo lac 2 lo.html`.  
3. Your default browser will open the page.

---

## 8. How to Use the Robot

1. **Prepare the seed hopper**
   - Fill the hopper with peanut seeds.
   - Make sure the two seed outlets (two holes) are not blocked.

2. **Power on**
   - Turn on the robot’s main power switch.
   - Ensure the PS2 controller is powered on and paired with the receiver.

3. **Control movement (example mapping)**
   - **Left joystick up**: move forward  
   - **Left joystick down**: move backward  
   - **Left joystick left**: turn left  
   - **Left joystick right**: turn right  
   - Centered joystick: stop (or call `stopMotors()` in code)

4. **Sow seeds**
   - When the robot reaches the correct position along the ridge:
     - Press the **sow button** (e.g. `X / CROSS` on the PS2 pad).
     - The servo rotates, opening the gate and dropping seeds from both outlets.
     - After a short delay, the servo closes the gate again.

5. **Repeat**
   - Move to the next sowing position and repeat the process until the row is completed.

---

## 9. System Architecture

The system is logically divided into three subsystems:

1. **Control subsystem**
   - STEMVN / Arduino board  
   - Reads PS2 input  
   - Generates motor and servo control signals

2. **Mobility subsystem**
   - DC motors + driver + chassis  
   - Handles robot movement over soil ridges / flat test surfaces

3. **Seeding subsystem**
   - Seed hopper + tubes + servo gate  
   - Releases seeds at two positions simultaneously when triggered

Data flow:

1. User moves joystick / presses button on PS2 controller.  
2. PS2 receiver module sends signal to STEMVN board.  
3. Firmware interprets input and:  
   - Controls DC motors (movement) via PWM and direction pins  
   - Controls servo (sowing) through `Servo` library  
4. Mechanical system drops seeds into the soil at predefined positions.

---

## 10. Educational & Practical Applications

- **For farmers**
  - Reduces manual labour in sowing  
  - Helps maintain consistent sowing distance and depth  
  - Suitable for **small plots** and **narrow ridges**

- **For schools & STEM centres**
  - Hands-on project integrating:
    - Electronics (Arduino, drivers, sensors/actuators)
    - Mechanics (chassis, seed mechanism)
    - Programming (C/C++ on microcontrollers)
  - Can be used in robotics competitions, project-based learning, and innovation challenges.

---

## 11. Future Work & AI Integration

Planned and possible improvements:

- **Full automation**
  - Add sensors (line tracking, distance sensors, IMU, GPS) for autonomous navigation.
- **AI-enhanced planning**
  - Integrate AI models to plan optimal paths, adapt sowing density to soil conditions, or predict yield.
- **Crop versatility**
  - Adjustable seeding mechanism for different seed sizes (corn, beans, vegetables).
- **Solar power**
  - Add small solar panels to recharge batteries in the field.
- **Mobile / web control**
  - Add Bluetooth / Wi-Fi module and develop a smartphone app for control and monitoring.

You may choose an open-source license that fits your goals (for example, MIT License or Creative Commons for educational use).  
Update this section when you decide on a specific license.

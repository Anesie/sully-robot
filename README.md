# 🤖 Project Sully: Autonomous Collector Robot (LeJOS EV3)

## 📖 Presentation
**Sully** is an autonomous robot developed in **Java** using the **LeJOS** library for the LEGO Mindstorms EV3 brick. 
Sully's main objective is to explore its environment to detect, catch, and bring back as many pucks as possible to a starting zone within a time limit.

This project implements advanced software robotics concepts: finite state machines, differential chassis control, basic odometry (internal compass system), and real-time sensory data processing.

## ⚙️ Project Architecture
The code is structured into three main classes to separate decision-making logic, mechanical actions, and data acquisition:

- **`SullyMain.java` (The Brain):** Contains the main program loop structured as a **Finite State Machine** (`Debut`, `RechercherPalet`, `PrendrePalet`, `RamenerPalet`, `Fin`). It manages Sully's logical transitions based on sensor feedback.
- **`Actions.java` (The Motricity):** Encapsulates all movement logic (via `MovePilot` and `WheeledChassis`). It handles wheel motor control (adjustable speeds), the gripper opening/closing system, and integrates an internal "compass" based on rotation time to track the robot's orientation.
- **`Capteurs.java` (The Senses):** Manages the hardware interface with the environment. It initializes and queries:
    * The **Ultrasonic** sensor (detecting pucks at a distance).
    * The **Touch / Pressure** sensor (confirming that the puck is securely inside the gripper).
    * The **Color** sensor (for floor analysis).

## ✨ Main Features
1. **Intelligent Search (Scanning):** Sully rotates on itself at reduced speed. It monitors sudden distance variations (calculating the `seuil` / threshold) via the ultrasonic sensor to isolate a puck's position.
2. **Secure Gripping:** Once a puck is spotted, Sully moves forward. The grippers only close when the pressure sensor confirms physical contact with the object.
3. **Odometry and Return to Base:** The robot tracks its rotation angle via a `boussole` (compass) variable incremented during movements. Once the puck is caught, Sully calculates the exact return angle (`getAnglePoints`) to bring it back to the starting point.
4. **Random Movements & Avoidance:** If no puck is detected during a scan, Sully moves randomly to change perspective and restart a search.

## 🛠️ Technologies Used
- **Language:** Java (Object-Oriented)
- **Robotics Framework:** [LeJOS EV3](http://www.lejos.org/ev3.php)
- **Hardware:** LEGO Mindstorms EV3 (2 Large Motors for wheels, 1 Motor for the gripper, Ultrasonic, Touch, and Color sensors).

## 🚀 Prerequisites and Execution
To compile and execute this project on your own EV3 robot:
1. Ensure your EV3 brick is flashed with an SD card containing the **LeJOS** OS.
2. Install the LeJOS plugin on your IDE (Eclipse recommended).
3. Import this repository as a Java/LeJOS project.
4. Connect the robot via Bluetooth or Wi-Fi.
5. Launch compilation and execution directly from the IDE.
6. Press any button on the EV3 brick to start the cycle (`Button.waitForAnyPress()`).

# CAN.pptx 

## Things I'm confused about 

## After class TODO

## Notes 

## CAN
CAN stands for **Controller Area Network**. It is a robust communication protocol designed to allow microcontrollers and devices (called "nodes") to communicate with each other without needing a central computer.
Originally developed by Bosch in the 1980s, CAN is widely used in automotive systems but is also popular in industrial automation, robotics, and medical equipment.

### 🚗 Real-World Example
In a car, systems like the engine control unit (ECU), anti-lock braking system (ABS), power steering, airbags, and dashboard displays all use CAN to talk to each other efficiently and reliably.

### 🧠 Key Features of CAN:
| Feature                 | Description                                                              |
| ----------------------- | ------------------------------------------------------------------------ |
| 🧩 Multi-Master Network | Any node can start communication if the bus is idle                      |
| 🔄 Message-Based        | Communication is based on messages, not device addresses                 |
| ⏱ Real-Time Capable     | Prioritization ensures time-critical messages are delivered first        |
| 🛡 Robust and Reliable  | Includes error detection, retransmission, and fault isolation            |
| 🔌 Two-Wire Bus         | Uses two twisted wires (CAN High and CAN Low) for differential signaling |

### 🧱 Basic CAN Bus Structure:
* Two physical wires: CAN\_H (high) and CAN\_L (low)
* Connected in parallel across all nodes
* Termination resistors (usually 120 ohms) at each end of the bus

### 💬 How Messages Work
* Each message includes:
  * An identifier (used for prioritization)
  * Up to 8 bytes of data (in classic CAN)
  * A CRC (for error checking)
* Nodes receive all messages but only process ones they care about.

### ✅ Summary

| What CAN Is     | A reliable protocol for communication between embedded devices            |
| --------------- | ------------------------------------------------------------------------- |
| Where It's Used | Cars, trucks, drones, robots, medical devices, industrial control systems |
| Why It’s Great  | Simple wiring, strong error detection, supports many devices on one bus   |

---

## Cyclic Redundancy Check (CRC)

A **Cyclic Redundancy Check (CRC)** is an error-detecting code used to detect accidental changes to raw data in digital networks and storage devices. It is widely used in communication protocols like Ethernet, USB, and file formats such as ZIP and PNG.
### 💡 In Simple Terms:
A CRC is a type of checksum — it’s a small value (typically 8, 16, or 32 bits) calculated from a larger block of data using polynomial division. When data is sent, the CRC value is calculated and sent along with it. On the receiving end, the CRC is recalculated and compared. If it doesn't match, there's likely an error in the data.

### 🧮 How It Works (Conceptually):
1. You treat the data as a large binary number.
2. You divide it (using binary division) by a fixed binary polynomial (called the generator).
3. The **remainder** from that division is the CRC.
4. You append this CRC value to the message.
5. The receiver performs the same division; if the remainder is not zero, it detects an error.

### ✅ CRC Use Cases:
* Ethernet frame error detection
* File integrity (e.g., .zip files)
* Flash memory storage validation
* Automotive and industrial communication (e.g., CAN bus)

### 📘 Example (CRC-8):
Let’s say your data is: `11010011101100`
And your generator polynomial is: `1011` (CRC-3)
You perform binary division and get a remainder (say, `100`).
So the full message sent becomes: `11010011101100100`.
If even 1 bit changes during transmission, the remainder won't match when the receiver checks.

---

## Bit Stuffing

### 🔧 Why do we "bit-stuff" in a CAN bus?
In the Controller Area Network (CAN) protocol, **bit stuffing** is used to ensure that the signal remains synchronized and to avoid confusion with special control signals — especially the **End of Frame (EOF)** and **acknowledgment** bits.

### 🧠 What is Bit Stuffing?
Bit stuffing means:
👉 Every time the transmitter sends **five consecutive bits** of the same value (either five 1s or five 0s), it **inserts a "stuffed" bit** of the opposite value.
For example:
* If the data has: `11111`, a 0 is added → `111110`
* If the data has: `00000`, a 1 is added → `000001`
The receiver knows to remove the stuffed bit when it sees five identical bits in a row.

### 🧩 Why is Bit Stuffing Necessary in CAN?
1. **Clock synchronization**
   * CAN is asynchronous — there’s no separate clock line.
   * Bit stuffing creates edges (changes from 1 to 0 or 0 to 1), which help the receiver stay synchronized with the sender's timing.
2. **Avoiding special bit patterns**
   * Certain patterns (like 6 or more consecutive 1s) have special meaning in CAN — for example, marking the end of a frame.
   * Bit stuffing prevents data from accidentally looking like control information.

### 🎯 Summary:
🟩 Bit stuffing ensures:
* Proper timing (synchronization)
* No accidental control signal mimicry
🟥 It is automatically handled by CAN controllers, so as a programmer or engineer, you usually don’t need to manually stuff bits.

---

<img width="573" alt="Screenshot 2025-05-20 at 9 41 22 AM" src="https://github.com/user-attachments/assets/5f50ba59-1459-4fa8-acd3-33e4269d2b9c" />

---

## OBD-II (On-Board Diagnostics II)

**OBD-II (On-Board Diagnostics II)** is a standardized system built into most modern cars and trucks to monitor and report the health of the vehicle's key systems—especially the engine and emissions-related components.

### 🚗 What Does OBD-II Do?
* It continuously monitors systems like the engine, transmission, fuel, and exhaust.
* If something goes wrong (e.g., a misfire, faulty oxygen sensor, or high emissions), the system:
  * Logs a **Diagnostic Trouble Code (DTC)**
  * Turns on the **"Check Engine" light**

### 🔌 Where Is It Found?
OBD-II systems are required in all cars and light trucks sold in the U.S. since **1996**.
You can usually find the OBD-II port:
* Under the dashboard
* Near the driver's seat
* It's a **16-pin** connector
This port is used to plug in a diagnostic tool or scanner.

### 🔧 What Can You Do With It?
Using an OBD-II scanner, you can:
* Read and clear error codes (DTCs)
* View real-time data (engine RPM, temperature, fuel trim, etc.)
* Perform emissions tests
* Track fuel efficiency and driving habits

### 📡 Communication Protocols
OBD-II supports several communication protocols (depending on vehicle make and model), including:
* **CAN (Controller Area Network)** — the most common today
* **ISO 9141-2**
* **SAE J1850 PWM/VPW**
* **KWP2000**

### ✅ Summary
| Feature        | Description                                          |
| -------------- | ---------------------------------------------------- |
| Full Name      | On-Board Diagnostics II                              |
| Required Since | 1996 (U.S. vehicles)                                 |
| Used For       | Emission control, engine diagnostics, data logging   |
| Interface Type | 16-pin port, usually under the dashboard             |
| Access Tool    | OBD-II scanner or Bluetooth/WiFi dongle + mobile app |







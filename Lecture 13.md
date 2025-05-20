# CAN.pptx 

## Things I'm confused about 

## After class TODO

## Notes 



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



<img width="573" alt="Screenshot 2025-05-20 at 9 41 22 AM" src="https://github.com/user-attachments/assets/5f50ba59-1459-4fa8-acd3-33e4269d2b9c" />


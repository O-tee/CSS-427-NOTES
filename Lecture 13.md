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

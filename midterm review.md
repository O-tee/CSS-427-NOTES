# Embedded systems
- A **microcontroller** contains a microprocessor, RAM, ROM and peripherals.
- An **Embedded System** is a microcontroller that is dedicated to a specific task; often not thought of as a computer.
- Embedded systems should be matched to their task: Too much computing power = lower battery life, higher cost
- An atom is the smallest unit of computer code. It cannot be interrupted.

 




# Bit Twiddling
Bit twiddling in Arduino (or any C/C++ program running on microcontrollers like the AVR-based Arduino Uno) involves using **bitwise operations** to directly manipulate individual bits of variables or hardware registers. Here's a quick guide to common bit twiddling techniques in Arduino:

### 🔧 Common Bit Twiddling Operations

| Operation                      | Code Example                   | Description                         |                                |
| ------------------------------ | ------------------------------ | ----------------------------------- | ------------------------------ |
| **Set a bit**                  | \`PORTB                        | = (1 << 2);\`                       | Sets bit 2 of `PORTB` to 1     |
| **Clear a bit**                | `PORTB &= ~(1 << 2);`          | Clears bit 2 of `PORTB` (sets to 0) |                                |
| **Toggle a bit**               | `PORTB ^= (1 << 2);`           | Toggles bit 2 of `PORTB`            |                                |
| **Check if bit is set**        | `if (PORTB & (1 << 2)) {...}`  | Tests if bit 2 of `PORTB` is 1      |                                |
| **Write a bit (set or clear)** | \`PORTB = (PORTB & \~(1 << 2)) | (val << 2);\`                       | Writes `val` (0 or 1) to bit 2 |

### 🧠 Example: Blinking an LED with Bit Twiddling
```cpp
void setup() {
  DDRB |= (1 << DDB5); // Set pin 13 (PB5) as output
}

void loop() {
  PORTB |= (1 << PORTB5);  // Set PB5 HIGH
  delay(500);
  PORTB &= ~(1 << PORTB5); // Set PB5 LOW
  delay(500);
}
```
This turns on and off the built-in LED on pin 13 using direct port manipulation.

### 💡 Why Bit Twiddle?

* **Faster** than `digitalWrite()`
* **More control** over hardware (multiple bits at once)
* **Essential** for low-level operations like setting timer registers, SPI control, etc.

Would you like a reference sheet for common AVR ports and pins for the Arduino Uno or Mega?






# UART Serial
- UART is full duplex but slow
- Every UART character needs a start bit and at least one stop bit
- Time to send string = #char * #bits / baud
- Processor does not wait after sending string
- Interrupts tell when Rx or Tx is complete
- USB is half duplex but fast
- Other forms of serial include SPI, I2C and CAN

**UART Serial** (Universal Asynchronous Receiver/Transmitter) is a **hardware communication protocol** that allows two devices to exchange data **asynchronously**, meaning there's no shared clock signal. It's one of the most common ways microcontrollers like an **Arduino** talk to other devices like computers, sensors, or Bluetooth modules.

### 🔌 Key Features of UART:
* **Two wires**:
  * **TX** (Transmit): sends data
  * **RX** (Receive): receives data
* **Asynchronous**: both sides agree on a common **baud rate** (speed), but don't share a clock.
* **Serial data transmission**: sends one bit at a time.
* **Start and stop bits** frame each byte of data.
* Often includes **parity bits** for basic error checking (optional).

### 🧠 UART in Arduino:
Arduino provides built-in UART support via the `Serial` object:
```cpp
void setup() {
  Serial.begin(9600); // Start UART at 9600 baud
  Serial.println("Hello!");
}

void loop() {
  if (Serial.available()) {
    char c = Serial.read();   // Read incoming character
    Serial.write(c);          // Echo it back
  }
}
```
### 🛰️ Uses:

* Communicating with a PC via USB-to-serial (Arduino Uno uses ATmega16U2 as USB-to-UART bridge)
* Connecting to GPS modules, Bluetooth (like HC-05), ESP8266/ESP32 modules, etc.
Would you like a diagram showing how UART works or how to connect two UART devices?

## SPI vs. UART
<img width="573" alt="Screenshot 2025-05-06 at 9 04 40 AM" src="https://github.com/user-attachments/assets/e2c14ac9-ba3b-4e2b-8b06-ff1969d6ea38" />

### Arduino SPI pins 
<img width="509" alt="Screenshot 2025-05-06 at 9 06 04 AM" src="https://github.com/user-attachments/assets/b005316f-0916-4749-892e-555fa3aa23d2" />




# Interrupts
A running process can pause when an interrupt takes over
- The interrupt must not corrupt registers or data used by others
- Lock out interrupts while manipulating any variables that could be changed by interrupts.
- Minimize time in interrupt service routines
- “volatile” warns the compiler not to optimize variables
- 2 external interrupts on Uno; 6 on Mega
- Interrupt vector table provides many more 

 
Initialize all variables; reset will not restore original values
- **EEPROM** is meant for parameters that seldom change
- Interrupts can remove the need for blocking code.
- Think of the worst case for interrupts happening at the wrong time and prevent it.
- Integer arithmetic is faster than floating point
- A union can remove the need to cast to another type
- Keypad outputs to rows and reads columns.

const int circum = 397
- stores in flash mem
- without const, it does to ram 

#define circum = 397
- takes the text 'circum and replaces it with 397

**Interrupts** are a fundamental feature in microcontrollers (like the one in an Arduino) that **temporarily pause the normal execution of code** to immediately respond to important events — like a button press, a sensor signal, or a timer expiring.

### ⚡ What is an Interrupt?

Think of it like this:

> You're reading a book (your `loop()` function), and someone taps you on the shoulder to tell you something important. You stop reading, deal with the situation (interrupt), and then go back to your book.

### 🧠 Why Use Interrupts?
* Efficient: You **don’t have to constantly check** (poll) a pin or timer — the system alerts you.
* Fast: The microcontroller **reacts immediately** to critical events.
* Accurate: Especially helpful for **precise timing**, like pulse-width measurements or responding to real-time input.

### 🚨 Common Interrupt Sources:

* **External interrupts**: triggered by changes on certain pins (e.g., a button press)
* **Timer interrupts**: triggered at regular intervals
* **Serial interrupts**: when data arrives via UART

### 🧪 Example in Arduino (Button on Pin 2):
```cpp
volatile bool flag = false;

void setup() {
  pinMode(2, INPUT_PULLUP);              // Attach button to pin 2
  attachInterrupt(digitalPinToInterrupt(2), handleInterrupt, FALLING);
  Serial.begin(9600);
}

void loop() {
  if (flag) {
    Serial.println("Button Pressed!");
    flag = false;
  }
}

void handleInterrupt() {
  flag = true;
}
```

### ⚠️ Interrupt Tips:
* **Keep interrupt functions short** — no `delay()`, `Serial.print()`, or long logic.
* Use `volatile` for variables shared between `loop()` and ISR (Interrupt Service Routine).
* Some interrupts disable other operations temporarily — plan accordingly.

Would you like a visual diagram of how interrupts work?






## Float Arithmetic

<img width="500" alt="image" src="https://github.com/user-attachments/assets/9346ca1a-8b4e-4777-834d-663ebf6683be" />






## Integer Arithmetic
<img width="694" alt="image" src="https://github.com/user-attachments/assets/f49e634d-2065-405c-8b5a-7391a93faf15" />




## Round off





## Avoiding Round off





# Timers




## Music with timer: Globals



## Set note duration timer




## Set frequency timer


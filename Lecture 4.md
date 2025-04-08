# Lecture 4 (4/8/25) Sensors Electronics.ppxt AND Serial.ppxt

## Things I'm confused about 

## Something to read after the lecture 

## Notes  

When tested at 25°C, the TMP36 typically is accurate to ±1°C, but it can be off by ±3°C
- scale factor is typically 10 mV/°C
- scale factor typically remains linear within 0.5°C
- When held at 150°C for 1000 hours, the sensor usually varies by 0.4°C or less.
- Output voltage is limited to 0.1 to 2V, corresponding to a temperature range of -40 to 150 °C (-40 to 302°F) 
<br/>

Calibration
- Linear: f(t) = a * t
- Affine: f(t) = a * t + b
- More general affine: f(t) = a * x(t) + b
- What is x(t)?
  - For the TMP36, f(x) = 100 (5/1023) * x + (-50)
    - f(x) = 0.489 * x - 50 
  - Here x is the reading we get from Arduino: 0 to 1023f(x) is temperature in C.
<br/>

Lower Level Calibration 
- If the sensor is not linear, we can force it.
  - Polynomial:
    - x(t) = a5 t5 + a4 t4+ a3 t3 + a2 t2 + a1 t + a0
- This extrapolates poorly!
- Usually dominated by a1 and a0.
- Higher order terms smooth out the bumps.
- Rational: x(t) = (a t + b) / (t + d)
  - Better extrapolation and easier to invert.
<br/>

Electronic and Microcontroller Symbols 
<img width="1039" alt="image" src="https://github.com/user-attachments/assets/15c12d25-2f2b-4cc9-b698-9db76dc0a33e" />
<br/>

Fuses
- If the current gets too high, it generates a lot of heat and burns out the resistor or IC.
- Circuits are usually designed with sacrificial elements called fuses. 
- The fuse will be destroyed with too much current, but it protects the rest of the circuit. 
- A fuse can be made from a thin piece of metal that vaporizes with too much current. 
- Fuses are rated for their maximum current. 
- There are fast-blow fuses that go right away at the stated current and slow-blow fuses that wait for the excess current to be sustained.
<br/>

Capacitors Explained
- https://www.youtube.com/watch?v=X4EUwTwZ110
<br/>

Transmitting data in parallel
- Suppose we want to send the character “W”.
- Convert to ASCII: 0x57 = 101 0111
- Use 6, 7 or 8 bits, and send
  1. High  (LSB)
  2. High
  3. High
  4. Low
  5. High
  6. Low
  7. High
  8. Low (MSB)
- Each signal is on a separate Data Out line

<img width="607" alt="Screenshot 2025-04-08 at 10 18 51 AM" src="https://github.com/user-attachments/assets/93e6e19a-f0a8-4df3-83ad-d8794e2be211" />
<br/>

Parallel is better than Serial 
<br/>

Serial Timing 
- Data is sent at a predetermined rate.
- Original RS-232 was intended for < 20,000 baud (bits / s).
- 300 baud had been common.
- With 1 start bit, 8 data bits, 1 stop bit, no parity: baud/10 = bytes/s.
- Common to have 6-8 data bits, 1-2 stop bits, sometimes parity bit.
<br/>

Universal Asynchronous Receive / Transmit (UART)
- Works with hardware standard RS-232.
- Or, can set voltage levels to 5V and 0V.
- A common rate is 9600 baud.
- Full duplex
  - Rx (receive)
  - Tx (transmit)
  - Vcc (high)  - optional
  - Ground (0V)
<br/>

Buffer
- To send the text “Hello, world”, the characters are written to a buffer.
- Hardware will place a byte on the parallel or serial line at the proper time.
- The hardware is driven by a timer. Microcontrollers have several timers that can go at different rates.
- After the last character has been sent to the receiving buffer (or when the buffer fills) the receiving processor gets an interrupt notifying it of data availability.
<br/>

Arduino Serial Class
- void Serial.begin( int baud_rate); /* 4800, 9600, 19200, 115200, etc.  */
- Serial.print(“Hello World”);
- Serial.print( value ); // int, float, char, *char
- Serial.print( value, BASE); /* BASE = BIN, OCT, DEC, HEX or floating digits. */
- Serial.println(); // same as print but includes CR, LF
- More on https://www.arduino.cc/reference/en/language/functions/communication/serial/ 
<br/>

Parity 
- UART Serial has the option to include a parity bit
- If data is corrupted and noise flips the value of one bit, parity will indicate that there is an error.
- Suppose we transmit “HELlo” with even parity.
  - In ASCII, “HELlo” is 0x48 45 4C 6C 6F or 
  - 01001000_ 01000101_ 01001100_ 01101100_ 01101111_
  - H has 2 bits set to 1. We want the total number of bits to be even; set the parity bit to 0.E has 3 bits set to 1; set the parity to 1.
- 010010000 010001011 010011001 011011000 011011110
- Adding start and stop bits gives
- 0010010000100100010111001001100110011011000100110111101
<br/>

To compute the transmission time for a message
<img width="660" alt="Screenshot 2025-04-08 at 10 35 54 AM" src="https://github.com/user-attachments/assets/17215d4a-943b-4aa2-b2b7-eea699dc2a83" />
<img width="677" alt="Screenshot 2025-04-08 at 10 39 13 AM" src="https://github.com/user-attachments/assets/004eb275-fdfc-4df3-92d9-041020e9b516" />



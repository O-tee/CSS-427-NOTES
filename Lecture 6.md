# Lecture 6 (4/15/25) Interrupts.ppxt

## Things I'm confused about 

## After class TODO

## Notes Interrupts 

Atomicity
- An atom is the smallest unit of computer code.
- Atoms correspond to machine language instructions.
- Interrupts can only occur between code atoms.
- What is atomic on one architecture is not on another.
- Interrupts can occur in the middle of a single C instruction.
<br/>

You can disable and enable interrupts (?) 
- 🔴 1st Red Arrow – disable();
This function call disables interrupts on the microcontroller. By turning off interrupts, it prevents the interrupt service routine (ISR) — in this case, vReadTemperatures() — from running while the main code is accessing the shared iTemperatures[] array. This avoids a situation where the array could be modified mid-read, causing inconsistent or corrupted values.
- 🔴 2nd Red Arrow – enable();
This re-enables interrupts after both temperature values have been safely copied to local variables (iTemp0 and iTemp1). Once the shared data is safely read, it's safe to let interrupts occur again.
- 🧠 In summary:
The red-arrowed section creates a "critical section" — a short block of code that is protected from concurrent modification by temporarily disabling interrupts. This ensures atomic access to the shared iTemperatures[] array.
<img width="488" alt="Screenshot 2025-04-15 at 9 19 57 AM" src="https://github.com/user-attachments/assets/0b941266-ef4b-4171-8e98-1c9e0b6aa2e5" />

Other Interrupts 
- The attachInterrupt() routine only works with the Arduino’s external interrupts.
- The AVR has other interrupts that are used for 
  - Timing
  - UART serial
  - SPI and TWI (I2C) serial
  - Pin change
  - Analog Input

Interrupt Vector Table
- There is a table of interrupt vectors (each vector is a few bytes).
- The table is typically at the start or end of addressable memory space.
- Each vector is typically a jump to an ISR.
- On power-on, the processor goes to address 0 or 0xFF...FF, where a vector jumps to start-up code.
- If D2 is attached to an interrupt, when that line goes active the processor jumps to the second entry in the table

Pin change interrupt
- The Uno is organized in ports
- Port D has digital pins 0,1,2,3,4,5,6,7  (PCINT2)
- Port B has digital pins 8,9,10,11,12,13 and two pins not used on Arduino  (PCINT0)
- Port C has analog pins 0,1,2,3,4,5 (PCINT1)
- The Mega has its own port organization.
- Whenever any pin on a port changes, the pin change interrupt is active.
- See pages 162-166 of Williams.

Name of Pin Interrupts <br/>
<img width="658" alt="Screenshot 2025-04-15 at 10 13 24 AM" src="https://github.com/user-attachments/assets/a3a8545c-c88a-4f7c-a6b9-e69968bb7f73" />





---
Interrupts are incredibly useful and often essential in embedded systems like the Arduino. Here’s why you’d want to use them:
### ✅ Why Use Interrupts?
1. **Respond to Events Immediately**  
   Interrupts let your microcontroller react instantly to external events (like a button press, sensor spike, or data from a serial port) without constantly checking (polling) for them in the main loop.
2. **Efficient CPU Usage**  
   Without interrupts, you'd have to write code that constantly checks for input ("busy waiting"). Interrupts free the CPU to do other things, making your program more efficient.
3. **Precise Timing**  
   For tasks like reading sensors at specific intervals or generating precise PWM signals, interrupts help maintain consistent timing—especially with timer interrupts.
4. **Handling Asynchronous Data**  
   Interrupts are perfect for receiving serial data, counting pulses from an encoder, or measuring the time between two signal edges.
   
### ⚠️ When to Be Careful
- If you’re using shared variables (like in the image you posted), you need to protect them from being changed mid-operation by disabling interrupts briefly (as shown).
- Interrupts should be kept short and fast—do as little as possible inside them and return quickly.

### 🔧 Common Use Cases
- External interrupt from a button (attachInterrupt in Arduino)
- Timer interrupt to blink an LED or log data every second
- Serial receive interrupt to store incoming bytes in a buffer
- Analog-to-digital conversion complete interrupt
So yes—you'd definitely want interrupts in your toolbelt. They're like your microcontroller's way of saying, "Hey, something just happened — you might want to deal with it!"



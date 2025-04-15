# Lecture 5 (4/10/25) Serial.ppxt AND Interrupts.ppxt

## Things I'm confused about 

## After class TODO

## Notes Serial 
Serial Peripheral Interpahce (SPI)
- Four wire connection
  - CIPO: Controller in, peripheral out. Aka MISO: Master in, slave out.
  - COPI: Controller out, peripheral in. Aka MOSI
  - SCK/CLK: Explicit clock
  - CS: Chip select (active low) aka SS.
  - Power
  - Ground
- All wires except CS are shared by one Controller and several Peripherals.
- There is a separate CS from Controller to each Peripheral.

![image](https://github.com/user-attachments/assets/ef2c22a4-6ae4-407f-badb-7608fe7c4e3c)

In System Programming (ISP) is a variant of SPI
- ISP includes SPI signals MISO, MOSI and SCK
- ISP supplies power and ground
- ISP does not include the SPI Chip Select line, which is usually required
- Protocols for ISP vary
- For chip programming, some systems keep the Vcc pin at 5V, others raise it to 12V
- The Reset pin is used to signal programming
<img width="554" alt="image" src="https://github.com/user-attachments/assets/b14924e9-3ab8-4277-a854-f48467e1ffc2" />

SPI Mode
- SPI is a loose standard; read the device datasheet.

SPI on Arduino
- SPI.beginTransaction( SPISettings(…) );
- digitalWrite (CS, LOW);  // Makes peripheral pay attention to SPI
- SPI.transfer(); // perhaps multiple times
- digitalWrite (CS, HIGH);  // Peripheral ignores SPI
- SPI.endTransaction(); 

Physical location of SPI pins
- You can use any pin for CS; can have several.
- Shields expect to find SPI on 10, 11, 12, 13
- All Arduinos have the same connection to SPI on the ICSP
- ICSP (In-Circuit Serial Programming) has no CS
<img width="478" alt="Screenshot 2025-04-10 at 9 52 39 AM" src="https://github.com/user-attachments/assets/6d3043c9-9978-4016-8f9f-84cbceed651d" />


<br/> Overhead percentage <br/>
<img width="443" alt="Screenshot 2025-04-11 at 10 16 47 AM" src="https://github.com/user-attachments/assets/d4b4da80-66d5-4d8e-94af-bef15a2a0132" />


<br/> USB: universal serial bus (425)
- Reference: https://simple.wikipedia.org/wiki/USB
- Huge installed base
- On most MCU (microcontroller unit), also used as the control port, for JTAG, downloading code to execute, and single-step MCU programs
- There may be addition USB ports for input or output:
  - USB 1.1: 1.5 or 12 Mbps
  - USB 2.0: 480 Mbps
- 4 wire interface (usb3 [?]):
  - Ground & +5v DC power (Vbus)
  - Twisted pair differential half-duplex data
<br/>

CAN: Controller Area Network (425)
- The Controller Area Network (CAN) bus is a robust communication protocol used in automotive and industrial applications to enable efficient data exchange between electronic control units (ECUs). It utilizes a two-wire twisted pair for differential signaling, enhancing resistance to electromagnetic interference. This system allows multiple ECUs to communicate over a single bus, reducing wiring complexity and improving reliability.
- Reference: https://en.wikipedia.org/wiki/CAN_bus
- Invented by Bosch for automobile control
- Widely used in cars, trucks and commercial aircraft
- Three wire:
  - Ground
  - Differential signal pair
- Half duplex
- Some microcontrollers support it, e.g. TIVA
- I have a pair of CAN shields for Arduino MCU
<br/>

DAC: Digital to Analog conversion (425)
- Two main types:
  - Direct: weighted sum of currents to produce a voltage
  - Indirect: vary duty cycle of a signal, and low pass filter it (PWM)
- DAC in MCU
  - In the Arduino Uno, in the TIVA and is simpler STM32, there is no internal DAC
  - In the lab kit, the TIVA port B is connected to an external DAC08 Integrated Circuit.
  - The STM32 devices in the lab contain two 12-bit DACs, which can be written at 5 MHz rates
  - In the Winter 2025 class, some students used the STM32 to generate the waveforms in software
<br/>

PWM: Pulse Width Modulation (425)
- This is a simple digital-to-analog conversion method
- Tradeoff: arbitrary precision, but precision costs time
- The GPIO output port is digital: high (e.g. +3.3v) or low voltage
- The output is periodic at some programmed frequency
- The output is low pass filtered, resulting in an average value somewhere between the low and high voltages
- If the duty cycle is 50%, the filtered output will be 50%, e.g. 1.65v
- If always off, filtered output is 0.0v; if always on, filtered output is 3.3.v
- The filter cutoff frequency should be a lot lower than the periodic frequency, perhaps 10:1
<br/>

ADC: Analog to Digital COnverstion (425)
- There are three main types of ADC:
  - Flash: expensive and fast
  - Dual slope: cheap, very accurate, and slow
  - Successive approximation: intermediate cost, can be fast enough
- Flash conversion is used in digitizing communication waveforms
  - Typically, their will be a low noise preamp and automatic gain control at the front end, to constrain the number of bits to convert
- Dual slow is mostly used in lab instruments
- Successive approximation ADC are common
  - All the MCUs described on Lesson 2 contain 1 or more of them
<br/>

Falsh ADC (425)
- In general, the number of comparators is exponential with resolution.
- The main application: digitizing communications waveforms or video camera waveforms.
- For communications (physical layers), there will typically be a low noise analog front end followed by an automatic gain control amplifier
- Result: constrain the dynamic range of the input, so less resolution is needed.

SAR: Successive Approximation Register (425) (do more research)








## Notes Inerrupts

Interrupts 
- When you move the mouse, it can generate an interrupt signal to the computer.
- The computer pauses the task it is doing, and jumps to a mouse service routine where it records the mouse position.
- The computer then resumes the task it was working on.
- At some time the operating system will run a thread that updates the display and moves the cursor to a new position.

AVR External Interrups 
- The Arduino Uno has two external interrupts, which are on D2 and D3.
- If you hook up a switch to D2, you can program the Arduino to react as soon as the switch changes state.
- The Arduino Mega has six interrupts on pins D2, D3, D18, D19, D20 and D21.
- The Arduino Due can interrupt on any digital pin.

Arduino Interrupts 
- attachInterrupt(number, ISR, mode);
  - ISR is interrupt service routine to call.
  - mode is RISING, FALLING, CHANGE or LOW.
- detachInterrupt();
- interrupts();
  - Looks like a subroutine but compiles to the one-byte assembly instruction SEI (set interrupt flag).
- noInterrupts();
  - Compiles to CLI (clear interrupt flag)
<br/>
 
Edge Interrupts 
- Edge interrupts have nothing to do with transitions of the system clock.
- An interrupt event (such as pushing a reset button) is asynchronous to the clock
- An edge interrupt is triggered when the button transitions from unpressed to pressed.
- A level interrupt is active while the button is pushed.
- There is no data associated with interrupts.

Interrupt Timing/Code
... 





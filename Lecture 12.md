<img width="321" alt="image" src="https://github.com/user-attachments/assets/b386305f-bb41-4cf5-9863-03d75261a645" /># (5/15/25) I2C.pptx and ARM.pptx

## Things I'm confused about 

## After class TODO

## Notes I2C.pptx

### Another Serial Format
- For short-distance intra-board communication
- Multi-controller
- Multi-peripheral
- Packet-switched
- Covered in Williams, pp. 361-364
- I2C is a trademark, so Arduino calls it TWI

### I2C transfer
- With the clock line (SCL) held high, bring SDA line low to start
- Master starts clock with a low pulse. Data goes onto SDA only while clock is low.
- When clock is high, receiver reads a data bit from SDA.
- After 8 bits, receiver writes a low on SDA to ACK the bit; or High if error
- When transfer is over, master stops clock and writes HIGH to both lines

### I2C Addresses
- Every device has a 7-bit address.
- Every communication between bus master and device starts with the address.
- 8th bit is direction:
  - High: Master will read data from device
  - Low: Master sends data to device

### Arduino Library: reading
- As Master: Wire.begin()
- As Device: Wire.begin(address)
- Master: Wire.requestFrom(address, quantity)
- A third bool parameter is stop:
  - if true, release I2C bus after request:
  - if false, retain bus for multiple requests.
- Wire.available();
- Wire.read();

### Writing
- Wire.beginTransmission(address);
- Wire.write(value);
- Wire.endTransmission();

### Clock
- Wire.setClock(frequency);
- 100,000 is standard.
- 400,000 is fast mode.
- Peripherals accept any frequency.

### Slave
Wire.onReceive(handler)

void handler( int numBytes) // expects to receive this many bytes.

<br/>

Wire.onRequest(handlerSend)

void handlerSend() // will be called when data is requested.

### Address
- Stephen Case; I2C Strikes Back; IEEE Spectrum, April 2023
- Mr. Case had published a project in which he left the last step to the readers: communicating from an Arduino Mega over I2C.
- Turns out this was non-trivial and involved hours of debugging to find out why it didn’t work.
- Tutorials had claimed I2C address range was 0-127; he selected 4.
- It turns out that addresses 0-15 are reserved.
- The code worked when he switched to a 2-digit address.


### Serial Standards
<img width="482" alt="Screenshot 2025-05-15 at 9 03 59 AM" src="https://github.com/user-attachments/assets/2ede4a0b-df11-4139-893a-3f5a4e77eef0" />







## Notes ARM.pptx

### Introduction
- ARM is a 32-bit Reduced Instruction Set Computer (RISC) instruction set architecture (ISA) developed by ARM.
- It was named the Advanced RISC Machine, and before that, the Acorn RISC Machine. Originally conceived by Acorn Computers for use in its personal computers.
- The relative simplicity of ARM processors makes them suitable for low power applications. As a result, they have become dominant in the
- mobile and embedded electronics market, as relatively low-cost, small microprocessors and microcontrollers.


### ARM CORTEX
- The family is divided into three subfamilies:CORTEX Ax, CORTEX Rx, and CORTEX Mx,
  - The x indicates that after the letter (A, R, M) is a number that identifies the core.>
<img width="522" alt="image" src="https://github.com/user-attachments/assets/18b2827e-f23a-467c-b303-33a112d80ac4" />

### ARM CORTEX Application
- ARM Cortex-A (Application)
- ARMv7-A or ARMv8-A architecture to provide fast performance for sophisticated devices such as smart phones and tablets. 
- They support full-fledged operating systems such as Linux, iOS, and Android.

### ARM CORTEX Real-Time
- The ARM Cortex-R (Real-time)
- High-performance computing solutions for embedded systems where reliability, high availability, fault tolerance and/or deterministic real-time responses are needed.
- Cortex-R processors are used in products where performance requirements and timing deadlines must always be met.
- In addition, Cortex-R processors are used in electronic systems which must be functionally safe to avoid hazardous situations, for example, in medical applications or autonomous systems.

### ARM CORTEX Microcontroller
- The ARM Cortex-M ( Microcontroller) 
- An excellent tradeoff between performance, cost, and energy efficiency.
- Suitable for a broad range of microcontroller applications such as home appliances, robotics, and smart watches\


### Architecture
<img width="461" alt="image" src="https://github.com/user-attachments/assets/f7509f36-e3f9-48d1-9b60-d43377be6531" />


### Thumb instructions
- ARMv7-M supports Thumb instructions and does not support the ARM 32. ARM processors are required to switch to the thumb state to execute 16-bit instruction and to the ARM state to run a 32-bit instruction. 
- Cortex-M processors can execute a mix of 16-bits and 32-bits thumb-2 instructions without changing the processor state, thus eliminating the overhead of state switching. 

### Instruction Sets
<img width="403" alt="image" src="https://github.com/user-attachments/assets/67329bed-2967-441e-97e7-e05f7c65ab74" />

Cortex-M processors are backward compatible. For example, a program compiled for M3 can run on Cortex-M4 without any modification


### Cortex-M Architecture
<img width="444" alt="image" src="https://github.com/user-attachments/assets/5c30724f-8856-4633-9104-5bcd76297bef" />

- Harvard Architecture RISC
- Instructions fetched from ROM using ICode bus
- Data are exchanged with memory and I/O via the system bus interface.
- On Cortex-M4, a second I/O bus for high-speed devices such as USB is available
- Having multiple buses means the processor can perform multiple tasks in parallel.
- The following are some of the tasks that can occur in parallel:
  - ICode bus: Fetch opcode from ROM
  - DCode bus: Read constant data from ROM
  - System bus: Read/write data from RAM or I/O, fetch opcode from RAM
  - PPB: Read/write data from internal peripherals
  - AHB: Read/write data from high-speed I/O and parallel ports (M4 only)
- Few instructions
- Fixed lengths
- Execute in 1 or 2 cycles,
- Only load and store can access memory,
- No one instruction can both read and write memory
- Many General Purposes registers
- Few addressing modes

---

- goes through load and store

---

### Initialization
- When the program {int x = -2; x = x + 1;} is loaded, x = -2.
- When the program executes once, x = -1.
- If the reset button is pushed, x stays -1 before execution.
- After reset and execution, x = 0.
- int x = 2; is a declaration and initialization; not an executable instruction.
- The program {int x; x = -2; x = x + 1} will behave differently.

### Assembly Instructions Supported
- Arithmetic and logic
  - Add, Subtract, Multiply, Divide, Shift, Rotate
- Data movement
  - Load, Store, Move
- Compare and branch
  - Compare, Test, If-then, Branch, compare and branch on zero
- Miscellaneous
  - Breakpoints, wait for events, interrupt enable/disable, data memory barrier, data synchronization barrier

### ARM Instruction Format
<img width="589" alt="Screenshot 2025-05-15 at 9 48 52 AM" src="https://github.com/user-attachments/assets/25c573eb-d16f-40e6-bdff-252289454aaa" />

- Label is a reference to the memory address of this instruction.
- Mnemonic represents the operation to be performed.
- The number of operands varies, depending on each specific instruction. Some instructions have no operands at all.
  - Typically, operand1 is the destination register, and operand2 and operand3 are source operands.
  - operand2 is usually a register.
  - operand3 may be a register, an immediate number, a register shifted to a constant amount of bits, or a register plus an offset (used for memory access).
- Everything after the semicolon “;” is a comment, which is an annotation explicitly declaring programmers’ intentions or assumptions. 

<img width="593" alt="Screenshot 2025-05-15 at 9 49 57 AM" src="https://github.com/user-attachments/assets/309705e0-bc42-4fe7-96a2-6e4a9de989a5" />

### Shifts
- Left shift << is multiplication by a power of two.
- X = y << 3;   // often faster than a multiply
- X = y * 8;   // same result
- In hardware, it is easy to build an adder or a shift register.
- How do you build a hardware multiplier?
- X = y * 5;   // 5 = 0b0101
- X = y + (y<<2);  // what the hardware is doing
- X = 1*y + 0*(y<<1) + 1*(y<<2) + 0*(y<<3);  // general
- A processor with no multiply instruction would add and shift in software.


### Registers

<img width="548" alt="Screenshot 2025-05-15 at 9 54 52 AM" src="https://github.com/user-attachments/assets/ec244d78-8a2b-4b35-a9ed-b1977627203b" />

- There are 21 registers (32 bit wide):
  - 13 General Purpose Registers which can hold data or addresses
  - Stack pointer, link pointer, and program counter
  - 5 special registers
 
- According to ARM Procedure Call Standard (AAPCS), registers R0,R1,R2, and R3 are used to pass input parameters into a C function. 
- The return parameter is placed in Register R0.
- The Program Counter R15 points to the address of the next instruction to be executed.


 <img width="520" alt="image" src="https://github.com/user-attachments/assets/2da2e0fa-b3b2-49d2-bd01-d0f9f4068c48" />


### PSR Register
<img width="567" alt="image" src="https://github.com/user-attachments/assets/d28f5979-a743-4ed8-ae4e-30688eef3128" />

- The Program Status Register has 3 status registers: Application (APSR), Interrupt(IPSR), and Execution (EPSR). 
- These registers can be accessed individually or in combination as the PSR.


### Link Register R14
- Link Register: Provides some linking functions to set up a connection between the main program and the calling functions or subroutines
- When a subroutine is called, the returning address should be entered into R14
- After the subroutine is done, the contents of R14 is fed into the PC so the program continues execution


### Stack Pointer Register R13
- Stack Pointer register (SPR) stores current stack address:
- The Main Stack Pointer (MSP) is used for the system program working in the handler mode
- The Process Stack Pointer (PSP) is used for the user’s program working in the thread mode.
- Only one stack pointer is active at a time. The default stack pointer is the MSP after the system is reset.

<img width="556" alt="image" src="https://github.com/user-attachments/assets/a4ae2605-29f9-4ccb-a9de-48f712dcc63d" />

<img width="546" alt="image" src="https://github.com/user-attachments/assets/18612755-de87-48ed-997b-46a3bc7672fe" />

### Memory

<img width="646" alt="Screenshot 2025-05-15 at 10 02 59 AM" src="https://github.com/user-attachments/assets/7c3c8e39-d089-45ea-b4da-505d162c0012" />

Microcontrollers within the same family differ by the amount of memory and by the types of I/O modules
Arduino Due is based on Atmel SAM3X8E Cortex-M3. It has100 KiB RAM, 512 KiB Flash, 103 PIO, PWM, CAN, DMA, USB

http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-11057-32-bit-Cortex-M3-Microcontroller-SAM3X-SAM3A_Datasheet.pdf 









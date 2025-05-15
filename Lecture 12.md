# (5/15/25) I2C.pptx and ARM.pptx

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


















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

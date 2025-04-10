# Lecture 5 (4/10/25) Serial.ppxt

## Things I'm confused about 

## After class TODO

## Notes
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





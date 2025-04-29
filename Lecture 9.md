# Lecture 9 (4/29/25) Actuators_Sensors.pptx

## Things I'm confused about 

## After class TODO

## Notes Actuators_Sensors

Wrist Watch 
- Actuators: Move the hands of the watch
- Sensors: Respond to knobs for settings

Blender 
- Actuators: Move the blender blades
- Sensors: Respond to pressed buttons

Mouse 
- Sensors: Button press, Wheel motion, Camera takes crude image of desktop
- Actuators: LED

Camera 
- Sensors: Light level, Focus, Button push
- Actuators: Lens zoom, Shutter activation, including video capture Flash

Sensors (inputs): 
<br/> <img width="466" alt="Screenshot 2025-04-29 at 8 57 55 AM" src="https://github.com/user-attachments/assets/79012bbd-235f-403b-8824-71fdf8e15adf" />

Analog to Digital Converter (ADC)
- Most sensors are analog.
- A transducer converts one quantity to another, typically voltage
- Analog voltages must go through an ADC before the microcontroller can use them
- The Arduino’s Analog Inputs use the ADC
- Chapter 7 of the text covers ADC in more detail than we need.

Step Resolution
- Suppose that a sensor has a 5V range.
- If it is sampled by an 8-bit ADC, there are 256 possibilities.
- The minimal detectable voltage change is 5V/255 = 20 mV.
- With a 10-bit ADC: 5V/1023 = 5 mv.
- With a 12-bit ADC: 5V/4095 = 1.2 mv.
- The resolution of the sensor needs to match the ADC

Excerise: Shaft Angle Sensor
- question: 
  - A sensor covers 360 degrees and is accurate to 1/3 of a degree. It produces an analog output of 0-5 V. What is the difference in voltages for two positions that differ by 1/3 degree?
  - How many bits should the ADC have?
  - If there is expected to be 10 mv of noise on the line, how does that change the choice of ADC?
  - Suppose a different model is selected that has the same 5V range and 1/3 degree accuracy, but only covers 60 degrees of rotation. How does the performance with 10 mv of noise compare to the other model?

- Answer
<img width="799" alt="Screenshot 2025-04-29 at 9 31 08 AM" src="https://github.com/user-attachments/assets/a07f5f0b-4b8e-4742-b7dc-c0ed62ae20ab" />
<img width="793" alt="Screenshot 2025-04-29 at 9 31 39 AM" src="https://github.com/user-attachments/assets/56af8638-9fd0-42b5-92a0-cef01fe4ed7e" />
<img width="768" alt="Screenshot 2025-04-29 at 9 31 51 AM" src="https://github.com/user-attachments/assets/975bfb84-bdf4-4eac-b7cc-afdb3ed6143a" />

**Summary**

| Model | Voltage per 1/3° | ADC Needed | Affected by 10 mV Noise? |
|-------|------------------|------------|---------------------------|
| **360° Range** | ~4.63 mV | ≥11 bits | Yes – noise overwhelms signal |
| **60° Range**  | ~27.8 mV | ≥8 bits  | No – signal exceeds noise |

Let me know if you want a diagram or table to help visualize this!



Digital to Analog Converter (DAC): 
- Need an external chip to do analog on AVR
- MCP48x2 takes 2 bytes of input over SPI
- Connects to Arduino with SDI (MOSI) SCK and CS
- Input gives digital data and three control bits


Actuators (outputs): 
- Motors
- Relays
- LEDs / lights
- Displays
- Speakers/beepers
- Magnetic fields


Actuator Interfaces: 
- Analog voltage level output (none on Arduino) – need DAC
- PWM duty cycle
- Pulse width
- Relay controlled by digital signal
- Serial interface
- Many sensors and actuators have their own embedded microprocessor

Servo Motors: 
- A servo motor will go to a commanded position.
- It uses built-in feedback
- Usual interface is pulse width
- Servos are often used with
  - Limit switches to keep from going too far
  - A home switch
- Lab 5A and chapter 11 of the text deal with servo motors



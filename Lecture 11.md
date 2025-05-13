# (5/13/25) Making Waves.pptx and Subsumption.pptx

## Things I'm confused about 

## After class TODO

## Notes Making Waves

### Synthesizers
- A good quality organ or synthesizer combines sine waves.
- The fundamental frequency makes the note.
- The timbre of instruments makes them sound different.
- Timbre consists of several things.
- One of the most important is subharmonics.

### % Power in Notes
<img width="594" alt="Screenshot 2025-05-13 at 9 01 54 AM" src="https://github.com/user-attachments/assets/5ca27b20-6784-4464-ac77-95890cafb786" />

### AVR output
- On AVR the only output is High or Low
- We can play A4 @ 440 Hz as a square wave:
- High for 1,136 μs and low for 1,136 μs
- How do we get a sine wave?

### Low Pass Filter
- R and C change fc
- At cut-off frequency, only 70% of voltage gets through.
- At higher frequencies there will be less voltage.
<img width="138" alt="Screenshot 2025-05-13 at 9 03 16 AM" src="https://github.com/user-attachments/assets/8c7a2748-b143-44ff-9464-820cfe939140" />

### Arduino PWM
- Default frequencies are 490 or 980
- We can set PWM to be any frequency
- Filtering will make it close to a sine wave
- PWM does not depend on CPU

### Filtered PWM Solution 
- Set PWM to a fast rate
- 𝑓_𝑃𝑊𝑀=𝑓_𝐶𝑃𝑈/(𝐷𝑖𝑣𝑖𝑠𝑜𝑟 ∙𝑆𝑡𝑒𝑝𝑠)
- E.G. 16,000,000/ (1*256) = 62,500 Hz
- A 440 Hz note would have 142 PWM clicks
- Suppose we sample the 440 Hz sine wave at 20 points
- Each point would have 7 PWM cycles
- We can use PWM to fake an analog voltage and smooth it with a low-pass filter

### Overflow time 
Modes 
- Normal
- Compare Output
- Waveform Generation
<img width="441" alt="Screenshot 2025-05-13 at 9 13 19 AM" src="https://github.com/user-attachments/assets/c4ff5172-bfb1-428e-b28b-0bbbc126d2d8" />

### Full Timer 
<img width="401" alt="Screenshot 2025-05-13 at 9 13 44 AM" src="https://github.com/user-attachments/assets/a1fe9183-ce8e-4601-9859-da73a95f14e9" />

### Two outputs
- Each timer has two Output Control Registers (OCRnA, OCRnB)
- Each timer has two outputs for Waveform Generation.
- Uno has three timers and six PWM outputs
- Mega has six timers and 12 PWM

### PWM on UNO
might be wrong slightly

<img width="460" alt="Screenshot 2025-05-13 at 9 15 53 AM" src="https://github.com/user-attachments/assets/3d9670ac-5d5f-4564-bb1f-1066fef7ce0e" />


### PWM (Waveform Generation Mode)
<img width="424" alt="Screenshot 2025-05-13 at 9 18 59 AM" src="https://github.com/user-attachments/assets/34a64fec-b192-45b9-a021-af0615054f43" />

### Waveform Generation
<img width="440" alt="Screenshot 2025-05-13 at 9 19 34 AM" src="https://github.com/user-attachments/assets/71aba5da-9a4e-492e-a0d8-0a9a771c7b80" />


### Maximum PWM speed
<img width="669" alt="Screenshot 2025-05-13 at 9 22 33 AM" src="https://github.com/user-attachments/assets/ba88ae39-26ca-4ed6-8e31-9094b7346509" />

---
bunch of pics:
compare outputs
clock divisors
output compare registers

---
### Direct-Digital Synthesis (DDS)
- Due has two analog outputsBut Due has different registers and architecture
- Once you can make analog output, drive it from a table
- The fast way to make sine is table-driven
- The same technique works for complex waveforms

### Sine wave notes
- Set up a fast PWM
- Run PWM output through a low-pass filter
- Set up a table
- At the right time, write a value from the table to PWM

### To go an octave up, skip every other sample 
<img width="342" alt="Screenshot 2025-05-13 at 9 31 26 AM" src="https://github.com/user-attachments/assets/fb2eeefc-08d4-4ca9-9ab4-dd6c9e807f78" />

### Arbitrary notes
- If original note was A4 (440 Hz, step size 1), octave is A5 (880 Hz, step size 2)
- We could get E5 (660 Hz) with a step size of 1.5
- Step size 1.5 means we alternate stepping by 1 and 2
- We can use this trick to get any note.

play a note

### Can use any waveform
- This technique works for more complicated waves than sine.
You can generate a base waveform for any instrument.
Instead of a note, the waveform can be speech
Willson shows how to make a talking instrument on p. 396-407

## Notes Subsumption

### Early Artificial Intelligence
<img width="437" alt="Screenshot 2025-05-13 at 9 50 47 AM" src="https://github.com/user-attachments/assets/c286b365-1834-411c-a2cd-a2c8275430d1" />

### Original MUSHR design
- Stock RC car has battery, motor, steering and RC controller.
- MUSHR upgraded transmission and replaced RC controller with game controller
- Second battery provides power to Jetson Nano.
- Nano controls car over USB using skateboard controller (VESC)
- Nano has USB connector to depth camera and hobbyist Lidar. 


### Subsumption Architecture
<img width="532" alt="Screenshot 2025-05-13 at 10 01 18 AM" src="https://github.com/user-attachments/assets/bdc68a06-ca4f-42d1-8e9a-0e251e80c38e" />

### Augmented finite state machine
FSM plus a timer that can initiate a state change.
- Networks are built by wiring input ports to output ports.
- Inputs receive short messages.
- All messages have the same number of bits.
<img width="366" alt="image" src="https://github.com/user-attachments/assets/0e1b6c49-df9f-4077-958a-89d414d51b62" />

### Highly Distributed System
- No central planner
- No world model
- Each sensor and actuator has its own simple microprocessor
- Similar to a chain  of reflexes

### AFSM
- Inputs may be suppressed by messages that arrive from elsewhere and block the normal input.
- Outputs may be inhibited by other messages that block normal output for a specified time.
- A reset state can force each FSM to state nil.
- There is no shared memory.
- There are no global world models.
- No traditional AI planning.

---
wandering robot slide 
- 13-16

hallway following robot
- 17 - 20

Genghis robot **(and other stuff)**
- 21 - 31 

Tom and jerry robot
- 32 - 39

---

















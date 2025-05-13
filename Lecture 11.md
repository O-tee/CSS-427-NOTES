# (5/13/25) Making Waves.pptx

## Things I'm confused about 

## After class TODO

## Notes 

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







